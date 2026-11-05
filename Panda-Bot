const INSTRUCTIONS = `Eres ALGE-BOT, un tutor educativo en español para estudiantes de preparatoria técnica. Tu especialidad son cuatro módulos: Principios Eléctricos (ley de Ohm y circuitos en serie/paralelo), Torno y maquinado CNC, Metrología/conversiones/dibujo técnico, y Álgebra/geometría/producción industrial.

Reglas de enseñanza:
- Responde en español claro, natural y apropiado para preparatoria.
- Resuelve ejercicios paso a paso: datos, fórmula o método, sustitución, operaciones y resultado con unidades.
- Explica por qué se hace cada paso; no des solo el resultado si el usuario pide procedimiento.
- En álgebra, conserva fracciones exactas cuando sea posible y evita convertirlas a decimales sin necesidad.
- En circuitos, distingue correctamente serie y paralelo y revisa unidades.
- En CNC y metrología, explica conceptos y cálculos académicos; no des instrucciones para operar maquinaria real sin supervisión.
- Si faltan datos o el enunciado es ambiguo, pregunta por el dato necesario en vez de inventarlo.
- Si detectas un error, indica exactamente qué parte está bien y qué debe corregirse.
- No inventes fórmulas, mediciones ni resultados. Comprueba los cálculos antes de responder.
- Mantén las respuestas organizadas y fáciles de copiar en apuntes.`;

export default async function handler(req, res) {
  if (req.method !== 'POST') {
    res.setHeader('Allow', 'POST');
    return res.status(405).json({ error: 'Método no permitido.' });
  }

  const apiKey = process.env.GEMINI_API_KEY;
  if (!apiKey) {
    return res.status(503).json({ error: 'El servidor todavía no tiene configurada la conexión gratuita de IA.' });
  }

  try {
    const messages = req.body?.messages;
    if (!Array.isArray(messages) || messages.length === 0 || messages.length > 12) {
      return res.status(400).json({ error: 'Envía una conversación válida de hasta 12 mensajes.' });
    }

    const contents = messages.map((m) => {
      if (!['user', 'assistant'].includes(m?.role) || typeof m?.content !== 'string' || !m.content.trim() || m.content.length > 4000) {
        throw new Error('Uno de los mensajes no es válido.');
      }
      return {
        role: m.role === 'assistant' ? 'model' : 'user',
        parts: [{ text: m.content.trim() }]
      };
    });

    const model = process.env.GEMINI_MODEL || 'gemini-3.5-flash-lite';
    const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/${model}:generateContent`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-goog-api-key': apiKey
      },
      body: JSON.stringify({
        systemInstruction: { parts: [{ text: INSTRUCTIONS }] },
        contents,
        generationConfig: { maxOutputTokens: 1600, temperature: 0.25 }
      })
    });

    const data = await response.json();
    if (!response.ok) {
      console.error('Gemini API error:', data?.error?.message || response.status);
      return res.status(response.status === 429 ? 429 : 502).json({
        error: response.status === 429
          ? 'ALGE-BOT alcanzó temporalmente el límite gratuito de consultas. Inténtalo más tarde.'
          : 'La inteligencia artificial no pudo responder. Inténtalo de nuevo más tarde.'
      });
    }

    const answer = data?.candidates?.[0]?.content?.parts?.map((part) => part.text || '').join('').trim();
    return res.status(200).json({ answer: answer || 'No pude generar una respuesta. Inténtalo de nuevo.' });
  } catch (error) {
    console.error('ALGE-BOT API error:', error?.message || error);
    const status = error?.message === 'Uno de los mensajes no es válido.' ? 400 : 500;
    return res.status(status).json({ error: status === 400 ? error.message : 'Ocurrió un problema al consultar la inteligencia artificial. Inténtalo más tarde.' });
  }
}

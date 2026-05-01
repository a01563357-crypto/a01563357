# Chatbot Educativo con IA Generativa
**Proyecto final · 2 semanas · 6° Semestre PrepaTec · Equipos de 2 – 3 personas**

---

## Descripción general

En este proyecto, los equipos diseñarán, construirán y evaluarán un asistente de estudio inteligente usando la API de un modelo de lenguaje grande (LLM) de su elección. El proyecto no se limita a un proveedor específico: pueden usar Claude (Anthropic), GPT (OpenAI), Gemini (Google) u otro modelo accesible con API pública.

El objetivo central no es solo aprender a "usar" la IA, sino aprender a instruirla con precisión, someterla a pruebas rigurosas y mejorarla de forma iterativa. Al finalizar, cada equipo habrá construido una herramienta real y adquirido las competencias fundamentales de la ingeniería de sistemas de IA:

- **Diseño pedagógico:** definir cómo debe enseñar un sistema de IA
- **Ingeniería de prompts:** redactar instrucciones precisas que determinen el comportamiento del modelo
- **Programación web básica:** conectar una interfaz HTML/JavaScript con una API externa
- **Evaluación de sistemas de IA:** probar fallos, sesgos y comportamientos inesperados
- **Comunicación técnica:** presentar decisiones de diseño a una audiencia no técnica

---

## Proveedores de IA compatibles

El código base entregado incluye adaptadores listos para los tres proveedores principales. El equipo solo necesita elegir uno, obtener su API key gratuita o de prueba y cambiar una línea del archivo:

| Proveedor | Modelo por defecto | Dónde obtener la key | Notas para estudiantes |
|---|---|---|---|
| Claude | claude-sonnet-4 | console.anthropic.com | Capa gratuita disponible. System prompt como campo separado. |
| OpenAI GPT | gpt-4o-mini | platform.openai.com/api-keys | Créditos de prueba al registrarse. System prompt como primer mensaje. |
| Gemini | gemini-2.0-flash | aistudio.google.com/apikey | Gratuito con cuenta Google. Instrucciones en system_instruction. |

**Para cambiar de proveedor:** abre el archivo `chatbot-educativo-base.html`, localiza la línea `const PROVIDER = "claude"` y reemplaza el valor por `"openai"` o `"gemini"`. El resto del código no requiere modificaciones.

---

## Estructura del proyecto

| # | Duración estimada | Fase | Entregable principal |
|---|---|---|---|
| 1 | 2 hrs | Diseño pedagógico | Ficha de diseño del bot |
| 2 | 3 hrs | Ingeniería de prompts | System prompt documentado |
| 3 | 4 – 5 hrs | Construcción de la interfaz | Archivo HTML funcional |
| 4 | 2 – 3 hrs | Pruebas y mejora iterativa | Hoja de registro de pruebas |
| 5 | 1 – 2 hrs | Demo y presentación final | Presentación + reflexión escrita |

---

## Fase 1: Diseño pedagógico (22 de Abril)
**Duración: 2 horas**

### Objetivo

Antes de escribir código, el equipo define el propósito educativo del chatbot: para qué sirve, a quién le habla y cómo enseña. Este proceso obliga a pensar como docentes, no solo como desarrolladores de software.

### Actividades

- Elegir la materia y los temas del semestre que cubrirá el bot (deben ser temas reales del plan de estudios de 6° semestre).
- Definir la personalidad: nombre, tono (formal, amigable, socrático) y un rasgo distintivo que haga al bot memorable.
- Establecer reglas pedagógicas: qué debe hacer cuando alguien pide respuestas directas de tarea, cuando el estudiante se frustra o cuando la pregunta está fuera del temario.
- Elegir el proveedor de IA que usará el equipo y verificar que la API key funciona antes de continuar.
- Completar la Ficha de Diseño del Bot (entregable de la fase).

### Ficha de diseño del bot (plantilla)

El equipo llena el siguiente formulario y lo entrega antes de avanzar a la Fase 2:

| Campo | Respuesta |
|---|---|
| Nombre del bot | |
| Materia y nivel | |
| Proveedor de IA elegido | Claude / OpenAI GPT / Gemini / Otro: ___ |
| 3 temas principales que cubrirá | |
| Tipo de estudiante al que le habla | Ej: estudiante curioso / bloqueado / de último minuto |
| Estilo de enseñanza | Ej: socrático, explicativo, motivacional |
| ¿Qué hará si alguien pide respuestas directas? | |
| ¿Qué hará si la pregunta está fuera del temario? | |
| Personalidad en una oración | |

### Entregable Fase 1: Ficha de diseño del bot (22 de Abril)

- Ficha completa con todos los campos llenados
- Proveedor de IA seleccionado y justificado brevemente
- API key probada y confirmada como funcional (el equipo lo indica en la ficha)

### Rúbrica de evaluación: Fase 1

| Criterio | Excelente (4) | Satisfactorio (3) | En desarrollo (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Claridad del propósito pedagógico** (30%) | El bot tiene una materia, nivel, público y propósito educativo específicos y coherentes entre sí. | El propósito es claro pero algún elemento (público o nivel) es vago. | Se menciona una materia pero sin propósito educativo definido. | No se identifica un propósito pedagógico claro. |
| **Reglas pedagógicas** (35%) | Se definen reglas explícitas y bien pensadas para tareas, frustración y preguntas fuera de tema. | Hay reglas pero son genéricas o incompletas. | Se mencionan reglas pero sin explicar cómo el bot las aplicará. | No hay reglas pedagógicas definidas. |
| **Selección y verificación del proveedor** (20%) | Proveedor elegido, justificado brevemente y API key verificada como funcional. | Proveedor elegido y key obtenida, sin verificación documentada. | Proveedor elegido pero sin obtener API key aún. | No se eligió proveedor ni se gestionó la key. |
| **Completitud de la ficha** (15%) | Todos los campos llenados con información específica y útil. | Al menos 7 de 9 campos completados. | Al menos 5 campos completados. | Menos de 5 campos o ficha no entregada. |

---

## Fase 2: Ingeniería de prompts (27 de abril)
**Duración: 3 horas**

### Objetivo

El system prompt es el conjunto de instrucciones que le dice al modelo cómo comportarse. Es, literalmente, el código pedagógico del chatbot. Esta fase enseña que la calidad del bot depende casi enteramente de qué tan bien está instruido, independientemente del proveedor o modelo elegido.

### Concepto clave: el system prompt

Aunque cada proveedor lo implementa de forma diferente a nivel técnico, el concepto es universal: un bloque de texto que el modelo lee antes de cada conversación y que define su rol, restricciones y comportamiento.

### Componentes del system prompt a diseñar

- **Rol y contexto:** quién es el bot, en qué materia es experto y para qué nivel educativo trabaja.
- **Restricciones de contenido:** temas que sí cubre y temas que están fuera de su alcance.
- **Estilo pedagógico:** cómo explica (con analogías, ejemplos locales, preguntas de verificación, etc.).
- **Manejo de tareas:** qué hace cuando el estudiante pide respuestas directas en lugar de comprensión.
- **Tono y longitud de respuestas:** máximo de párrafos, nivel de formalidad, uso de ejemplos cotidianos.
- **Manejo de preguntas fuera de tema:** cómo redirige sin ser brusco.

### Ejercicio de iteración

Los equipos prueban su prompt directamente en el chat del proveedor elegido (Claude.ai, ChatGPT o Google AI Studio) antes de escribir código. Para cada prueba registran:

- Pregunta de prueba enviada al modelo
- Respuesta obtenida
- Problema identificado (si hay)
- Modificación aplicada al prompt

Se requieren al menos 5 pruebas documentadas antes de considerar el prompt como versión 1.0.

### Entregable Fase 2: System prompt documentado (27 de abril)

- Archivo `.txt` o `.md` con el system prompt final (versión 1.0)
- Tabla de iteraciones con al menos 5 pruebas: pregunta / respuesta / problema / corrección
- Nota al pie indicando el proveedor y modelo usado para las pruebas

### Rúbrica de evaluación: Fase 2

| Criterio | Excelente (4) | Satisfactorio (3) | En desarrollo (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Cobertura de los 6 componentes** (25%) | Los 6 componentes están presentes, son específicos y coherentes entre sí. | Al menos 5 componentes presentes con buena especificidad. | Al menos 4 componentes, pero algunos son vagos. | Menos de 4 componentes o el prompt es genérico. |
| **Calidad pedagógica del prompt** (35%) | El prompt produce respuestas que guían sin revelar respuestas directas, usan analogías y terminan con preguntas de verificación. | El prompt guía bien pero no siempre cierra con verificación. | El prompt da algunas guías pero en ocasiones responde directamente. | El prompt no diferencia entre guiar y dar respuestas. |
| **Proceso de iteración documentado** (30%) | 5+ iteraciones documentadas con problema identificado y corrección aplicada claramente. | 5 iteraciones documentadas pero con conexión débil entre problema y corrección. | 3 – 4 iteraciones documentadas. | Menos de 3 pruebas o sin documentación. |
| **Adaptación al proveedor elegido** (10%) | El equipo explica correctamente cómo su proveedor maneja el system prompt y lo aplicaron bien. | Lo aplicaron bien pero sin explicación. | Hay confusión entre cómo funciona en distintos proveedores. | No consideraron las diferencias entre proveedores. |

---

## Fase 3: Construcción de la interfaz (28 Abril)
**Duración: 4 – 5 horas**

### Objetivo

Los equipos integran el system prompt diseñado en la Fase 2 dentro de una aplicación web funcional que conecta con la API del proveedor elegido. No se requiere experiencia previa en programación: el archivo base entregado incluye toda la estructura; los estudiantes modifican la sección de configuración.

### Archivo base entregado

Se proporciona el archivo `chatbot-educativo-base.html`, que incluye:

- Interfaz de chat completa (envío de mensajes, historial, indicador de escritura)
- Adaptadores de API para Claude, OpenAI GPT y Gemini integrados
- Sección `CONFIG` claramente delimitada con comentarios en español
- Mensajes de error descriptivos cuando falta la API key o hay problemas de conexión
- Pantalla de bienvenida con preguntas de inicio rápido personalizables

### Lo que los estudiantes modifican

Solo es necesario editar el bloque de configuración al inicio del script. Las variables clave son:

| Variable | Qué controla | Ejemplo |
|---|---|---|
| `PROVIDER` | Qué API usar | `"claude"` \| `"openai"` \| `"gemini"` |
| `API_KEY` | Llave del proveedor elegido | `"sk-ant-..."` o `"sk-..."` o `"AIza..."` |
| `CONFIG.systemPrompt` | El prompt diseñado en Fase 2 | Texto completo del system prompt |
| `CONFIG.botName` | Nombre del chatbot | `"MateBot"`, `"HistorIA"`, etc. |
| `CONFIG.starterQuestions` | Preguntas de inicio rápido | Lista de 4 – 5 preguntas del temario |

### Extensiones opcionales (para equipos avanzados)

- Cambiar la paleta de colores del tema visual para reflejar la materia elegida
- Usar speech-to-text para que el usuario "diga" la pregunta
- Agregar un contador de mensajes
- Implementar la opción de exportar la conversación como archivo `.txt`
- Agregar botones de "No entendí" y "Dame otro ejemplo" conectados a prompts predefinidos
- Comparar el comportamiento del mismo system prompt en dos proveedores distintos

### Entregable Fase 3: Aplicación web funcional (28 Abril)

- Archivo `chatbot-educativo-base.html` modificado con el nombre, materia y system prompt del equipo
- La aplicación responde correctamente a preguntas del temario usando el proveedor elegido
- La pantalla de bienvenida muestra el nombre del bot y al menos 4 preguntas de inicio
- Captura de pantalla de una conversación de prueba exitosa (mínimo 4 intercambios)

### Rúbrica de evaluación: Fase 3

| Criterio | Excelente (4) | Satisfactorio (3) | En desarrollo (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Funcionalidad del chatbot** (35%) | El bot responde correctamente, mantiene el contexto de la conversación y el indicador de escritura funciona. | El bot responde pero pierde el contexto en conversaciones largas. | El bot funciona de forma intermitente o con errores visibles. | El archivo no conecta con la API o no funciona. |
| **Integración del system prompt** (30%) | El system prompt de Fase 2 está íntegramente integrado y el comportamiento del bot lo refleja con fidelidad. | El prompt está integrado pero el comportamiento del bot difiere en algunos aspectos. | El prompt está integrado parcialmente. | Se usa el prompt de ejemplo sin modificaciones propias. |
| **Personalización visual y de contenido** (20%) | Nombre propio, emoji, materia y preguntas de inicio son originales y coherentes con el diseño de Fase 1. | La mayoría de elementos están personalizados. | Solo el nombre fue cambiado. | Sin personalizaciones: el archivo entregado es idéntico al base. |
| **Manejo de errores** (15%) | La app muestra mensajes de error claros y descriptivos si falla la API key o la conexión. | Hay manejo de errores básico pero los mensajes son técnicos o confusos. | La app falla silenciosamente sin informar al usuario. | Sin manejo de errores. |

---

## Fase 4: Pruebas y mejora iterativa (29 Abril)
**Duración: 2 – 3 horas**

### Objetivo

Esta fase enseña que la ingeniería de IA no termina cuando el código funciona. Los equipos someten su chatbot a pruebas sistemáticas, documentan fallos y aplican correcciones al system prompt. El proceso de "probar, encontrar el fallo, corregir y volver a probar" es el flujo de trabajo real de quienes desarrollan sistemas de IA.

### Tipos de prueba a realizar

- **Pruebas de calidad pedagógica:** ¿El bot responde correctamente preguntas del temario? ¿Adapta la dificultad? ¿Guía sin dar respuestas directas?
- **Pruebas de robustez:** ¿Qué pasa si la pregunta está mal redactada? ¿Responde bien en oraciones largas o con faltas de ortografía?
- **Pruebas de límites:** ¿Qué hace cuando alguien pide la respuesta completa de un examen? ¿Maneja bien preguntas de otra materia?
- **Pruebas de sesgo:** ¿El bot trata igual distintos tipos de estudiantes o preguntas? ¿Hay temas donde responde peor?
- **Prueba de usuario real:** un compañero de otro equipo usa el bot durante 5 minutos y anota su experiencia.

### Plantilla de registro de pruebas

| # | Pregunta enviada | Respuesta obtenida (resumen) | Tipo de prueba | Problema encontrado / Corrección aplicada |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |
| 8 | | | | |
| 9 | | | | |
| 10 | | | | |

### Entregable Fase 4: Hoja de registro de pruebas (29 Abril)

- Tabla con al menos 10 pruebas documentadas (incluyendo al menos una de cada tipo)
- Al menos 3 filas con correcciones aplicadas al system prompt
- Versión 2.0 del system prompt reflejando las mejoras (archivo `.txt` o `.md` actualizado)
- Párrafo de reflexión: ¿cuál fue el fallo más sorprendente y qué les enseñó sobre los LLMs?

### Rúbrica de evaluación: Fase 4

| Criterio | Excelente (4) | Satisfactorio (3) | En desarrollo (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Cobertura de tipos de prueba** (25%) | Al menos 10 pruebas cubriendo los 5 tipos: pedagógica, robustez, límites, sesgo y usuario real. | 8 – 10 pruebas cubriendo al menos 4 tipos. | 5 – 7 pruebas, mayormente del mismo tipo. | Menos de 5 pruebas o sin variedad de tipos. |
| **Calidad del análisis de fallos** (35%) | Cada fallo está descrito con precisión: qué ocurrió, por qué ocurrió y cómo se corrigió en el prompt. | Los fallos están descritos pero la conexión entre causa y corrección es débil. | Se identifican fallos pero sin análisis de causa. | No se identifican fallos o se asume que el bot funciona perfectamente. |
| **Mejoras aplicadas al prompt** (25%) | Al menos 3 correcciones aplicadas al system prompt con justificación clara y versión 2.0 entregada. | 2 correcciones aplicadas y versión 2.0 entregada. | 1 corrección aplicada o versión 2.0 muy similar a la 1.0. | Sin correcciones o sin versión 2.0. |
| **Reflexión sobre comportamiento del LLM** (15%) | El párrafo de reflexión demuestra comprensión de por qué los LLMs fallan de determinada forma y conecta con conceptos de IA. | La reflexión describe el fallo pero sin conectar con el funcionamiento del modelo. | Reflexión superficial o muy breve. | Sin reflexión. |

---

## Fase 5: Demo y presentación final (Lunes 4 y Miércoles 6 de Mayo)
**Duración: 1 – 2 horas**

### Objetivo

Cada equipo demuestra su chatbot en funcionamiento frente al grupo, comunica las decisiones de diseño que tomaron y reflexiona sobre lo que aprendieron sobre la IA. La capacidad de explicar un sistema técnico a una audiencia no técnica es una habilidad central en cualquier carrera relacionada con tecnología.

### Formato de presentación

- Duración: 3 – 4 minutos de demo en vivo + 2 minutos de preguntas del grupo
- El bot debe funcionar en tiempo real durante la presentación
- Se permite que alguien del público haga una pregunta real al chatbot durante la demo

### Estructura sugerida

| Tiempo | Contenido |
|---|---|
| 30 seg | Presentación: nombre del bot, materia, proveedor de IA elegido y por qué lo eligieron. |
| 30 seg | Decisión pedagógica más importante que tomaron en el system prompt y cómo la aplicaron. |
| 2 min | Demo en vivo: 2 – 3 conversaciones que ilustren el comportamiento del bot, incluyendo un caso de fallo conocido y cómo lo resolvieron. |
| 1 min | Reflexión: ¿qué aprendieron sobre cómo funcionan los LLMs que no sabían antes? |

### Entregable Fase 5: Demo y reflexión escrita

- Demo en vivo funcional frente al grupo (el bot debe responder en tiempo real)
- Reflexión escrita individual (1 párrafo por integrante): ¿qué cambiarías del sistema si tuvieras más tiempo?
- Versión final del archivo HTML y del system prompt (versión 2.0 o superior)

### Rúbrica de evaluación: Fase 5

| Criterio | Excelente (4) | Satisfactorio (3) | En desarrollo (2) | Insuficiente (1) |
|---|---|---|---|---|
| **Demo en vivo** (30%) | El bot funciona en tiempo real, se muestran al menos 3 conversaciones ilustrativas y se demuestra el manejo de un caso límite. | El bot funciona y se muestran 2 conversaciones. | El bot funciona pero la demo es muy breve o poco ilustrativa. | El bot no funciona durante la presentación. |
| **Claridad en la comunicación de decisiones** (25%) | El equipo explica con claridad por qué tomaron cada decisión pedagógica y técnica, conectando Fase 1, 2 y 3. | Explican las decisiones pero sin conectar las fases. | Describen el bot pero no las decisiones de diseño. | Sin explicación de decisiones. |
| **Profundidad de la reflexión** (25%) | La reflexión demuestra comprensión real de cómo funciona un LLM y conecta con al menos un concepto del campo (hallucination, context window, prompt injection, etc.). | La reflexión es honesta y menciona limitaciones concretas del sistema. | Reflexión superficial o enfocada solo en aspectos técnicos sin reflexión sobre IA. | Sin reflexión o reflexión de una oración. |
| **Reflexión escrita individual** (20%) | Cada integrante entrega un párrafo propio con ideas distintas y concretas sobre cómo mejoraría el sistema. | Todos entregan el párrafo pero con ideas similares entre sí. | Al menos la mitad del equipo entrega el párrafo. | Sin reflexión escrita o entregada por solo una persona. |

---

## Calificación global del proyecto

| Fase | Nombre | Peso | Entregable principal |
|---|---|---|---|
| 1 | Diseño pedagógico | 15% | Ficha de diseño del bot |
| 2 | Ingeniería de prompts | 25% | System prompt documentado con iteraciones |
| 3 | Construcción de la interfaz | 25% | Archivo HTML funcional y personalizado |
| 4 | Pruebas y mejora iterativa | 20% | Hoja de registro + system prompt v2.0 |
| 5 | Demo y presentación final | 15% | Demo en vivo + reflexión escrita individual |

**Escala de calificación:**

| Nivel | Promedio ponderado |
|---|---|
| Excelente | ≥ 3.5 |
| Satisfactorio | 2.5 – 3.4 |
| En desarrollo | 1.5 – 2.4 |
| Insuficiente | < 1.5 |


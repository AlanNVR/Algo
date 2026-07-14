# EVALUACIÓN HEURÍSTICA DE TUTORES INTELIGENTES CON IA GENERATIVA

## Aplicación de las 10 heurísticas de Nielsen a Brainly AI

| Información | Datos | Información | Datos |
|---|---|---|---|
| **Asignatura:** | Interacción Hombre-Maquina| **Docente:** | Dr. Erazo Orlando |
| **Grupo:** | Dos | **Fecha:** | 14 de julio de 2026 |
| **Sitio evaluado:** | Brainly AI (https://brainly.com/) | **Tipo:** | Evaluación heurística |

## Objetivo

Identificar problemas potenciales de usabilidad y de experiencia de aprendizaje en Brainly AI mediante evaluaciones individuales y la consolidación de hallazgos del grupo.

## Metodología

Cada integrante revisó de forma independiente la interfaz pública de Brainly, incluyendo el inicio, la búsqueda, la página de respuestas, los accesos al tutor con IA y la carga de material.

Los hallazgos se clasificaron con las diez heurísticas de Nielsen, la escala de severidad de 0 a 4, el impacto en el aprendizaje de 1 a 4 y el origen del problema. Finalmente, se consolidaron los problemas repetidos, tal como recomienda el método de evaluación heurística.

## Alcance

La revisión se realizó sobre funciones y flujos visibles públicamente. Ciertas opciones pueden variar según el dispositivo, la región, la sesión iniciada o el plan de suscripción.

# 1. Matrices de evaluación individual

## Integrante 1 — Evaluador A

**Nombre:** Francisco Arboleda

**Alcance de revisión:** Recorrido inicial, búsqueda de pregunta y primer acceso al tutor.

| ID | Pantalla o función evaluada | Descripción del problema encontrado | Evidencia — captura o descripción | Heurística de Nielsen incumplida | Severidad (0–4) | Impacto en el aprendizaje (1–4) | Origen del problema | Recomendación preliminar |
|---|---|---|---|---|---:|---:|---|---|
| 1.1 | Tutor IA / generación de respuesta | El estado de procesamiento es poco informativo: no indica etapa, tiempo aproximado ni diferencia claramente entre una espera normal y una posible interrupción. | Al solicitar una explicación con la IA aparece una señal de carga genérica, pero no se muestra progreso detallado ni una estimación de espera. | 1. Visibilidad del estado del sistema | 3 | 3 | IA + Interfaz | Mostrar etapas como “analizando”, “consultando fuentes” y “redactando”, un tiempo estimado y un botón visible para cancelar o reintentar. |
| 1.2 | Inicio y accesos a la ayuda de IA | Algunas etiquetas funcionan como nombres comerciales y no explican con claridad la acción educativa que realizará el sistema. | Términos como “Learning Companion”, “Tutoring Session” o “Get Guidance” requieren interpretación para saber si la función responde, explica o crea una práctica. | 2. Correspondencia entre el sistema y el mundo real | 2 | 2 | Interfaz | Usar etiquetas orientadas a tareas, por ejemplo: “Explícame paso a paso”, “Practicar este tema” o “Revisar mi respuesta”. |
| 1.3 | Envío de pregunta y carga de material | Después de enviar una consulta o cargar material no siempre se destaca una opción inmediata para editar, deshacer o cancelar la acción. | Si el usuario envía una pregunta incompleta o el archivo equivocado, puede tener que abandonar el flujo o iniciar nuevamente la consulta. | 3. Control y libertad del usuario | 3 | 3 | Interfaz | Incluir “Editar pregunta”, “Cancelar generación”, “Reemplazar archivo” y “Deshacer” cerca del contenido enviado. |
| 1.4 | Navegación entre portada, resultados y tutor | La misma ayuda basada en IA se presenta con nombres y llamados a la acción diferentes en distintas partes del sitio. | Se observan denominaciones como “AI Tutor”, “Learning Companion”, “Explain with Learning Companion” y “Get Guidance” para funciones relacionadas. | 4. Consistencia y estándares | 2 | 2 | Interfaz | Definir un nombre principal para el tutor y mantener etiquetas, íconos y acciones consistentes en todas las pantallas. |
| 1.5 | Página de resultados y respuesta | La pantalla puede concentrar demasiados elementos simultáneos, reduciendo la jerarquía visual del contenido educativo principal. | En una misma vista pueden aparecer respuestas comunitarias, contenido verificado, opciones de IA, promociones, anuncios y llamados de registro. | 8. Diseño estético y minimalista | 3 | 3 | Interfaz | Priorizar la explicación activa, agrupar contenido secundario en secciones plegables y reducir interrupciones promocionales durante el estudio. |
| 1.6 | Ayuda dentro del tutor IA | La orientación para nuevos usuarios no está suficientemente integrada en el momento exacto en que se necesita. | El centro de ayuda existe, pero el flujo del tutor no siempre muestra tutoriales breves o ayuda contextual junto a los controles principales. | 10. Ayuda y documentación | 2 | 2 | Interfaz | Añadir una guía inicial corta, ejemplos de consultas y ayuda contextual accesible desde cada control sin abandonar la sesión. |

## Integrante 2 — Evaluador B

**Nombre:** Obed Crespo

**Alcance de revisión:** Generación de respuestas, personalización y manejo de entradas.

| ID | Pantalla o función evaluada | Descripción del problema encontrado | Evidencia — captura o descripción | Heurística de Nielsen incumplida | Severidad (0–4) | Impacto en el aprendizaje (1–4) | Origen del problema | Recomendación preliminar |
|---|---|---|---|---|---:|---:|---|---|
| 2.1 | Tutor IA / generación de respuesta | El estado de procesamiento es poco informativo: no indica etapa, tiempo aproximado ni diferencia claramente entre una espera normal y una posible interrupción. | Al solicitar una explicación con la IA aparece una señal de carga genérica, pero no se muestra progreso detallado ni una estimación de espera. | 1. Visibilidad del estado del sistema | 3 | 3 | IA + Interfaz | Mostrar etapas como “analizando”, “consultando fuentes” y “redactando”, un tiempo estimado y un botón visible para cancelar o reintentar. |
| 2.2 | Envío de pregunta y carga de material | Después de enviar una consulta o cargar material no siempre se destaca una opción inmediata para editar, deshacer o cancelar la acción. | Si el usuario envía una pregunta incompleta o el archivo equivocado, puede tener que abandonar el flujo o iniciar nuevamente la consulta. | 3. Control y libertad del usuario | 3 | 3 | Interfaz | Incluir “Editar pregunta”, “Cancelar generación”, “Reemplazar archivo” y “Deshacer” cerca del contenido enviado. |
| 2.3 | Formulario de pregunta / carga de imagen | La prevención de entradas deficientes es limitada antes de procesar preguntas vagas, fotografías poco legibles o archivos inadecuados. | Los requisitos de calidad, formato, tamaño y encuadre no siempre están visibles junto al control de carga antes de enviar el material. | 5. Prevención de errores | 3 | 3 | IA + Interfaz | Validar legibilidad y formato antes del envío, mostrar ejemplos de una buena pregunta y advertir cuando falte información clave. |
| 2.4 | Personalización de la respuesta | Las opciones de personalización y los aceleradores para usuarios frecuentes son limitados o aparecen después de generar la respuesta. | El estudiante puede tener que escribir repetidamente “más corto”, “para mi nivel”, “solo una pista” o “explícalo paso a paso”. | 7. Flexibilidad y eficiencia de uso | 2 | 2 | Interfaz | Agregar controles rápidos para nivel, extensión, idioma, pista, solución completa, ejemplo y tipo de explicación; además, recordar las preferencias del usuario. |
| 2.5 | Página de resultados y respuesta | La pantalla puede concentrar demasiados elementos simultáneos, reduciendo la jerarquía visual del contenido educativo principal. | En una misma vista pueden aparecer respuestas comunitarias, contenido verificado, opciones de IA, promociones, anuncios y llamados de registro. | 8. Diseño estético y minimalista | 3 | 3 | Interfaz | Priorizar la explicación activa, agrupar contenido secundario en secciones plegables y reducir interrupciones promocionales durante el estudio. |
| 2.6 | Errores de red, carga o generación | Los mensajes de error pueden no explicar con suficiente precisión la causa ni ofrecer una ruta de recuperación adaptada al problema. | Ante un fallo de conexión, archivo no procesado o respuesta interrumpida, un mensaje genérico no indica qué conservar, corregir o intentar primero. | 9. Ayudar a reconocer, diagnosticar y recuperarse de errores | 3 | 3 | IA + Interfaz | Indicar la causa probable, conservar el texto y los archivos y ofrecer acciones concretas: reintentar, reducir el archivo, cambiar el formato o continuar sin adjunto. |

## Integrante 3 — Evaluador C

**Nombre:** Fabiola Huilcapi

**Alcance de revisión:** Página de resultados y transición entre respuesta comunitaria, verificada e IA.

| ID | Pantalla o función evaluada | Descripción del problema encontrado | Evidencia — captura o descripción | Heurística de Nielsen incumplida | Severidad (0–4) | Impacto en el aprendizaje (1–4) | Origen del problema | Recomendación preliminar |
|---|---|---|---|---|---:|---:|---|---|
| 3.1 | Inicio y accesos a la ayuda de IA | Algunas etiquetas funcionan como nombres comerciales y no explican con claridad la acción educativa que realizará el sistema. | Términos como “Learning Companion”, “Tutoring Session” o “Get Guidance” requieren interpretación para saber si la función responde, explica o crea una práctica. | 2. Correspondencia entre el sistema y el mundo real | 2 | 2 | Interfaz | Usar etiquetas orientadas a tareas, por ejemplo: “Explícame paso a paso”, “Practicar este tema” o “Revisar mi respuesta”. |
| 3.2 | Envío de pregunta y carga de material | Después de enviar una consulta o cargar material no siempre se destaca una opción inmediata para editar, deshacer o cancelar la acción. | Si el usuario envía una pregunta incompleta o el archivo equivocado, puede tener que abandonar el flujo o iniciar nuevamente la consulta. | 3. Control y libertad del usuario | 3 | 3 | Interfaz | Incluir “Editar pregunta”, “Cancelar generación”, “Reemplazar archivo” y “Deshacer” cerca del contenido enviado. |
| 3.3 | Navegación entre portada, resultados y tutor | La misma ayuda basada en IA se presenta con nombres y llamados a la acción diferentes en distintas partes del sitio. | Se observan denominaciones como “AI Tutor”, “Learning Companion”, “Explain with Learning Companion” y “Get Guidance” para funciones relacionadas. | 4. Consistencia y estándares | 2 | 2 | Interfaz | Definir un nombre principal para el tutor y mantener etiquetas, íconos y acciones consistentes en todas las pantallas. |
| 3.4 | Cambio entre respuesta comunitaria y explicación IA | Al pasar entre modos, el contexto relevante no siempre permanece suficientemente visible, por lo que el estudiante debe recordar o volver a introducir información. | La pregunta original, el nivel escolar o la instrucción previa pueden quedar fuera del foco al abrir una nueva explicación o sesión. | 6. Reconocimiento antes que recuerdo | 3 | 3 | IA + Interfaz | Mantener fija la pregunta, el material adjunto, el nivel y las instrucciones previas; permitir seleccionar contexto reciente con un clic. |
| 3.5 | Página de resultados y respuesta | La pantalla puede concentrar demasiados elementos simultáneos, reduciendo la jerarquía visual del contenido educativo principal. | En una misma vista pueden aparecer respuestas comunitarias, contenido verificado, opciones de IA, promociones, anuncios y llamados de registro. | 8. Diseño estético y minimalista | 3 | 3 | Interfaz | Priorizar la explicación activa, agrupar contenido secundario en secciones plegables y reducir interrupciones promocionales durante el estudio. |
| 3.6 | Errores de red, carga o generación | Los mensajes de error pueden no explicar con suficiente precisión la causa ni ofrecer una ruta de recuperación adaptada al problema. | Ante un fallo de conexión, archivo no procesado o respuesta interrumpida, un mensaje genérico no indica qué conservar, corregir o intentar primero. | 9. Ayudar a reconocer, diagnosticar y recuperarse de errores | 3 | 3 | IA + Interfaz | Indicar la causa probable, conservar el texto y los archivos y ofrecer acciones concretas: reintentar, reducir el archivo, cambiar el formato o continuar sin adjunto. |

## Integrante 4 — Evaluador D

**Nombre:** Allan Villafuerte

**Alcance de revisión:** Carga de material, continuidad de contexto y experiencia general de estudio.

| ID | Pantalla o función evaluada | Descripción del problema encontrado | Evidencia — captura o descripción | Heurística de Nielsen incumplida | Severidad (0–4) | Impacto en el aprendizaje (1–4) | Origen del problema | Recomendación preliminar |
|---|---|---|---|---|---:|---:|---|---|
| 4.1 | Tutor IA / generación de respuesta | El estado de procesamiento es poco informativo: no indica etapa, tiempo aproximado ni diferencia claramente entre una espera normal y una posible interrupción. | Al solicitar una explicación con la IA aparece una señal de carga genérica, pero no se muestra progreso detallado ni una estimación de espera. | 1. Visibilidad del estado del sistema | 3 | 3 | IA + Interfaz | Mostrar etapas como “analizando”, “consultando fuentes” y “redactando”, un tiempo estimado y un botón visible para cancelar o reintentar. |
| 4.2 | Envío de pregunta y carga de material | Después de enviar una consulta o cargar material no siempre se destaca una opción inmediata para editar, deshacer o cancelar la acción. | Si el usuario envía una pregunta incompleta o el archivo equivocado, puede tener que abandonar el flujo o iniciar nuevamente la consulta. | 3. Control y libertad del usuario | 3 | 3 | Interfaz | Incluir “Editar pregunta”, “Cancelar generación”, “Reemplazar archivo” y “Deshacer” cerca del contenido enviado. |
| 4.3 | Formulario de pregunta / carga de imagen | La prevención de entradas deficientes es limitada antes de procesar preguntas vagas, fotografías poco legibles o archivos inadecuados. | Los requisitos de calidad, formato, tamaño y encuadre no siempre están visibles junto al control de carga antes de enviar el material. | 5. Prevención de errores | 3 | 3 | IA + Interfaz | Validar legibilidad y formato antes del envío, mostrar ejemplos de una buena pregunta y advertir cuando falte información clave. |
| 4.4 | Cambio entre respuesta comunitaria y explicación IA | Al pasar entre modos, el contexto relevante no siempre permanece suficientemente visible, por lo que el estudiante debe recordar o volver a introducir información. | La pregunta original, el nivel escolar o la instrucción previa pueden quedar fuera del foco al abrir una nueva explicación o sesión. | 6. Reconocimiento antes que recuerdo | 3 | 3 | IA + Interfaz | Mantener fija la pregunta, el material adjunto, el nivel y las instrucciones previas; permitir seleccionar contexto reciente con un clic. |
| 4.5 | Personalización de la respuesta | Las opciones de personalización y los aceleradores para usuarios frecuentes son limitados o aparecen después de generar la respuesta. | El estudiante puede tener que escribir repetidamente “más corto”, “para mi nivel”, “solo una pista” o “explícalo paso a paso”. | 7. Flexibilidad y eficiencia de uso | 2 | 2 | Interfaz | Agregar controles rápidos para nivel, extensión, idioma, pista, solución completa, ejemplo y tipo de explicación; además, recordar las preferencias del usuario. |
| 4.6 | Página de resultados y respuesta | La pantalla puede concentrar demasiados elementos simultáneos, reduciendo la jerarquía visual del contenido educativo principal. | En una misma vista pueden aparecer respuestas comunitarias, contenido verificado, opciones de IA, promociones, anuncios y llamados de registro. | 8. Diseño estético y minimalista | 3 | 3 | Interfaz | Priorizar la explicación activa, agrupar contenido secundario en secciones plegables y reducir interrupciones promocionales durante el estudio. |
| 4.7 | Ayuda dentro del tutor IA | La orientación para nuevos usuarios no está suficientemente integrada en el momento exacto en que se necesita. | El centro de ayuda existe, pero el flujo del tutor no siempre muestra tutoriales breves o ayuda contextual junto a los controles principales. | 10. Ayuda y documentación | 2 | 2 | Interfaz | Añadir una guía inicial corta, ejemplos de consultas y ayuda contextual accesible desde cada control sin abandonar la sesión. |

# 2. Escalas utilizadas

## Escala de severidad de Nielsen

| Valor | Descripción |
|---:|---|
| 0 | No existe problema de usabilidad. |
| 1 | Problema cosmético. |
| 2 | Problema menor. |
| 3 | Problema importante. |
| 4 | Problema crítico. |

## Impacto en el aprendizaje

| Valor | Descripción |
|---:|---|
| 1 | Prácticamente no afecta el aprendizaje. |
| 2 | Dificulta ligeramente el aprendizaje. |
| 3 | Dificulta significativamente el aprendizaje. |
| 4 | Impide o compromete seriamente el aprendizaje. |

## Origen del problema

| Categoría | Descripción |
|---|---|
| Interfaz | Diseño visual, navegación o controles. |
| IA | Comportamiento o respuestas de la inteligencia artificial. |
| IA + Interfaz | Combinación de problemas relacionados con la IA y la interfaz. |

# 3. Matriz consolidada del grupo

| ID | Problema consolidado | N.º de evaluadores (1–4) | Heurística | Severidad | Impacto | Origen | Recomendación preliminar |
|---|---|---:|---|---:|---:|---|---|
| C1 | El estado de procesamiento es poco informativo: no indica etapa, tiempo aproximado ni diferencia claramente entre una espera normal y una posible interrupción. | 3 | 1. Visibilidad del estado del sistema | 3 | 3 | IA + Interfaz | Mostrar etapas como “analizando”, “consultando fuentes” y “redactando”, un tiempo estimado y un botón visible para cancelar o reintentar. |
| C2 | Algunas etiquetas funcionan como nombres comerciales y no explican con claridad la acción educativa que realizará el sistema. | 2 | 2. Correspondencia entre el sistema y el mundo real | 2 | 2 | Interfaz | Usar etiquetas orientadas a tareas, por ejemplo: “Explícame paso a paso”, “Practicar este tema” o “Revisar mi respuesta”. |
| C3 | Después de enviar una consulta o cargar material no siempre se destaca una opción inmediata para editar, deshacer o cancelar la acción. | 4 | 3. Control y libertad del usuario | 3 | 3 | Interfaz | Incluir “Editar pregunta”, “Cancelar generación”, “Reemplazar archivo” y “Deshacer” cerca del contenido enviado. |
| C4 | La misma ayuda basada en IA se presenta con nombres y llamados a la acción diferentes en distintas partes del sitio. | 2 | 4. Consistencia y estándares | 2 | 2 | Interfaz | Definir un nombre principal para el tutor y mantener etiquetas, íconos y acciones consistentes en todas las pantallas. |
| C5 | La prevención de entradas deficientes es limitada antes de procesar preguntas vagas, fotografías poco legibles o archivos inadecuados. | 2 | 5. Prevención de errores | 3 | 3 | IA + Interfaz | Validar legibilidad y formato antes del envío, mostrar ejemplos de una buena pregunta y advertir cuando falte información clave. |
| C6 | Al pasar entre modos, el contexto relevante no siempre permanece suficientemente visible, por lo que el estudiante debe recordar o volver a introducir información. | 2 | 6. Reconocimiento antes que recuerdo | 3 | 3 | IA + Interfaz | Mantener fija la pregunta, el material adjunto, el nivel y las instrucciones previas; permitir seleccionar contexto reciente con un clic. |
| C7 | Las opciones de personalización y los aceleradores para usuarios frecuentes son limitados o aparecen después de generar la respuesta. | 2 | 7. Flexibilidad y eficiencia de uso | 2 | 2 | Interfaz | Agregar controles rápidos para nivel, extensión, idioma, pista, solución completa, ejemplo y tipo de explicación; además, recordar las preferencias. |
| C8 | La pantalla puede concentrar demasiados elementos simultáneos, reduciendo la jerarquía visual del contenido educativo principal. | 4 | 8. Diseño estético y minimalista | 3 | 3 | Interfaz | Priorizar la explicación activa, agrupar contenido secundario en secciones plegables y reducir interrupciones promocionales durante el estudio. |
| C9 | Los mensajes de error pueden no explicar con suficiente precisión la causa ni ofrecer una ruta de recuperación adaptada al problema. | 2 | 9. Ayudar a reconocer, diagnosticar y recuperarse de errores | 3 | 3 | IA + Interfaz | Indicar la causa probable, conservar el texto y los archivos y ofrecer acciones concretas: reintentar, reducir el archivo, cambiar el formato o continuar sin adjunto. |
| C10 | La orientación para nuevos usuarios no está suficientemente integrada en el momento exacto en que se necesita. | 2 | 10. Ayuda y documentación | 2 | 2 | Interfaz | Añadir una guía inicial corta, ejemplos de consultas y ayuda contextual accesible desde cada control sin abandonar la sesión. |

# 4. Análisis de resultados

Los hallazgos más repetidos fueron la falta de control inmediato después de enviar una consulta y la sobrecarga visual de la página de resultados, identificados por los cuatro evaluadores.

Ambos problemas alcanzaron una severidad de 3 porque pueden interrumpir el flujo de estudio y dificultar que el usuario concentre su atención en la explicación.

También se observaron problemas importantes en la visibilidad del procesamiento, la prevención de entradas deficientes, la conservación del contexto y la recuperación ante fallos.

En cambio, las inconsistencias terminológicas, las opciones de personalización y la ayuda contextual fueron valoradas como problemas menores, aunque su mejora aumentaría la facilidad de aprendizaje y la confianza del estudiante.

# 5. Conclusión

Brainly AI ofrece una propuesta educativa útil al combinar respuestas comunitarias, contenido verificado y asistencia generativa.

Sin embargo, la evaluación muestra que su experiencia puede mejorar si concentra la interfaz en la tarea académica, mantiene nombres y controles consistentes, informa claramente el estado de la IA y permite corregir o cancelar acciones sin reiniciar el proceso.

Asimismo, validar mejor las preguntas y archivos, conservar el contexto y ofrecer ayuda dentro del flujo reduciría errores y carga mental.

En conjunto, los problemas encontrados no impiden completamente el uso de la plataforma, pero varios afectan de forma significativa la continuidad y la calidad del aprendizaje, por lo que deberían priorizarse las recomendaciones con severidad 3.

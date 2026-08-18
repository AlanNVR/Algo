# Cómo compilar este informe en Overleaf

## 1. Subir el proyecto

1. Entrar en <https://www.overleaf.com> → **New Project** → **Upload Project**.
2. Arrastrar este archivo `.zip` completo. **No lo descompriman antes**: Overleaf lo hace solo y
   conserva la estructura.
3. Al terminar la subida deben verse 18 archivos en el panel izquierdo.

## 2. Configurar el compilador (importante)

Abrir el **Menú** (esquina superior izquierda) y comprobar dos ajustes:

| Ajuste | Valor correcto | Qué pasa si está mal |
|---|---|---|
| **Compiler** | `pdfLaTeX` | Con XeLaTeX o LuaLaTeX pueden fallar las fuentes T1 |
| **Main document** | `PE5_U5_PFC_Final_MORA_RIZZO_VILLAFUERTE.tex` | Overleaf intentaría compilar un archivo de sección suelto |

La bibliografía usa **BibTeX**, no Biber. Overleaf lo detecta solo por el comando `\bibliography{}`;
no hay que cambiar nada.

## 3. Compilar

Pulsar **Recompile** **tres veces seguidas**. Es obligatorio y no es un capricho del documento:

- La **primera** pasada genera el `.aux` y deja el índice y las referencias sin resolver.
- Overleaf ejecuta BibTeX automáticamente entre pasadas.
- La **segunda** resuelve las citas.
- La **tercera** fija el índice general, el de tablas, el de figuras y las referencias cruzadas.

Con menos de tres pasadas aparecerán marcas `??` en el PDF y el índice mostrará números de página
equivocados.

**Resultado esperado:** 55 páginas, sin errores y sin advertencias de referencias sin resolver.
De esas 55, **41 son de contenido** (páginas 5 a 45), por encima del mínimo de 40 que exige la guía.

## 4. Archivos del proyecto

| Archivo | Contenido |
|---|---|
| `PE5_U5_PFC_Final_MORA_RIZZO_VILLAFUERTE.tex` | **Archivo principal.** Preámbulo, carátula, resumen bilingüe, índices y llamadas a las secciones |
| `sec1_introduccion.tex` | §1 Introducción |
| `sec2_metodologia.tex` | §2 Metodología y fundamento teórico |
| `sec3_ers.tex` | §3 ERS final |
| `sec4_uml.tex` | §4 Modelos UML y de procesos |
| `sec5_validacion.tex` | §5 Validación |
| `sec6_gestion.tex` | §6 Gestión y trazabilidad |
| `sec7_ia.tex` | §7 Requisitos de los componentes de IA |
| `sec8_metricas.tex` | §8 Métricas de calidad |
| `sec9_retrospectiva.tex` | §9 Retrospectiva |
| `sec10_conclusiones.tex` | §10 Conclusiones |
| `anexos.tex` | Anexos A a E, incluido el banco de 22 preguntas del tribunal |
| `tabla_rf.tex` | Filas del catálogo de 42 requisitos funcionales |
| `tabla_rnf.tex` | Filas de los 19 requisitos no funcionales |
| `tabla_defectos.tex` | Filas de los 33 defectos de la inspección |
| `tabla_e2e.tex` | Las 73 filas de la matriz de trazabilidad |
| `referencias.bib` | 51 entradas bibliográficas en formato BibTeX |

Los cuatro archivos `tabla_*.tex` **no son secciones**: contienen únicamente filas de tabla y no
compilan por separado. Se cargan desde dentro de un entorno `longtable` de la sección
correspondiente.

## 5. Qué falta rellenar antes de entregar

El documento tiene **19 marcadores rojos** con la forma `[PENDIENTE: ...]`. Son datos que solo tiene
el equipo. Para localizarlos, usar la búsqueda de Overleaf (`Ctrl+F` en el editor) con el texto
`\pendiente`.

| Archivo | Marcadores | Qué falta |
|---|---|---|
| Archivo principal | 1 | Fecha de entrega, en la carátula |
| `sec9_retrospectiva.tex` | 11 | Responsable de cada elemento Start-Stop-Continue |
| `anexos.tex` | 7 | Aporte individual, número de commits por integrante y versión del asistente de IA |

**Comprobación final antes de entregar:** buscar `PENDIENTE` en el PDF compilado. Debe devolver cero
resultados. Un solo marcador rojo visible activa el indicador S2 de la escala de integridad
académica, que descuenta el 50 % de la nota.

## 6. Si algo falla

| Síntoma | Causa probable | Solución |
|---|---|---|
| Aparecen `??` en lugar de números de sección | Menos de tres pasadas | Pulsar Recompile hasta tres veces |
| Las referencias salen como `[?]` | BibTeX no llegó a ejecutarse | Menú → **Clear cached files**, y recompilar tres veces |
| Error `File not found: sec1_introduccion.tex` | El zip se descomprimió antes de subirlo y se perdió la estructura | Volver a subir el `.zip` sin descomprimir |
| Las tildes salen mal | El archivo se guardó en otra codificación | Los archivos están en UTF-8; no cambiar la codificación al editar |
| Compila pero sin partición silábica en español | Overleaf sin el paquete de idioma | No ocurre en Overleaf, que lo incluye. El documento carga `babel` de forma condicional, así que compila igual |

## 7. Al terminar

Descargar el PDF desde Overleaf y **subirlo también al repositorio**, en `05_Informe/`, junto a estos
mismos archivos fuente. El criterio G2 exige que el PDF entregado se regenere clonando el
repositorio: si las fuentes están solo en Overleaf y no en Git, ese criterio no se cumple.

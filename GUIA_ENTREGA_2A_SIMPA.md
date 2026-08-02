# Guía de ejecución — Entrega 3 (2A) · ERS SIMPA

**Equipo AHMRV · ISR-401 · UTEQ · 2026–2027 PPA**
Documento de trabajo interno. Fecha de corte prorrogada: **lunes 03/08/2026, 23:59**.

---

## Cómo usar esta guía

Las fases están ordenadas **por retorno sobre el tiempo invertido**, no por el orden del documento. La razón es aritmética:

> Los gatekeepers son **topes multiplicativos**, no puntos que se suman. Un gatekeeper incumplido convierte un trabajo de 9,2 en un 2,50. Ninguna cantidad de redacción compensa eso.

Por lo tanto: **la Fase 0 vale más que las Fases 5 a 9 juntas.** No se avanza a la siguiente fase hasta cerrar la anterior.

Cada tarea lleva: `[responsable] (tiempo estimado)`.

---

## Estado de partida — auditoría del repositorio (02/08/2026)

### Lo que ya está bien

| Elemento | Estado |
|---|---|
| Commits distribuidos entre los 6 integrantes | ✅ 105+ commits; todos superan el mínimo |
| Git LFS operativo | ✅ Punteros resuelven; `.7z` = 1,77 GB, audio = 38 MB |
| Videos de entrevistas | ✅ ~10 archivos dentro del contenedor cifrado |
| Mockups | ✅ 8 pantallas en `03_Modelado/mockups/` |
| Diagramas draw.io | ✅ contexto, casos de uso, clases |
| ERS 1B | ✅ 20 RF, 9 RNF, 7 RD, 5 CU, 24 filas de matriz |
| Encuesta piloto | ✅ 4 respondientes, PDF exportado |

### Lo que hoy pone techo de 2,50/10

| # | Hallazgo | Gatekeeper |
|---|---|---|
| 1 | El ERS público contiene consentimientos con **cédula y firma visibles** (Fig. 12–14) y **rostros identificables** (Fig. 15–17) | **G8** |
| 2 | `02_Evidencias/formularios/` tiene los 3 consentimientos en JPEG sin enmascarar | **G8** |
| 3 | `08_Etica/` contiene solo un `readme.md` de 1 byte — sin aval institucional | **G3 + G8** |
| 4 | `fichas_tecnicas.csv` tiene un **conflicto de merge sin resolver** y solo contiene la plantilla de ejemplo | **G4** |
| 5 | `checksums.sha256` lista 13 archivos de video que no son verificables sin la ficha técnica correspondiente | **G4** |

### Lo que pone techo de 4,00/10

| # | Hallazgo | Gatekeeper |
|---|---|---|
| 6 | El ERS está en Word; no existe `.tex` ni `referencias.bib` en `01_ERS/` | **G2** |
| 7 | Mínimos incumplidos: 20/25 RF, 9/15 RNF, 5/10 CU, 24/40 filas | **G5** |

### Penalizaciones directas en rúbrica

- La raíz del repositorio no es el proyecto: contiene `Grupo_C/`, `MRV_Equipo_B/`, `Tareas_Villafuerte/`
- Faltan `LICENSE`, `CITATION.cff`, `CHANGELOG.md`; el `README.md` raíz tiene 7 bytes
- Nomenclatura incorrecta: `23-05-2026 entrevista_ing_Rodolfo_Villafuerte.mpeg` usa **nombre propio** y formato no conforme
- `02_Evidencias/documentos/documento` es un archivo vacío de 1 byte
- Faltan las carpetas `Consentimientos/`, `Fotos_Entorno/`, `Cuestionario/`

---

# FASE 0 — Blindaje (CRÍTICA, hacer primero)

**Objetivo:** eliminar los cinco hallazgos que hoy fuerzan 2,50/10.
**Tiempo total: ~3 h.** No se avanza a la Fase 1 sin terminar esta.

## 0.1 Retirar los datos identificables del ERS público `[Denisses] (45 min)`

El PDF actual en `01_ERS/` debe salir del repositorio hasta que esté corregido.

```bash
git rm --cached AHMRV/01_ERS/ERS_SIMPA_v2.0_A.pdf
git commit -m "fix(etica): retiro temporal del ERS con datos identificables (LOPDP)"
git push
```

Sobre la copia local, para cada figura de consentimiento (12, 13, 14):

- Colocar un **recuadro opaco** (no difuminado, no transparencia) sobre: nombre completo, número de cédula, firma
- **Dejar legibles**: el cargo, la fecha manuscrita y el código de participante
- Sustituir el nombre en el pie de figura por el código: *"Figura 12: Consentimiento informado — Participante ENTR-01 (Administrador General)"*

Sobre las figuras 15, 16, 17 (fotos de sesión): difuminar rostros o recortar el encuadre.

> **Criterio de aceptación:** abrir el PDF y buscar con Ctrl+F cualquier nombre propio de stakeholder. Cero resultados fuera de la zona restringida.

## 0.2 Enmascarar los consentimientos del repositorio `[Edson] (30 min)`

```bash
mkdir -p AHMRV/02_Evidencias/Consentimientos
```

Para cada uno de los tres JPEG en `formularios/`:

1. Abrir en GIMP o cualquier editor
2. Rectángulo negro sólido sobre cédula y firma
3. Exportar a ≥200 dpi con el nombre de código:
   - `2026-05-23_Administrador_ENTR-01_Consentimiento.jpg`
   - `2026-05-23_AsesorTecnico_ENTR-02_Consentimiento.jpg`
   - `2026-05-23_JefePolinizacion_ENTR-03_Consentimiento.jpg`
4. Guardar en `Consentimientos/`
5. **Los originales íntegros van al contenedor cifrado**, nunca al repositorio público

```bash
git rm AHMRV/02_Evidencias/formularios/*.jpeg
```

## 0.3 Limpiar metadatos GPS y rostros de las fotos `[Francisco] (30 min)`

```bash
sudo apt install libimage-exiftool-perl   # si no está
cd AHMRV/02_Evidencias
mkdir -p Fotos_Entorno
cp fotos/*.jpeg fotos/*.jpg Fotos_Entorno/ 2>/dev/null

# eliminar TODA la información GPS de forma irreversible
exiftool -gps:all= -overwrite_original Fotos_Entorno/

# verificar que no queda nada
exiftool -gps:all Fotos_Entorno/ | grep -i gps
# salida esperada: vacía
```

Renombrar según `YYYY-MM-DD_descripcion.jpg`:

```
2026-05-23_sesion_entrevista_ENTR-01.jpg
2026-06-27_deteccion_plaga_lote3.jpg
2026-06-27_bomba_sistema_riego.jpg
2026-06-27_vista_general_cultivo.jpg
...
```

Difuminar rostros en las tres fotos de sesión. **Regla:** ninguna foto publicada conserva coordenadas GPS ni rostros identificables.

## 0.4 Cargar el paquete ético completo `[Allan] (45 min)`

Esta es la tarea más rentable de todas: el paquete ya existe, solo hay que subirlo.

```bash
cd AHMRV/08_Etica
# copiar los 12 documentos del Anexo A + los 4 de Categoría C
```

Estructura esperada:

```
08_Etica/
├── A01_Protocolo_Investigacion.pdf
├── A02_Instrumentos_Recoleccion.pdf
├── A03_...  (hasta A13)
├── Categoria_C/
│   ├── C1_Aval_Institucional.pdf        ← CRÍTICO para G3
│   ├── C2_...
│   ├── C3_...
│   └── C4_...
├── Adenda_Segunda_Ronda.pdf             ← se genera en Fase 2
└── README_Etica.md
```

> **El aval institucional (C.1) es el que cierra G3.** Sin él, 2,50/10 aunque todo lo demás esté perfecto.

## 0.5 Reparar `fichas_tecnicas.csv` `[Edson] (45 min)`

Primero, eliminar el conflicto de merge. Luego generar el inventario real. Descifrar el `.7z` localmente y ejecutar:

```bash
# Encabezado
echo "id_archivo;tipo;fecha;codigo_participante;duracion_segundos;codec;tamano_bytes;sha256;contenedor" > fichas_tecnicas.csv

# Por cada archivo multimedia dentro del contenedor
for f in videos/**/*.mp4 videos/**/*.MOV audios/*.mp3; do
  dur=$(ffprobe -v error -show_entries format=duration -of csv=p=0 "$f")
  cod=$(ffprobe -v error -select_streams v:0 -show_entries stream=codec_name -of csv=p=0 "$f")
  siz=$(stat -c%s "$f")
  sha=$(sha256sum "$f" | cut -d' ' -f1)
  echo "$(basename $f);video;2026-07-28;ENTR-06;$dur;$cod;$siz;$sha;evidencias_restringidas_2A.7z" >> fichas_tecnicas.csv
done
```

> **Prueba de fuego:** cada línea de `fichas_tecnicas.csv` debe tener un hash que coincida con `checksums.sha256`, y el archivo debe existir dentro del `.7z`. Un archivo listado que no aparezca ⇒ G4.

## 0.6 Verificar que ningún archivo multimedia es un falso `[Edson] (15 min)`

```bash
# ffprobe debe pasar sin error y mostrar duración > 0 en TODOS
for f in $(find . -name "*.mp4" -o -name "*.MOV" -o -name "*.mp3" -o -name "*.mpeg"); do
  d=$(ffprobe -v error -show_entries format=duration -of csv=p=0 "$f" 2>/dev/null)
  echo "$f -> ${d:-FALLO}"
done
```

Cualquier salida que diga `FALLO`, o cualquier archivo de 2 o 54 bytes que en realidad sea texto ASCII, es **evidencia falsificada** ⇒ G4 con nota mínima 2,50/10. Borrarlo o reemplazarlo por el archivo real.

## ✅ Checkpoint Fase 0

- [ ] Ningún nombre, cédula o firma legible en zona pública
- [ ] Ninguna foto con GPS o rostro identificable
- [ ] `08_Etica/` con paquete completo y aval C.1
- [ ] `fichas_tecnicas.csv` sin conflicto de merge y con datos reales
- [ ] `ffprobe` pasa en el 100 % de los multimedia

---

# FASE 1 — Reestructuración del repositorio

**Tiempo: ~1 h.** `[Francisco + Anderson]`

La §8.1 exige que la raíz **sea** el árbol del proyecto. Hoy el proyecto está un nivel abajo y comparte raíz con tareas de otras materias.

## 1.1 Mover el proyecto a la raíz

```bash
git mv AHMRV/* .
git rmdir AHMRV
# Archivar lo que no pertenece al PFC (NO borrar el historial)
git rm -r Grupo_C MRV_Equipo_B Tareas_Villafuerte
git commit -m "refactor(repo): estructura conforme a la Seccion 8.1 de la guia 2A"
```

> El historial de commits se conserva íntegro tras `git mv` y `git rm`. C9 no se ve afectado.

## 1.2 Crear el árbol completo

```bash
mkdir -p 01_ERS 02_Evidencias/{00_Restringido,Consentimientos,Transcripciones,Fotos_Entorno,Cuestionario/{Fotos_Aplicacion,Respuestas},Documentos_Organizacion,Validacion_Walkthrough,Codificacion_Tematica}
mkdir -p 03_Modelado/{Diagramas_UML,Mockups} 04_Trazabilidad 05_MVP
mkdir -p 06_Experimento/{instrumentos,prompts_llm,resultados,scripts_analisis}
mkdir -p 07_Publicacion/dataset_zenodo 08_Etica/Categoria_C
```

Eliminar `02_Evidencias/documentos/documento` (1 byte) y las carpetas viejas `fotos/`, `formularios/`, `audio/`, `encuestas/`, `documentos/` una vez migrado su contenido.

## 1.3 Renombrar el repositorio (opcional pero recomendado)

En GitHub → Settings → `SIMPA_ISR401`. GitHub mantiene la redirección y el historial. **Actualizar el enlace en la portada del ERS.**

## 1.4 Crear los cinco archivos raíz

| Archivo | Contenido mínimo |
|---|---|
| `README.md` | Nombre del sistema, 6 integrantes con rol, resumen del dominio, enlace al ERS PDF, enlace al MVP, enlace OSF, instrucciones para reproducir el análisis, tabla de contenidos, **instrucción de `git lfs pull`** |
| `LICENSE` | MIT para el MVP + CC BY 4.0 para documento y dataset. Declarar expresamente que `02_Evidencias/00_Restringido/` **no se licencia ni se redistribuye** |
| `CITATION.cff` | YAML v1.2.0 con `cff-version`, `message`, `authors` (ORCID de cada integrante), `title`, `version`, `date-released` |
| `CHANGELOG.md` | Versiones desde la 1A, formato Keep a Changelog |
| `checksums.sha256` | Regenerar tras la reestructuración: `find . -type f \( -name "*.mp4" -o -name "*.mp3" -o -name "*.jpg" \) -exec sha256sum {} \; > checksums.sha256` |

> **Importante para el README:** el docente debe saber que hay LFS. Incluir literalmente:
> ```
> git clone https://github.com/AlanNVR/SIMPA_ISR401.git
> cd SIMPA_ISR401
> git lfs pull        # OBLIGATORIO: descarga videos y contenedor cifrado (1,8 GB)
> ```
> Sin esta línea, el docente ve punteros de 133 bytes y concluye que la evidencia es falsa.

## ✅ Checkpoint Fase 1

- [ ] La raíz coincide **exactamente** con el árbol de la §8.1
- [ ] Los 5 archivos raíz existen y están completos
- [ ] `README.md` explica `git lfs pull`

---

# FASE 2 — Documentación ética y adenda

**Tiempo: ~1 h.** `[Allan]`

## 2.1 Resolver el conflicto de numeración de evidencias

La numeración nueva choca con la del ERS 1B. **Decisión: conservar EV-01…EV-05 tal como están y numerar la segunda ronda desde EV-06.**

| ID | Participante | Rol | Organización | Ronda |
|---|---|---|---|---|
| EV-01 | ENTR-01 | Administrador General | Palmicultora M | 1ª |
| EV-02 | ENTR-02 | Asesor Técnico | Palmicultora M | 1ª |
| EV-03 | ENTR-03 | Jefe de Polinización | Palmicultora M | 1ª |
| EV-04 | — | Observación de campo | Palmicultora M | 1ª |
| EV-05 | — | Cuestionario piloto (n=4) | Palmicultora M | 1ª |
| **EV-06** | ENTR-04 | **Técnico agrícola de extractora** | **Extractora E** | 2ª |
| **EV-07** | ENTR-05 | Trabajador agrícola (chapia) | Palmicultora M | 2ª |
| **EV-08** | ENTR-06 | Trabajador agrícola (multilabor) | Palmicultora M | 2ª |
| **EV-09** | ENTR-07 | *(por confirmar cargo)* | *(por confirmar)* | 2ª |
| **EV-10** | ENTR-08 | Asistente de administración | Palmicultora M | 2ª |
| **EV-11** | — | Documentos organizacionales | Palmicultora M / J | 2ª |
| **EV-12** | — | Cuestionario ampliado | Multi-perfil | 2ª |

El `CHANGELOG.md` documenta la continuidad. No se rompe ninguna de las 24 filas heredadas.

## 2.2 Redactar la adenda de segunda ronda

`08_Etica/Adenda_Segunda_Ronda.pdf` debe declarar:

1. **Nuevos participantes previstos por rol** (no por nombre): técnico de extractora, 3 trabajadores agrícolas, asistente de administración
2. **Instrumentos actualizados**: guion v2.0 y cuestionario v2.0
3. **Enfoque empírico elegido** (Fase 3)
4. **Cláusula de uso de datos anonimizados** en publicaciones revisadas por pares y depósito en Zenodo con CC BY 4.0
5. **Declaración de conflicto de interés** para EV-10 (Bryan Villafuerte, parentesco de segundo grado con el analista líder) con las seis medidas de mitigación ya documentadas en la 1B
6. **Incorporación de Extractora E** como segunda organización fuente

### ⚠️ Punto delicado sobre la fecha

La guía exige que **la adenda tenga fecha anterior al primer consentimiento nuevo**. Las entrevistas EV-06 a EV-10 se realizaron el 28/07/2026.

**No antedatar el documento.** Es fabricación documental y, si se detecta, cuesta más que el gatekeeper. La ruta correcta:

> Redactar la adenda con la fecha real, e incluir un párrafo de **declaración de desviación de procedimiento**: reconocer que la carga formal fue posterior a la ejecución de campo, explicar que los consentimientos individuales sí se firmaron antes de cada grabación, y solicitar al docente la convalidación prevista en la §4.2 de la guía.

Una desviación declarada se evalúa; una desviación oculta se sanciona.

## 2.3 Consentimientos de la segunda ronda

Necesitan **8 participantes distintos**. Tienen 5 nuevos (EV-06 a EV-10). Faltan 3.

Opciones realistas para completar hoy:
- Otros trabajadores de La Manuela (hay 30 jornales semanales de polinización según los documentos)
- Personal de Hacienda José Antonio
- Personal de la extractora

Cada uno firma el consentimiento LOPDP con **cláusula explícita de publicación anonimizada en Zenodo**. Sin esa cláusula, la respuesta se excluye del dataset.

## ✅ Checkpoint Fase 2

- [ ] Numeración EV consolidada y documentada en el CHANGELOG
- [ ] Adenda con fecha real y declaración de desviación
- [ ] Conflicto de interés de EV-10 declarado
- [ ] ≥8 consentimientos de segunda ronda (o el número real, declarado como limitación)

---

# FASE 3 — Protocolo experimental y registro OSF

**Tiempo: ~1,5 h.** `[Allan + Josthyn]`
**Hacer temprano: la fecha del registro debe ser anterior a la ejecución.**

## 3.1 Enfoque elegido: Enfoque 1

*Comparar la calidad de los RF elicitados por el equipo humano con los generados por un LLM a partir del mismo material fuente.*

**Por qué este y no otro:**

| Enfoque | Viabilidad hoy |
|---|---|
| 1 — Humano vs LLM | ✅ El material fuente ya existe (transcripción EV-06); el conjunto humano ya existe (el ERS) |
| 2 — Detector de ambigüedad | 🟡 Requiere escribir y calibrar el detector |
| 3 — Explicabilidad | ❌ Exige dos rondas de validación con 6 participantes cada una |

## 3.2 Contenido de `06_Experimento/protocolo.pdf`

**Pregunta de investigación en formato PICOC:**

- **P (Población):** requisitos funcionales de un sistema agroindustrial real de gestión de palma africana
- **I (Intervención):** generación de RF mediante un LLM a partir de transcripción de entrevista anonimizada
- **C (Comparación):** RF elicitados por el equipo humano a partir del mismo material
- **O (Resultado):** puntuación en cinco dimensiones de calidad (completitud, ausencia de ambigüedad, verificabilidad, corrección respecto de la fuente, consistencia interna)
- **C (Contexto):** proyecto académico de Ingeniería de Requerimientos en Ecuador

**RQ1:** ¿En qué dimensiones de calidad difieren los RF elicitados por un equipo humano de los generados por un LLM a partir del mismo material fuente?

**Hipótesis:**
- H₀: no hay diferencia en la puntuación media entre ambos conjuntos
- H₁: existe diferencia estadísticamente significativa

**Variables:**
- Independiente: origen del requisito (humano / LLM)
- Dependientes: las cinco dimensiones de calidad (escala 1–5)
- Control: material fuente único, misma rúbrica, evaluación a ciegas

**Plan de análisis:**
1. Shapiro-Wilk para normalidad
2. Prueba *t* pareada si normal; Wilcoxon si no
3. Tamaño del efecto: Cohen *d* o Cliff *δ*
4. Acuerdo inter-evaluador: κ de Cohen por pares, κ de Fleiss para el conjunto
5. α = 0,05; potencia 1−β = 0,80

## 3.3 Ejecución del experimento

1. **Material fuente:** transcripción completa de EV-06 (técnico de extractora), anonimizada
2. **Consigna exacta al LLM** (registrar literalmente):
   > *"A partir del siguiente material fuente, redacta requisitos funcionales del sistema descrito, con los ocho atributos de la plantilla del sílabo."*
3. **Registrar en `prompts_llm/`:** modelo exacto, temperatura, top-p, top-k, semilla, fecha y hora
4. **Conjunto A** (LLM) y **Conjunto B** (humano, del ERS), ambos ≥25 requisitos, mezclados y sin etiqueta
5. **3 evaluadores independientes** (estudiantes de otro paralelo) puntúan a ciegas
6. Cálculos con script en `scripts_analisis/`

> **Si no consiguen los 3 evaluadores esta noche:** se entrega el protocolo registrado en OSF sin resultados. Los resultados corresponden formalmente a la Entrega 4. Inventar cifras dispara G4 y anula C9.

## 3.4 Registro en OSF

1. Crear proyecto en https://osf.io
2. Subir `protocolo.pdf`
3. Crear un **Registration** (no basta el proyecto: la URL persistente con timestamp es lo que exige G6)
4. Descargar comprobante como `06_Experimento/osf_registration.pdf`

## ✅ Checkpoint Fase 3

- [ ] `protocolo.pdf` completo con PICOC, hipótesis, variables y plan estadístico
- [ ] Registro OSF con URL persistente y timestamp
- [ ] `prompts_llm/` con parámetros completos si se ejecutó

---

# FASE 4 — Evidencias de la segunda ronda

**Tiempo: ~3 h (en paralelo con la Fase 5).** `[Anderson + Denisses + Edson]`

## 4.1 Transcripciones anonimizadas — cobertura 100 %

`02_Evidencias/Transcripciones/`, formato TXT o JSON. Reglas:

- Sin nombres propios: sustituir por código de participante
- Sin cargos que identifiquen de forma unívoca
- Incluir el identificador `EV-XX` en cabecera
- Un archivo por entrevista declarada

Ya tienen transcritas EV-06, EV-07 y EV-08 (documento `Entrevistas.md`). **Pendiente:** anonimizarlas — actualmente contienen "Galo Zambrano", "Marcos Masia", "Ángel Zambrano" y "Johnny Mawyin".

> Nota sobre EV-08 (Marcos Masia): la transcripción advierte que puede ser el mismo audio que otra entrevista. **Verificar contra el video antes de declararla como entrevista independiente.** Si es duplicado, declararlo así; una entrevista declarada sin audio propio dispara G4.

## 4.2 Documentos de la organización — falta un tipo

Tienen dos documentos, pero son **del mismo tipo** (plan semanal de presupuesto). La guía exige ≥3 documentos **de tipos distintos**.

| Documento | Tipo | Estado |
|---|---|---|
| `HACIENDA_LA_MANUELA.docx` (sem. 27–30) | Plan semanal de labores | ✅ |
| `HACIENDA_JOSE_ANTONIO.docx` (sem. 27–30) | Plan semanal de labores | ✅ (mismo tipo) |
| **Falta** | Hoja de conteo del polinizador, boleta de pesaje de la extractora, o cuaderno de registro del trabajador | ❌ |

El cuaderno que menciona EV-08 en su entrevista (*"Lo anoto en el diario... en un cuadernito, diariamente"*) es el candidato más fácil: una foto de una página es suficiente.

**Anonimización obligatoria antes de publicar:** tachar de forma irreversible precios (`DIESEL... $705`), tonelajes (`34.87 TONELADAS`) y cualquier información tributaria. Los originales van al contenedor cifrado.

### ⚠️ Decisión pendiente: Hacienda José Antonio

Si es una **segunda organización**, necesita su propio aval institucional y seudónimo (p. ej. "Palmicultora J"). Si comparte administración con La Manuela, es un **segundo sitio del mismo cliente** y se cubre con el aval existente. **Confirmar antes de escribir la sección 2 del ERS.**

## 4.3 Cuestionario

- **Objetivo:** n ≥ 30 por perfil dominante
- **Realidad:** tienen 4 respondientes
- **Población accesible:** ~30 jornales semanales de polinización en La Manuela + personal de José Antonio + extractora

**Plan honesto:** desplegar el cuestionario v2.0 en Google Forms hoy, recoger cuanto se pueda, y documentar en `protocolo.pdf` un **censo justificado de la población accesible** con el cálculo de potencia explícito. Declararlo en el ERS como limitación y en el manuscrito como amenaza a la validez externa.

No olvidar: **≥5 fotografías de la aplicación real** del cuestionario, con rostros fuera de encuadre o difuminados → `Cuestionario/Fotos_Aplicacion/`.

## 4.4 Ronda de validación (walkthrough)

3 sesiones con acta firmada: 2 con usuarios técnicos + 1 con usuarios no técnicos.

**Formato mínimo del acta** (`Validacion_Walkthrough/`, PDF con firma enmascarada):
- Fecha, lugar, duración
- Lista de participantes **por código**
- Requisitos revisados (IDs)
- Decisiones tomadas y cambios acordados
- Firma enmascarada

Si solo alcanzan una o dos sesiones, se declaran las que hubo. La grabación va al contenedor restringido.

## 4.5 Codificación temática y curva de saturación

`Codificacion_Tematica/codificacion.csv` con columnas exactas:

```
Fragmento;Codigo;Categoria;Requisito_derivado;ID_evidencia;Analista_codificador
```

Cobertura del 100 % de las transcripciones.

**Curva de saturación:** eje X = número de entrevista acumulada (1…10), eje Y = códigos nuevos aportados por esa entrevista. Esperable: EV-01 aporta muchos, EV-06 (extractora) genera un repunte por ser un dominio nuevo, EV-07/EV-08 aportan pocos. Ese repunte **es un hallazgo reportable**, no un defecto: demuestra que el muestreo no había alcanzado saturación en la primera ronda.

## ✅ Checkpoint Fase 4

- [ ] Transcripciones anonimizadas al 100 %
- [ ] ≥3 documentos de organización de tipos distintos, anonimizados
- [ ] Cuestionario desplegado + ≥5 fotos de aplicación
- [ ] Actas de walkthrough (las que se logren, declaradas)
- [ ] Codificación temática + figura de curva de saturación

---

# FASE 5 — Documento ERS/SRS en LaTeX

**Tiempo: ~8 h.** `[Denisses + Allan]`
**G2: el ERS debe ser un PDF único reproducible desde `.tex`. Word ⇒ techo 4,00/10.**

## 5.1 Migración a LaTeX

Base recomendada: el preámbulo del `Matriz_de_trazabilidad.tex` del Taller GA, que ya está depurado (sin dependencia de `babel-spanish`, `longtable` con anchos fijos, `\sloppy` global). Estructura:

```
01_ERS/
├── ERS_SRS_2A_v1.0.tex
├── ERS_SRS_2A_v1.0.pdf
├── referencias.bib
└── img/            (figuras vectoriales)
```

## 5.2 Sección 1 — Introducción

**Cambio principal: de 7 a ≥25 referencias primarias**, al menos 10 de los últimos tres años, indexadas en Scopus o Web of Science.

Las 7 actuales son normas y libros de texto. Faltan **artículos revisados por pares**. Fuentes obligatorias que ya vienen dadas por la guía y cuentan para el mínimo:

- Cheng et al. (2026), *Software: Practice and Experience* — GenAI para RE
- Vogelsang & Fischbach (2024) — LLM para PLN en RE
- Chazette & Schneider (2020), *Requirements Engineering* — explicabilidad como RNF
- Chazette, Brunotte & Speith (2021, 2022)
- Arora, Grundy & Abdelrazek (2024), *CACM*
- Montgomery et al. (2022) — calidad de requisitos
- Ferrari, Spoletini & Gnesi (2016) — ambigüedad en entrevistas
- Molléri, Petersen & Mendes (2020) — checklist de encuestas
- Hennink, Kaiser & Marconi (2017) — saturación
- Runeson & Höst (2009) — estudios de caso
- Wohlin et al. (2012) — experimentación
- Wilkinson et al. (2016) — FAIR
- Nosek et al. (2018) — pre-registro

Añadir 5–8 del dominio agroindustrial (visión por computador aplicada a *Elaeis guineensis*, detección de plagas por imagen, agricultura de precisión) publicados 2023–2026.

> **Verificar cada DOI antes de citarlo.** Las referencias inventadas son fabricación académica.

## 5.3 Sección 2 — Descripción general

**Nuevo en 2A: modelado organizacional i\*** con Diagrama de Dependencia Estratégica (SD) y Diagrama de Razón Estratégica (SR).

Actores i\* para SIMPA, derivados de la evidencia:

| Actor | Depende de | Para |
|---|---|---|
| Administrador | Trabajador | Ejecución de labor conforme al presupuesto semanal |
| Administrador | Sistema SIMPA | Verificación de cumplimiento sin recorrido físico |
| Trabajador | Administrador | Asignación de lote y pago por avance |
| Extractora | Cuadrilla de cosecha | Racimos con desprendimiento suficiente |
| Propietario | Administrador | Rendimiento ≥40 t/ha/año |
| Asesor técnico | Sistema SIMPA | Diagnóstico nutricional a distancia |

El SR profundiza en el actor Administrador: su objetivo *"cultivo en buen estado"* se descompone en tareas (supervisar equipos, revisar sanidad, controlar riego) con *softgoals* (oportunidad del diagnóstico, confiabilidad del conteo).

Actualizar también el mapa de stakeholders con matriz poder/interés incluyendo los nuevos: técnico de extractora, trabajadores agrícolas, asistente de administración.

## 5.4 Sección 3 — Requisitos

### 3.2 · De 20 a ≥25 RF

Los nuevos salen directamente de EV-06 (extractora) y de los documentos organizacionales. Propuesta:

| ID | Requisito | Evidencia | Justificación |
|---|---|---|---|
| RF-21 | Clasificación de madurez del racimo por desprendimiento basal (IA sobre imagen) | EV-06 | *"Con 5 pepas desprendidas ya está listo para el corte"* |
| RF-22 | Alerta preventiva de porcentaje estimado de racimos verdes por lote antes del despacho | EV-06 | Umbral de castigo en 3–5 % |
| RF-23 | Registro de resultado de calidad y acidez por lote entregado a la extractora | EV-06 | Laboratorio con resultado semanal |
| RF-24 | Trazabilidad lote → cuadrilla → racimo rechazado | EV-06 | *"Si es del grupo de cosecha o del cultivo"* |
| RF-25 | Planificación semanal de labores con presupuesto por cumplir y cumplido | EV-11 | Estructura de los documentos organizacionales |
| RF-26 | Arrastre automático de labor incompleta a la semana siguiente | EV-11 | `(CONTINUA)` recurrente en los planes |
| RF-27 | Registro de avance por unidad de labor (coronas, bancos, plantas, jornales) | EV-07, EV-08, EV-11 | Unidades reales de medición |
| RF-28 | Consulta del avance acumulado y estimación de pago quincenal por el propio trabajador | EV-07 | *"Ya sé lo que estoy ganando"* |
| RF-29 | Reporte de incidencia fitosanitaria desde el campo con foto y lote | EV-07, EV-08 | Flujo actual verbal al encargado |
| RF-30 | Solicitud de insumos asociada al plan semanal | EV-11 | Sección *Requerimientos* de los documentos |

**Atributo nuevo obligatorio:** cada RF debe referenciar explícitamente el `EV-XX` que lo respalda.

### 3.3 · De 9 a ≥15 RNF sobre las 9 características de ISO/IEC 25010:2023

Cobertura por característica:

| Característica | RNF actuales | Añadir |
|---|---|---|
| Adecuación funcional | — | Exactitud del clasificador de madurez (métrica y umbral) |
| Eficiencia de desempeño | NFR-01, 02, 08 | ✅ |
| Compatibilidad | NFR-07 (parcial) | Formato de intercambio con la extractora |
| Interacción de usuario | NFR-05 | Accesibilidad para baja alfabetización tecnológica |
| Fiabilidad | NFR-03, 04 | Tolerancia a pérdida de señal GPS |
| Seguridad | NFR-06 | Cifrado en reposo; retención de datos |
| Mantenibilidad | NFR-09 | Reentrenamiento del modelo |
| Portabilidad | NFR-07 | ✅ |
| Flexibilidad | — | Parametrización de umbrales por variedad |

### ⚠️ RNF de explicabilidad — cierra G7

Obligatorio para todo componente de IA/ML. Sin él, **C3 vale la mitad**. Plantilla:

> **RNF-XX · Explicabilidad del diagnóstico por imagen**
> Para cada diagnóstico emitido por el módulo de IA, el sistema debe presentar una explicación en ≤2 segundos, de no más de 60 palabras, en español y sin terminología técnica no definida en el glosario, que incluya: (i) el rasgo visual que sustentó la clasificación, (ii) el nivel de confianza en escala cualitativa, (iii) la acción recomendada.
> **Métrica:** comprensión reportada ≥4/5 en escala Likert por usuarios de perfil no técnico.
> **Verificación:** prueba con ≥6 participantes (3 técnicos + 3 no técnicos).
> **Origen:** EV-01, EV-02, EV-06 — usuarios sin conocimiento especializado necesitan saber *por qué*.

Aplicar el marco de Chazette & Schneider (2020) y Chazette, Brunotte & Speith (2021, 2022). Cubrir los tres componentes de IA: detección de plagas (RF-07), diagnóstico nutricional (RF-08) y clasificación de madurez (RF-21).

### Requisitos legales — trazabilidad LOPDP

Tabla nueva con mapeo Artículo → RF/RNF:

| Artículo LOPDP | Obligación | Requisito |
|---|---|---|
| Art. 7 | Consentimiento | RF de aceptación de tratamiento en el alta de usuario |
| Art. 12 | Derecho de acceso | RF de exportación de datos personales del trabajador |
| Art. 13 | Rectificación | RF de corrección de registro de labor |
| Art. 14 | Eliminación | RF de borrado tras finalizar la relación laboral |
| Art. 37 | Seguridad | RNF de cifrado en reposo y en tránsito |
| Art. 40 | Registro de actividades | RNF de bitácora de acceso |

> **Contexto crítico:** el SIMPA rastrea la ubicación GPS de trabajadores. Eso es tratamiento de datos personales de una población en relación de dependencia laboral. Es el punto más delicado del sistema y **tratarlo bien es diferencial en C4**. Aprovechar el dato de EV-05: el 75 % de los trabajadores no manifestó preocupación por el registro de recorrido — eso es evidencia empírica de consentimiento informado, cítenla.

### Historias de usuario Connextra + INVEST + Gherkin

Para **cada RF de prioridad Must**. Formato:

```
Como <rol>, quiero <funcionalidad>, para <beneficio esperado>.

Criterios INVEST verificados: I ✓ N ✓ V ✓ E ✓ S ✓ T ✓

Escenario (Gherkin):
  Dado que el polinizador tiene una jornada activa en el Lote 3
  Cuando finaliza el recorrido y el GPS ha registrado marcaciones
  Entonces el sistema calcula el total de flores polinizadas sin ingreso manual
  Y muestra el avance acumulado de la quincena
```

## 5.5 Sección 4 — UML completo

Ya tienen CU general y clases conceptual. **Faltan 5 tipos de diagrama.**

| Diagrama | Alcance mínimo | Herramienta |
|---|---|---|
| CU general | Actualizado con los nuevos actores (Extractora) | draw.io |
| **10 CU detallados** | Todos los asociados a RF Must (tienen 5) | texto |
| Clases refinado | **Con atributos Y operaciones** (el actual solo tiene atributos) | draw.io |
| **Secuencia** | Uno por CU Must | PlantUML |
| **Actividad** | Flujos principales | PlantUML |
| **Estados** | Entidades con ciclo no trivial: **Racimo** (verde→maduro→cosechado→despachado→aceptado/castigado), **Alerta**, **Labor** | PlantUML |
| **Componentes** | App móvil, API REST, servicio IA, BD, GPS | PlantUML |
| **Despliegue** | Dispositivo Android, servidor nube, laboratorio extractora | PlantUML |

**Los 5 CU detallados que faltan** (elegir entre los Must nuevos): CU-06 Clasificar madurez de racimo, CU-07 Planificar semana de labores, CU-08 Consultar avance y pago, CU-09 Reportar incidencia desde campo, CU-10 Registrar resultado de calidad de la extractora.

**Entrega por triplicado** de cada diagrama: fuente editable (`.drawio` / `.puml`), PNG ≥300 dpi, SVG cuando la herramienta lo permita.

## 5.6 Sección 5 — Priorización extendida

Los mockups tienen que estar **incrustados en el cuerpo** y como PNG/SVG en el repositorio, cada uno con identificador `MU-01`…`MU-08` y tabla de trazado a los RF que soportan. Los enlaces de Figma **por sí solos ya no valen** en esta entrega.

## 5.7 Sección 6 — Conclusiones

Debe incluir explícitamente las limitaciones declaradas: tamaño muestral del cuestionario, número de sesiones de walkthrough, cobertura del MVP. **Declararlas suma; ocultarlas resta.**

## ✅ Checkpoint Fase 5

- [ ] PDF único generado desde `.tex`, numerado, con historial de versiones y enlace GitHub en portada
- [ ] ≥25 RF con 8 atributos + `EV-XX`
- [ ] ≥15 RNF sobre las 9 características + explicabilidad
- [ ] ≥10 CU detallados
- [ ] 8 tipos de diagrama, por triplicado
- [ ] ≥25 referencias verificadas
- [ ] i\* SD y SR
- [ ] Mapeo LOPDP

---

# FASE 6 — Trazabilidad y priorización

**Tiempo: ~2 h.** `[Josthyn + Francisco]`

## 6.1 `04_Trazabilidad/matriz_trazabilidad.csv`

**Mínimo 40 filas.** Columnas exactas, en este orden:

```
ID;Ley;Articulo;Objetivo;Stakeholder;ID-EV;ID-RF;Tipo;ID-CU;ID-HU;ID-CA;ID-Componente;ID-Mockup
```

Partida: las 24 filas de la 1B + ~16 nuevas de EV-06 a EV-11. Cada fila debe encadenar de extremo a extremo. **Las filas heredadas también necesitan las columnas nuevas** — no basta con añadir 16 filas completas y dejar 24 a medias.

> Nota sobre la matriz del Taller GA: **no es reutilizable como matriz.** Usa la numeración de "Equipo B", que no corresponde con la del ERS. Sí es aprovechable su preámbulo LaTeX y su bloque RFC/CCB como apéndice de gestión de cambios.

## 6.2 `04_Trazabilidad/priorizacion_moscow_kano.csv`

```
ID-RF;MoSCoW;Kano;Valor_negocio_WSJF;Justificacion
```

**Kano** — clasificación sugerida:

| Categoría | Requisitos | Razón |
|---|---|---|
| Básicas | RF-01, RF-02, RF-04 | Su ausencia genera insatisfacción; su presencia no genera entusiasmo |
| De desempeño | RF-19, RF-27, RF-28 | Satisfacción proporcional a la calidad de ejecución |
| De deleite | RF-07, RF-08, RF-21 | El análisis por imagen genera entusiasmo desproporcionado — visible en EV-01, EV-02 y EV-06, y en el 4,75/5 de la encuesta |
| Indiferentes | RF-10 | Solo relevante para variedades específicas |

**WSJF** = (Valor de negocio + Criticidad temporal + Reducción de riesgo) / Tamaño del trabajo. Escala Fibonacci 1-2-3-5-8-13. RF-21 (madurez del racimo) debería salir alto: valor directo en dinero, criticidad temporal por la temporada de cosecha, y reduce el riesgo de castigo del lote.

## ✅ Checkpoint Fase 6

- [ ] ≥40 filas con las 13 columnas completas
- [ ] MoSCoW + Kano + WSJF para todos los RF

---

# FASE 7 — MVP

**Tiempo: variable.** `[Anderson + Francisco]` · **Peso: 0,75 pts**

Exigencia: repositorio Git separado, cobertura ≥60 % de RF Must, `README.md` con despliegue local, video ≤3 min.

**Estrategia realista dado el tiempo:** priorizar amplitud sobre profundidad. Una app que registre labor, muestre lotes, capture foto y liste alertas con datos mock cubre más RF Must que un módulo de IA perfecto.

- Stack sugerido: lo que el equipo ya domine
- `docker compose up` o equivalente
- Marcar explícitamente en el README qué RF Must cubre y cuáles no
- `05_MVP/video_demo.mp4` (≤3 min) y submódulo Git para trazar el commit evaluado

Si no da el tiempo: **declarar el MVP como no alcanzado en las conclusiones del ERS.** Cuesta 0,75 pts. Fingirlo cuesta el gatekeeper.

---

# FASE 8 — Preparación de publicación

**Tiempo: ~2 h.** `[Allan + Denisses]` · **Peso: 0,50 pts**

## 8.1 `07_Publicacion/analisis_revistas.md`

Dos candidatas por editorial (una con APC, una por suscripción o híbrida sin cargo). Documentar para cada una: nombre completo, editorial, indexación JCR y cuartil, factor de impacto, modelo de acceso, tarifa APC en USD, tiempo medio a primera decisión, tasa de aceptación, y justificación del ajuste temático.

Usar las tres herramientas oficiales: `journalsuggester.springer.com`, `journalfinder.elsevier.com`, `publication-recommender.ieee.org`.

## 8.2 Manuscrito v1.0

Solo tres secciones cerradas en esta entrega: **introducción, trabajo relacionado y metodología.** Resultados y discusión son de la Entrega 4 y **no pueden escribirse antes de tener datos**.

**Título propuesto (10–15 palabras):**
> *Calidad de requisitos elicitados por analistas humanos frente a un modelo grande de lenguaje en un sistema agroindustrial de palma africana*

**Resumen:** 200–250 palabras, estructura Contexto / Objetivo / Método / Resultados / Conclusiones.

## 8.3 `dataset_zenodo/`

Transcripciones anonimizadas en JSON estructurado, respuestas del cuestionario en CSV, corpus etiquetado de RF/RNF en JSON, matriz en CSV, prompts y respuestas del LLM, scripts de análisis, y `README_dataset.md` con diccionario de datos.

---

# FASE 9 — Verificación final antes del corte

**Tiempo: ~1 h.** `[Edson, como verificador]`

Recorrer la checklist de la §8.10 de la guía. Marcar solo lo verificado, no lo supuesto.

## Gatekeepers

- [ ] **G1** — Enlace GitHub verificable en **una sola línea** de la portada del PDF subido al SGA
- [ ] **G2** — PDF único, numerado, reproducible desde `.tex` según el README
- [ ] **G3** — Aval institucional en `08_Etica/`; seudónimo usado en todos los artefactos públicos
- [ ] **G4** — Evidencia audiovisual real de la 2ª ronda, con hash coincidente, en la zona correcta
- [ ] **G5** — 25 RF · 15 RNF · 10 CU · 40 filas · mínimos de la §4.2
- [ ] **G6** — Protocolo en OSF con fecha anterior a la ejecución
- [ ] **G7** — Explicabilidad como RNF para los tres componentes de IA
- [ ] **G8** — Paquete ético completo + adenda; **cero datos identificables en zona pública**

## Verificación técnica

```bash
# 1. Ningún multimedia falso
find . \( -name "*.mp4" -o -name "*.mp3" -o -name "*.MOV" \) -size -1k

# 2. Ninguna foto con GPS
exiftool -gps:all Fotos_Entorno/ | grep -i gps

# 3. Checksums coherentes
sha256sum -c checksums.sha256

# 4. El contenedor abre con la contraseña
7z t 02_Evidencias/00_Restringido/evidencias_restringidas_2A.7z

# 5. Filas de la matriz
wc -l 04_Trazabilidad/matriz_trazabilidad.csv   # ≥41 con encabezado

# 6. LFS resuelve desde cero
cd /tmp && git clone <url> test && cd test && git lfs pull && ls -la
```

## Entrega

- Nombre del archivo: `ERS_SIMPA_v3.0_A.pdf`
- Contraseña del contenedor: **por el espacio de la actividad en el SGA**, nunca en el repositorio ni en el README
- Último commit válido antes del corte

---

# Asignación por integrante

| Integrante | Rol | Responsabilidad en 2A |
|---|---|---|
| **Allan Villafuerte** | Analista líder | Fases 0.4, 2, 3, 8 · coordinación · firma electrónica del PDF |
| **Denisses Huilcapi** | Documentadora | Fases 0.1, 5 (redacción LaTeX), 8.2 |
| **Josthyn Macías** | Modelador | Fase 5.5 (los 5 diagramas nuevos), Fase 6 |
| **Francisco Arboleda** | Apoyo modelado | Fases 0.3, 1 (reestructuración), 6, 7 |
| **Edson Rizzo** | Verificador | Fases 0.2, 0.5, 0.6, 4, **9 (verificación final)** |
| **Anderson Alcívar** | Apoyo repositorio | Fases 4, 7 · commits distribuidos |

> **Regla de commits:** cada integrante debe registrar commits propios a lo largo de las horas de trabajo, no un bloque final. C9 evalúa distribución temporal.

---

# Cronograma sugerido (~36 h)

| Franja | Actividad | Quién |
|---|---|---|
| **H+0 a H+3** | **FASE 0 completa** — blindaje | Todos |
| H+3 a H+4 | Fase 1 — reestructuración del repo | Francisco, Anderson |
| H+4 a H+5 | Fase 2 — adenda ética | Allan |
| H+5 a H+6,5 | Fase 3 — protocolo + registro OSF | Allan, Josthyn |
| H+6,5 a H+10 | Fase 4 — evidencias (paralelo) | Anderson, Denisses, Edson |
| H+6,5 a H+18 | Fase 5 — ERS en LaTeX (paralelo) | Denisses, Allan |
| H+10 a H+16 | Fase 5.5 — diagramas UML | Josthyn |
| H+16 a H+18 | Fase 6 — trazabilidad | Josthyn, Francisco |
| H+18 a H+26 | Fase 7 — MVP (si hay margen) | Anderson, Francisco |
| H+26 a H+28 | Fase 8 — publicación | Allan, Denisses |
| H+28 a H+30 | Compilación final del PDF | Denisses |
| **H+30 a H+31** | **FASE 9 — verificación** | Edson |
| H+31 | Subida al SGA + contraseña | Allan |

---

# Decisiones pendientes que bloquean el trabajo

1. **¿Hacienda José Antonio comparte administración con La Manuela?** Determina si es un segundo sitio (aval existente) o una segunda organización (aval propio + seudónimo).
2. **Duraciones reales de los videos del contenedor** (salida de `ffprobe`). Sin esto no se puede llenar la ficha técnica ni saber si llegan a los 120 min exigidos.
3. **Cargo y organización de Darwin Litardo (EV-09).**
4. **¿Se consiguen los 3 evaluadores independientes esta noche?** Determina si el experimento se ejecuta o solo se registra.
5. **¿Marcos Masia (EV-08) es una entrevista independiente o duplicado de audio?** Verificar contra el video antes de declararla.

---

# Tres principios para todo el trabajo

**1. Nada declarado en el ERS puede quedar solo declarado.**
Toda técnica de elicitación mencionada requiere su evidencia; toda evidencia debe reposar dentro del repositorio; todo archivo debe pasar la verificación técnica de su tipo.

**2. Una limitación declarada se evalúa; una limitación oculta se sanciona.**
El cuestionario con n=12 declarado honestamente en amenazas a la validez cuesta décimas. Un n=30 inventado dispara G4 y cuesta 7,5 puntos.

**3. Prevalece la restricción ética.**
Ante cualquier duda entre una exigencia evidencial de la guía y una restricción del paquete ético, gana la restricción ética. Se documenta en el protocolo y se solicita la ruta alterna de la §4.2.

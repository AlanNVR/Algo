# Fase 0 — Reponer las fuentes del ERS en el repositorio

**Responsable:** Villafuerte Rosero Allan Noe (`AlanNVR`)
**Tiempo estimado:** 20–30 minutos
**Bloquea:** todas las demás fases del plan de acción

---

## Por qué esta fase es urgente

Las fuentes `.tex` que hoy están en `01_ERS/` del repositorio son las de la **v1.0 sin corregir**:

- El archivo principal se llama `ERS_SRS_2A_v1.0.tex`.
- Su portada declara «Versión 3.0».
- Contiene 39 requisitos funcionales, no 42.
- No incluye los diagramas de flujo de datos, ni los casos de uso `CU-11` a `CU-18`, ni los criterios
  BDD, ni la sección de componentes de inteligencia artificial.

El `ERS_v1.1.pdf` que está publicado **no se puede regenerar desde ellas**. Eso incumple el criterio
de piso **G2** (el PDF debe generarse clonando el repositorio y compilando el `.tex`), cuya sanción
es la calificación cero.

Además, el `README.md` actual apunta a `01_ERS/ERS_SRS_2A.tex`, archivo que no existe en el
repositorio: copiar y pegar sus comandos de compilación falla.

---

## Contenido de este paquete

```
Fase0_ERS/
├── LEEME_FASE0.md              este archivo
├── README.md                   versión actualizada, para la raíz del repositorio
└── 01_ERS/
    ├── ERS_SRS_2A.tex          archivo principal (nombre nuevo, sin sufijo de versión)
    ├── seccion4_uml.tex        modelado UML e i*  ·  ahora carga cu_11_18.tex
    ├── seccion5_priorizacion.tex
    ├── seccion6_7_mvp_conclusiones.tex
    ├── seccion8_dfd.tex        NUEVO — diagramas de flujo de datos en TikZ
    ├── seccion9_ia.tex         NUEVO — componentes de inteligencia artificial
    ├── cu_11_18.tex            NUEVO — especificación de CU-11 a CU-18
    ├── apendice_bdd.tex        NUEVO — criterios CB-01 a CB-37
    ├── apendices.tex           ahora carga apendice_bdd.tex
    ├── referencias.bib         35 entradas (se añadieron el Reglamento UE y la LOPDP)
    └── img/                    las 14 figuras, idénticas a las del repositorio
```

Las figuras van incluidas por comodidad, para que el paquete compile por sí solo. Si prefieren
conservar las que ya están en el repositorio, son las mismas: pueden omitir la carpeta.

---

## Pasos

### 1. Comprobar el estado actual

Antes de tocar nada, conviene ver de qué se parte:

```bash
cd ISR401-PFC-ERS-EQUIPO_B/01_ERS
ls *.tex
grep -n "bfseries Versión" ERS_SRS_2A_v1.0.tex
grep -c "^\\\\RF{" ERS_SRS_2A_v1.0.tex
```

Debe devolver `ERS_SRS_2A_v1.0.tex`, «Versión: 3.0» y `39`. Si devuelve otra cosa, **parar y avisar
al equipo**: alguien ya tocó las fuentes y hay que revisar qué se cambió antes de sobrescribir.

### 2. Retirar las fuentes antiguas

```bash
cd ISR401-PFC-ERS-EQUIPO_B/01_ERS
git rm ERS_SRS_2A_v1.0.tex seccion4_uml.tex seccion5_priorizacion.tex \
       seccion6_7_mvp_conclusiones.tex apendices.tex referencias.bib
```

**No borrar `img/` ni los PDF.** `ERS_v1.0.pdf` se conserva: es el documento sobre el que se ejecutó
la inspección de la Unidad IV y con el que se comparan las correcciones.

### 3. Copiar las fuentes nuevas

Descomprimir este paquete y copiar el contenido de su carpeta `01_ERS/` sobre `01_ERS/` del
repositorio. Deben quedar diez archivos `.tex` más `referencias.bib` más `img/`.

```bash
ls *.tex | wc -l    # debe devolver 10
```

### 4. Compilar

```bash
pdflatex ERS_SRS_2A
bibtex   ERS_SRS_2A
pdflatex ERS_SRS_2A
pdflatex ERS_SRS_2A
```

Las tres pasadas de `pdflatex` son obligatorias: la primera genera el `.aux`, `bibtex` resuelve las
citas y las dos siguientes fijan índices y referencias cruzadas.

**Resultado esperado: 106 páginas, sin errores y sin citas sin resolver.** Comprobación:

```bash
grep -cE "^!" ERS_SRS_2A.log                    # debe devolver 0
grep -c "Citation.*undefined" ERS_SRS_2A.log    # debe devolver 0
```

Si falla por paquetes ausentes:

```bash
sudo apt-get install -y texlive-lang-spanish texlive-publishers \
                        texlive-science texlive-pictures texlive-latex-extra
```

En MiKTeX se instalan solos al compilar; basta con aceptar las descargas.

### 5. Sustituir el PDF publicado

```bash
mv ERS_SRS_2A.pdf ERS_v1.1.pdf
```

Este PDF **reemplaza** al `ERS_v1.1.pdf` anterior. El que estaba publicado no incorporaba todas las
correcciones que el informe de la PE4 declaraba aplicadas, y esa discrepancia es precisamente lo que
la re-inspección de la PE5 registró como los siete defectos residuales de la métrica M6.

### 6. Actualizar el README

Copiar el `README.md` de este paquete a la **raíz** del repositorio, sustituyendo el anterior.
Corrige el nombre del archivo principal y añade una sección que documenta por qué el `ERS_v1.1.pdf`
publicado en la PE4 no coincidía con sus fuentes.

### 7. Commits

Dos commits, ambos desde la cuenta de Villafuerte:

```bash
cd ISR401-PFC-ERS-EQUIPO_B

git add 01_ERS/*.tex 01_ERS/referencias.bib
git commit -m "fix(ers): reponer fuentes LaTeX correspondientes a la v1.1" \
           -m "Las fuentes publicadas en la PE4 correspondían a la v1.0 sin corregir, de modo que el
PDF entregado no se regeneraba desde el repositorio. Se reponen las fuentes que sí lo generan e
incorporan los diagramas de flujo de datos (§8), los componentes de IA (§9), la especificación de
CU-11 a CU-18 y los criterios BDD del Apéndice F."

git add 01_ERS/ERS_v1.1.pdf README.md
git commit -m "docs(ers): v1.1 final con DFD, casos de uso, criterios BDD y componentes de IA" \
           -m "Cierra M1b (18/18 casos de uso especificados) y M3 (61/61 criterios con criterio BDD).
El README declara qué versión producen las fuentes y por qué ERS_v1.0.pdf se conserva sin regenerar."

git push
```

---

## Verificación final

Desde una carpeta limpia, y preferiblemente en la máquina de otro integrante:

```bash
cd /tmp && rm -rf prueba
git clone https://github.com/erizzov-boop/ISR401-PFC-ERS-EQUIPO_B.git prueba
cd prueba/01_ERS
pdflatex ERS_SRS_2A && bibtex ERS_SRS_2A && pdflatex ERS_SRS_2A && pdflatex ERS_SRS_2A
```

Si produce 106 páginas sin errores, la Fase 0 está cerrada y G2 queda cubierto para el ERS.

---

## Lo que queda pendiente en el ERS

El documento conserva **dos marcadores rojos** que no se pueden rellenar sin datos del equipo:

| Archivo | Marcador | Qué falta |
|---|---|---|
| `ERS_SRS_2A.tex` | portada | Fecha de cierre de la PE5 |
| `seccion6_7_mvp_conclusiones.tex` | limitación `L-06` | Número efectivo de sesiones de *walkthrough* realizadas |

Se pueden dejar para el final, junto con los del informe, pero **deben estar en cero antes de la
entrega**: un marcador visible en el PDF activa el indicador S2 de la escala de integridad académica.

Comprobación:

```bash
grep -c "pendienteERS" 01_ERS/*.tex
```

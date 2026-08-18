# ISR401-PFC-ERS-EQUIPO_B

Repositorio del **Proyecto Fin de Curso** de la asignatura Ingeniería de Requerimientos (ISR-401),
Carrera de Software (Rediseño), Facultad de Ciencias de la Computación, Universidad Técnica Estatal
de Quevedo. Contiene los artefactos de las Prácticas Experimentales de la **Unidad IV (PE4)** y de la
**Unidad V (PE5)**.

**URL pública:** <https://github.com/erizzov-boop/ISR401-PFC-ERS-EQUIPO_B>

---

## 1. El sistema

**SIMPA — Sistema Inteligente de Mantenimiento de Palma Africana.**

Sistema de gestión y diagnóstico asistido para el cultivo de palma aceitera, desarrollado como
Proyecto Fin de Curso sobre una organización real del cantón El Empalme (Guayas, Ecuador). La
Especificación de Requisitos de Software (ERS) que se valida en esta práctica corresponde a la
Entrega 2A y especifica 39 requisitos funcionales, 18 no funcionales, 10 restricciones de diseño y
8 requisitos legales derivados de la Ley Orgánica de Protección de Datos Personales (LOPDP).

Esta práctica **no desarrolla software**: aplica inspección formal Fagan sobre el ERS, tramita
solicitudes de cambio ante un Change Control Board simulado, construye la trazabilidad en Jira y
establece la línea base del documento con Git.

## 2. Integrantes y roles

| Integrante | Rol en la inspección | Rol en el CCB | Usuario de GitHub |
|---|---|---|---|
| Mora Duarte Alex José | Lector | Representante del cliente | [`amorad35`](https://github.com/amorad35) |
| Rizzo Vélez Edson Nagib | Moderador e Inspector 2 | Presidente del CCB | [`erizzov-boop`](https://github.com/erizzov-boop) |
| Villafuerte Rosero Allan Noe | Inspector 1 | Analista y desarrollador | [`AlanNVR`](https://github.com/AlanNVR) |

**Declaración sobre el criterio A3.** La guía exige que los cuatro roles de la inspección
correspondan a personas distintas. El equipo está integrado por tres personas, de modo que la
exigencia no puede satisfacerse literalmente. Se acumulan los roles de Moderador e Inspector 2 en un
mismo integrante y se declara de forma expresa, en lugar de simular un cuarto participante. La
acumulación recae sobre el Moderador porque conducir y consolidar es compatible con haber realizado
preparación individual previa, mientras que mantener separados a los dos inspectores preserva la
independencia de las dos lecturas críticas del documento.

## 3. Estructura de carpetas

```
ISR401-PFC-ERS-EQUIPO_B/
├── README.md                       Este archivo
├── CHANGELOG.md                    Registro de cambios del ERS, una entrada por RFC aprobado
├── .gitignore                      Intermedios de LaTeX; los PDF SÍ se versionan
│
├── 01_ERS/                         Especificación de Requisitos de Software
│   ├── ERS_v1.0.pdf                Versión inspeccionada en la PE4 (Entrega 2A)
│   ├── ERS_v1.1.pdf                Versión final del PFC — la que generan estas fuentes
│   ├── seccion8_dfd.tex            Diagramas de flujo de datos (TikZ)
│   ├── ERS_SRS_2A.tex              Archivo principal del ERS
│   ├── seccion4_uml.tex            Modelado UML e i*
│   ├── seccion5_priorizacion.tex   MoSCoW, Kano, WSJF y matriz de trazabilidad
│   ├── seccion6_7_mvp_conclusiones.tex
│   ├── apendices.tex               Apéndices A–E
│   ├── referencias.bib
│   └── img/                        14 figuras en PDF vectorial
│
├── 02_Inspeccion/
│   ├── AnexoA_checklists/          Una copia firmada y fechada por inspector
│   ├── AnexoB_registro_defectos.xlsx
│   └── metricas.xlsx               Las cinco métricas, con fórmulas vivas
│
├── 03_CCB/
│   ├── RFC-01.pdf  RFC-02.pdf  RFC-03.pdf
│   └── Acta_CCB.pdf                Acta firmada
│
├── 04_Trazabilidad/
│   ├── matriz_trazabilidad.xlsx    52 filas, 13 columnas
│   ├── backlog_import_jira.csv     Archivo de carga generado por el equipo
│   ├── backlog_export.csv          Anexo D: exportación producida por Jira
│   └── capturas/
│
├── 05_Informe/
│   ├── PE4_U4_MORA_RIZZO_VILLAFUERTE.tex    Archivo principal del informe
│   ├── referencias.bib
│   ├── PE4_U4_MORA_RIZZO_VILLAFUERTE.pdf
│   └── figuras/
│
└── 06_Evidencias/
    ├── capturas_git/               git log --oneline --graph --decorate y git tag -n
    ├── fotos_sesion/
    └── declaracion_IA.pdf
```

## 4. Instrucciones de compilación

### 4.1 Dependencias

| Requisito | Versión de referencia | Por qué |
|---|---|---|
| Distribución LaTeX | TeX Live 2023 o superior (MiKTeX equivalente) | Compilador |
| `pdflatex` | Incluido en la distribución | Motor de compilación |
| `bibtex` | Incluido en la distribución | Procesa `referencias.bib` |

**Paquetes que no vienen en una instalación mínima** y que hay que instalar de forma explícita:

| Paquete Debian/Ubuntu | Provee | Se necesita para |
|---|---|---|
| `texlive-lang-spanish` | `spanish.ldf` | Opción `spanish` de `babel` (partición silábica y rótulos en español) |
| `texlive-publishers` | `IEEEtran.bst` | Estilo bibliográfico IEEE exigido por la guía |
| `texlive-science` | `siunitx` | Formato numérico con coma decimal |
| `texlive-pictures` | `pgfplots`, `tikz` | Gráficos de las métricas de inspección |
| `texlive-latex-extra` | `booktabs`, `enumitem`, `float`, `caption`, `multirow`, `xurl`, `adjustbox`, `titlesec`, `hyphenat` | Tablas, listas y composición |

Instalación completa en Debian/Ubuntu:

```bash
sudo apt-get install -y texlive-latex-base texlive-latex-recommended \
    texlive-latex-extra texlive-lang-spanish texlive-publishers \
    texlive-science texlive-pictures texlive-fonts-recommended
```

En MiKTeX, la instalación bajo demanda resuelve estos paquetes automáticamente la primera vez que se
compila; basta con aceptar las descargas.

> **Nota sobre robustez.** Tanto el ERS como el informe cargan `babel` y el estilo `IEEEtran` de forma
> **condicional**, mediante `\IfFileExists`. Si alguno de los dos paquetes falta, el documento compila
> igual — con partición silábica inglesa y estilo `unsrt` — en lugar de abortar. Esto evita que una
> instalación incompleta produzca un fallo de compilación, pero el PDF entregado se genera **con
> ambos paquetes presentes**, que es la configuración de referencia.

### 4.2 Compilar el informe de la práctica

Archivo principal: `05_Informe/PE4_U4_MORA_RIZZO_VILLAFUERTE.tex`

```bash
git clone https://github.com/erizzov-boop/ISR401-PFC-ERS-EQUIPO_B.git
cd ISR401-PFC-ERS-EQUIPO_B/05_Informe

pdflatex PE4_U4_MORA_RIZZO_VILLAFUERTE
bibtex   PE4_U4_MORA_RIZZO_VILLAFUERTE
pdflatex PE4_U4_MORA_RIZZO_VILLAFUERTE
pdflatex PE4_U4_MORA_RIZZO_VILLAFUERTE
```

Las **tres pasadas de `pdflatex` son obligatorias**: la primera genera el `.aux`, `bibtex` resuelve
las referencias, y las dos siguientes fijan el índice, las referencias cruzadas y la numeración de
tablas y figuras. Con menos pasadas aparecen marcas `??` en el PDF.

Resultado esperado: el PDF correspondiente, sin errores y sin referencias sin resolver.

### 4.3 Compilar el ERS

Archivo principal: `01_ERS/ERS_SRS_2A.tex`

```bash
cd ISR401-PFC-ERS-EQUIPO_B/01_ERS

pdflatex ERS_SRS_2A
bibtex   ERS_SRS_2A
pdflatex ERS_SRS_2A
pdflatex ERS_SRS_2A
```

El documento carga cuatro archivos por `\input` (`seccion4_uml.tex`, `seccion5_priorizacion.tex`,
`seccion6_7_mvp_conclusiones.tex`, `apendices.tex`) y las figuras de `img/`. Compilar cualquiera de
esos archivos por separado no produce salida útil.

> **Qué versión producen estas fuentes.** Las fuentes de `01_ERS/` generan **`ERS_v1.1.pdf`**, que es la
> versión final del PFC. `ERS_v1.0.pdf` se conserva como artefacto histórico: es el documento sobre el
> que se ejecutó la inspección formal de la PE4 y con el que se comparan las correcciones, de modo que
> no se regenera desde estas fuentes.
>
> **Las fuentes de la v1.0 no se duplican en una carpeta paralela.** Están congeladas en el historial
> con la etiqueta `ers-v1.0`, y se recuperan con `git checkout ers-v1.0 -- 01_ERS/`. Mantener dos
> copias de los mismos archivos es el mecanismo que produjo los once defectos de consistencia
> detectados en la inspección de la Unidad IV; Git ya versiona y la etiqueta hace el resto. El detalle
> está en `01_ERS/LEEME.md`.
>
> Véase también la nota de la sección 5 bis.

### 4.4 Verificación rápida

```bash
grep -c "PENDIENTE" 05_Informe/PE4_U4_MORA_RIZZO_VILLAFUERTE.tex   # debe devolver 0 antes de entregar
grep -i "undefined" 05_Informe/*.log                               # no debe devolver nada
```

## 5. Línea base

La línea base del ERS aprobada por el CCB se publica como etiqueta anotada de Git:

```bash
git tag -n                    # lista las etiquetas con su mensaje
git show ers-v1.0             # fuentes del ERS inspeccionado en la PE4
git show baseline-v1.1        # línea base aprobada por el CCB
git show baseline-final       # línea base de cierre del PFC (PE5)
```

La versión vigente del ERS es la **v1.1**, y se declara de forma idéntica en la portada del documento,
en su historial de revisiones, en `CHANGELOG.md` y en la etiqueta anotada de Git. La etiqueta
`baseline-v1.1` marca la línea base aprobada por el CCB al cierre de la PE4; `baseline-final` marca el
cierre del proyecto integrador tras la auditoría de la PE5.

**Sobre la numeración de versiones.** El ERS del SIMPA registra internamente sus revisiones desde la
Entrega 1A y llegó a la Entrega 2A como revisión interna 3.0. La asignatura emplea una numeración
distinta: designa como **v1.0** al documento de la Entrega 2A y como **v1.1** a la versión resultante
del CCB de esta práctica. Se adopta la numeración de la asignatura como versión oficial.

Para que la coexistencia de ambas no produzca una ambigüedad, el historial del ERS rotula su columna
como *Revisión interna* —no como *Versión*— y declara la equivalencia de forma explícita:

| Numeración de la asignatura | Revisión interna | Entrega |
|---|---|---|
| **v1.0** | 3.0 | Entrega 2A (documento inspeccionado) |
| **v1.1** | 3.1 | Resultante del CCB de la PE4 |

Las revisiones internas 1.0, 1.1 y 2.0 que figuran en el historial del ERS corresponden a las
Entregas 1A y 1B y **no** son las versiones v1.0 y v1.1 de la asignatura. La distinción está
declarada dentro del propio ERS, en el recuadro que sigue al historial de versiones.

## 5 bis. Nota sobre el contenido de `ERS_v1.1.pdf`

El PDF publicado al cierre de la PE4 no incorporaba la totalidad de las correcciones que el informe de
aquella práctica declaraba aplicadas: conservaba la contradicción entre 48 y 52 filas de la matriz, no
incluía las historias de usuario de `RF-36` y `RF-37` y no recalculaba la cobertura del MVP.

La re-inspección de la PE5 detectó esas discrepancias junto con otras cinco, y todas se cierran en la
versión que generan las fuentes de `01_ERS/`. **`ERS_v1.1.pdf` se regenera desde el repositorio** y
sustituye al publicado en la PE4: la versión declarada no cambia, cambia su contenido. El resultado
de la re-inspección es el dato empírico de la métrica M6 de la auditoría de calidad
(`02_Auditoria/AnexoA_auditoria_calidad.xlsx`, hoja `Reinspeccion_M6`).

## 6. Contexto académico

| | |
|---|---|
| Asignatura | Ingeniería de Requerimientos (ISR-401) — 4.º nivel |
| Unidad | IV — Validación, Gestión de Requisitos y Herramientas CASE |
| Docente | Ing. Gleiston Cicerón Guerrero Ulloa, PhD |
| Periodo | 2026–2027 PPA |
| Entregable | `PE4_U4_MORA_RIZZO_VILLAFUERTE.pdf` |

## 7. Declaración de uso de inteligencia artificial

El uso de asistentes de IA en la elaboración de estos artefactos se declara de forma detallada en el
**Anexo F** del informe: herramienta, versión, tarea asistida, fragmento afectado y verificación
crítica realizada por el equipo, con firma de los integrantes.

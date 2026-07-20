# Especificación del modelo UML de origen — SIMPA

## Propósito

Este modelo refina el diagrama conceptual del PFC para convertirlo en un modelo apto para generación de esqueletos C# con Visual Paradigm. No reemplaza los diagramas anteriores: debe ubicarse como una vista nueva denominada **`MDD_Origen_SIMPA`** dentro del archivo existente `SIMPA_MDD_Grupo_C.vpp`.

## Paquetes recomendados

- `SIMPA.Dominio`: clases del dominio y enumeraciones.
- `SIMPA.Aplicacion`: servicios de aplicación.
- `SIMPA.Persistencia`: interfaces de repositorio.
- `SIMPA.Integraciones`: servicios externos y DTO.

## Clases del dominio

### `Plantacion` — «Entity»

Atributos:

- `- idPlantacion: int`
- `- nombre: string`
- `- ubicacion: string`

Operaciones:

- `+ registrarLote(lote: Lote): void`
- `+ buscarLote(codigo: string): Lote`
- `+ listarLotes(): List<Lote>`

Trazabilidad: RF-002.

### `Lote` — «Entity»

Atributos:

- `- idLote: int`
- `- codigo: string`
- `- areaHectareas: decimal`
- `- fechaSiembra: DateTime`
- `- etapaActual: EtapaCultivo`

Operaciones:

- `+ agregarPalma(palma: Palma): void`
- `+ registrarLabor(labor: Labor): void`
- `+ consultarHistorial(desde: DateTime, hasta: DateTime): List<Labor>`

Trazabilidad: RF-002, RF-006, RF-020.

### `Palma` — «Entity»

Atributos:

- `- idPalma: int`
- `- codigo: string`
- `- estado: EstadoPalma`
- `- fechaUltimoMantenimiento: DateTime [0..1]`

Operaciones:

- `+ actualizarEstado(nuevoEstado: EstadoPalma): void`
- `+ registrarMantenimiento(labor: Labor): void`
- `+ requiereMantenimiento(fechaReferencia: DateTime): bool`

Trazabilidad: RF-002, RF-004, RF-005, RF-020.

### `Usuario` — «Entity», clase abstracta

Atributos:

- `- idUsuario: int`
- `- nombre: string`
- `- cedula: string`
- `- nombreUsuario: string`
- `- rol: RolUsuario`

Operaciones:

- `+ autenticar(clave: string): bool`
- `+ cerrarSesion(): void`

Trazabilidad: RF-001.

### `Trabajador` — «Entity»

Generalización: `Trabajador --|> Usuario`.

Atributos:

- `- equipo: string`

Operaciones:

- `+ registrarLabor(labor: Labor): void`
- `+ consultarLabores(fecha: DateTime): List<Labor>`

Trazabilidad: RF-003, RF-004.

### `Labor` — «Entity»

Atributos:

- `- idLabor: int`
- `- tipo: TipoLabor`
- `- fecha: DateTime`
- `- descripcion: string`
- `- estado: EstadoLabor`

Operaciones:

- `+ validar(): bool`
- `+ completar(observacion: string): void`
- `+ estaCompletada(): bool`

Trazabilidad: RF-004, RF-020.

### `Diagnostico` — «Entity»

Atributos:

- `- idDiagnostico: int`
- `- fecha: DateTime`
- `- tipo: TipoDiagnostico`
- `- resultado: string`
- `- nivelConfianza: decimal`
- `- severidad: Severidad`

Operaciones:

- `+ actualizarResultado(resultado: string, confianza: decimal): void`
- `+ esCritico(): bool`
- `+ generarAlerta(): Alerta`

Trazabilidad: RF-005, RF-007, RF-008.

### `Alerta` — «Entity»

Atributos:

- `- idAlerta: int`
- `- tipo: TipoAlerta`
- `- fecha: DateTime`
- `- estado: EstadoAlerta`
- `- mensaje: string`
- `- fechaAtencion: DateTime [0..1]`

Operaciones:

- `+ marcarAtendida(fechaAtencion: DateTime): void`
- `+ estaPendiente(): bool`

Trazabilidad: RF-012.

## Clases técnicas para la vista de generación

### `MantenimientoService` — «Service»

- `+ registrarLabor(idPalma: int, idTrabajador: int, tipo: TipoLabor, fecha: DateTime, descripcion: string): Labor`
- `+ registrarDiagnostico(idPalma: int, imagen: byte[]): Diagnostico`
- `+ consultarHistorial(idLote: int, desde: DateTime, hasta: DateTime): List<Labor>`

### `IPalmaRepository` — «Repository», interfaz

- `+ obtenerPorId(idPalma: int): Palma`
- `+ listarPorLote(idLote: int): List<Palma>`
- `+ guardar(palma: Palma): void`

### `IServicioAnalisisIA` — «ExternalService», interfaz

- `+ analizar(imagen: byte[]): ResultadoAnalisisDTO`

### `ResultadoAnalisisDTO` — «DTO»

Atributos:

- `+ tipo: TipoDiagnostico`
- `+ resultado: string`
- `+ confianza: decimal`
- `+ severidad: Severidad`

Operación:

- `+ esValido(): bool`

## Enumeraciones

- `RolUsuario { ADMINISTRADOR, TECNICO_ASESOR, TRABAJADOR }`
- `EtapaCultivo { SIEMBRA, CRECIMIENTO, POLINIZACION, COSECHA }`
- `EstadoPalma { NORMAL, OBSERVACION, AFECTADA, INACTIVA }`
- `TipoLabor { RIEGO, POLINIZACION, CONTROL_FITOSANITARIO, CHAPIA, CORONA, PODA, PODA_SANITARIA }`
- `EstadoLabor { REGISTRADA, EN_PROCESO, COMPLETADA, CANCELADA }`
- `TipoDiagnostico { PLAGA, ENFERMEDAD, DEFICIENCIA_NUTRICIONAL }`
- `Severidad { BAJA, MEDIA, ALTA, CRITICA }`
- `TipoAlerta { FITOSANITARIA, NUTRICIONAL, MANTENIMIENTO }`
- `EstadoAlerta { ABIERTA, EN_ATENCION, ATENDIDA }`

## Relaciones y cardinalidades

| Origen | Relación | Destino | Multiplicidad |
|---|---|---|---|
| Plantacion | composición | Lote | `Plantacion 1` — `Lote 1..*` |
| Lote | composición | Palma | `Lote 1` — `Palma 1..*` |
| Lote | asociación | Labor | `Lote 1` — `Labor 0..*` |
| Trabajador | asociación «responsable» | Labor | `Trabajador 1` — `Labor 0..*` |
| Palma | asociación opcional | Labor | `Palma 0..1` — `Labor 0..*` |
| Palma | asociación | Diagnostico | `Palma 1` — `Diagnostico 0..*` |
| Diagnostico | asociación «genera» | Alerta | `Diagnostico 1` — `Alerta 0..1` |
| Trabajador | generalización | Usuario | herencia |
| MantenimientoService | dependencia | IPalmaRepository | uso |
| MantenimientoService | dependencia | IServicioAnalisisIA | uso |
| MantenimientoService | dependencia | Labor, Diagnostico, Alerta | creación/consulta |

## Reglas de modelado para la generación

1. Todos los atributos deben tener tipo explícito y visibilidad privada.
2. Todas las operaciones deben indicar parámetros, tipos y tipo de retorno.
3. No crear atributos duplicados para relaciones ya representadas mediante asociaciones.
4. Las colecciones se derivan de las multiplicidades `0..*` y `1..*`.
5. `Usuario` debe marcarse como abstracta.
6. Los repositorios y servicios externos deben modelarse como interfaces.
7. Validar el modelo con Model Quality antes de generar.
8. Mantener el diagrama conceptual anterior sin cambios y crear una vista nueva para este modelo de origen.

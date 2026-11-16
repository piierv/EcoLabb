# ♻️ Avances de la propuesta — Aplicación web y contenedores inteligentes

Esta sección reúne el estado de desarrollo de la solución EcoFab Lab según el informe de avance del equipo de noviembre de 2026. Se distingue entre las funciones que ya están construidas en el prototipo, los componentes que siguen pendientes y las etapas que todavía deben validarse.

## 💻 Aplicación web de registro de residuos

El equipo desarrolló un **prototipo web** que se puede abrir desde el navegador, sin necesidad de instalar una aplicación en el celular. La propuesta contempla dos vistas conectadas: el formulario que utiliza la persona que genera el residuo y el panel destinado al equipo operador del Lab881.

### 1. Vista de la persona usuaria

El flujo comienza escaneando el código QR de la estación. Luego, la persona registra:

- Material que necesita desechar.
- Proceso u origen del residuo.
- Máquina relacionada.
- Cantidad aproximada (con opción de indicar gramos).

Con esa información, el sistema asigna uno de los cuatro contenedores y muestra dónde depositar el residuo:

| Contenedor | Tipo de residuo |
|---|---|
| A | PLA |
| B | Resina endurecida, con confirmación previa de curado |
| C | Resina líquida y alcohol; manejo exclusivo del operador |
| D | Residuos de la cortadora láser |

Después de depositar el material, la persona escanea el QR del contenedor para confirmar. Si escanea uno distinto al asignado, el sistema indica cuál corresponde y deja el registro marcado como corregido.

También se incorporaron reglas de seguridad: solicitar confirmación del curado para la resina endurecida, derivar la resina líquida al operador y mostrar una advertencia que bloquea el registro de PVC para corte láser.

### 2. Panel del equipo operador

El prototipo incluye un panel para que el operador pueda revisar la información registrada. Entre sus funciones se encuentran:

- Visualizar el estado de los cuatro contenedores.
- Consultar alertas de llenado.
- Revisar los kilos registrados por material.
- Identificar las máquinas que presentan más fallas.
- Consultar los últimos registros y los retiros.
- Registrar el retiro de un contenedor y generar un lote con su peso, contenido y gestor.

El panel se actualiza cuando se realiza un nuevo registro. El acceso de esta vista considera inicio de sesión, mientras que el formulario de las personas usuarias no solicita datos personales.

## 🧪 Estado del prototipo web

Según el informe de avance, el prototipo implementa el flujo principal utilizando **datos simulados**. El equipo reporta que las nueve pruebas funcionales internas realizadas en el navegador fueron satisfactorias.

Entre los casos probados se encuentran el registro de PLA y su asignación al contenedor A, la confirmación del depósito, la validación del curado de resina, la detección y corrección de un contenedor equivocado, el manejo de resina líquida y las funciones del panel y del registro de retiros.

Es importante señalar que estas pruebas son internas: permiten comprobar el comportamiento del prototipo, pero todavía no demuestran su funcionamiento con usuarios reales ni con datos reales del Lab881.

## 🗑️ Segunda etapa: contenedores inteligentes

Como proyección, la propuesta considera incorporar sensores a los contenedores para medir automáticamente el peso y el nivel de llenado. El diseño contempla:

- **ESP32:** microcontrolador que recopilaría las lecturas y las enviaría mediante Wi-Fi.
- **Celdas de carga y módulo HX711:** medirían el peso acumulado.
- **Sensor ultrasónico:** estimaría el espacio ocupado dentro del contenedor.
- **Alertas de llenado:** el sistema avisaría al operador al alcanzar el 80 % y el 95 %.

El cálculo considera el mayor valor entre el porcentaje de llenado por peso y por volumen. Esto es relevante para residuos livianos y voluminosos, como recortes de MDF, que pueden ocupar mucho espacio sin alcanzar un peso elevado.

Esta parte corresponde a una segunda fase y todavía no está integrada al prototipo web mediante sensores reales.

## 📊 Estado de desarrollo

| Componente | Estado informado | Observación |
|---|---|---|
| Formulario web de registro, asignación y confirmación | Construido | Funciona con datos simulados |
| Reglas de seguridad para resina y PVC | Construidas | Probadas internamente |
| Detección y corrección de contenedor equivocado | Construida | Marca el registro como corregido |
| Panel del operador y alertas | Construido | Se actualiza con los registros simulados |
| Registro de retiros y generación de lotes | Construido | Funciona en el prototipo |
| Servidor y API con base de datos real | Pendiente | El prototipo aún no guarda información en una base real |
| Recepción de lecturas desde ESP32 | Pendiente | Requiere el servidor real |
| Señalética, rótulos y códigos QR | En desarrollo según el informe | Deben prepararse para la estación |
| Protocolo de manejo de resina e instructivo del operador | En desarrollo según el informe | Documentos de apoyo para la operación |
| Contenedor con sensores en banco de pruebas | Pendiente | Requiere componentes y armado |
| Piloto con usuarios en el Lab881 | Pendiente | Depende de la autorización del Hub |

## 🔜 Próximos pasos

1. Completar la señalética y los códigos QR para los contenedores.
2. Terminar el protocolo de manejo de resina y el instructivo para el operador.
3. Implementar el servidor y la base de datos para almacenar registros reales.
4. Construir y probar en banco un contenedor con celda de carga, HX711, sensor ultrasónico y ESP32.
5. Validar el formulario y el panel con usuarios reales, si se obtiene autorización del Hub.
6. Revisar los resultados del piloto y ajustar el sistema según las dificultades observadas.

## ✅ Síntesis del avance

EcoFab Lab ya cuenta con un prototipo web que representa el recorrido del residuo desde su registro hasta la confirmación del depósito, además de un panel para el operador y funciones de seguimiento. El equipo informa que el flujo principal superó nueve pruebas funcionales internas con datos simulados.

El trabajo pendiente se concentra en conectar el prototipo a una base de datos real, integrar los sensores físicos, completar los materiales de apoyo y validar la solución en las condiciones reales del Lab881. Por lo tanto, el avance es un prototipo funcional a nivel de demostración, todavía no una implementación operativa en el laboratorio.

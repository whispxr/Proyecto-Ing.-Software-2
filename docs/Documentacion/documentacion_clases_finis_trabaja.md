# Documentación Técnica del Modelo de Clases: "Finis Trabaja"

## 1. Contexto y Arquitectura Base
El presente documento detalla la estructura orientada a objetos del sistema **Finis Trabaja**. La arquitectura está diseñada para ser implementada en Java, utilizando fuertemente los principios de herencia (para los roles de usuario), polimorfismo (mediante interfaces para búsquedas y recomendaciones), y clases asociativas (para el manejo de postulaciones).

---

## 2. Interfaces (Contratos de Comportamiento)

### `<<Interface>> IFiltrable`
Define el contrato para cualquier entidad que deba ser sometida al motor de búsqueda del sistema.
* **Métodos:**
  * `+ boolean cumpleFiltros(Map<String, String> criteriosBusqueda)`: Recibe un mapa clave-valor con los filtros (ej. "jornada" -> "Part-time", "carrera" -> "Informática"). La clase que lo implemente debe iterar sobre estos criterios y retornar `true` solo si sus atributos coinciden con todos los filtros exigidos.

### `<<Interface>> IRecomendable`
Establece la capacidad de una entidad para ser procesada por el algoritmo de "Match" o recomendación.
* **Métodos:**
  * `+ double calcularIndiceCompatibilidad(CVV perfilEstudiante)`: Contiene la lógica matemática/condicional. Compara los atributos internos de la clase que lo implementa contra los atributos del `CVV` entregado por parámetro, retornando un valor entre 0.0 y 100.0 (porcentaje de compatibilidad).

---

## 3. Clases Base y Tipos de Usuario

### `<<Abstract Class>> Usuario`
Superclase que centraliza la lógica de autenticación y datos básicos de cualquier individuo o entidad que ingrese al sistema.
* **Atributos:**
  * `- String idUsuario`: Identificador único (UUID o Primary Key de base de datos).
  * `- String correo`: Credencial principal de acceso. Debe validarse formato.
  * `- String contrasena`: Hash de seguridad (no guardar en texto plano).
  * `- Date fechaRegistro`: Timestamp de la creación de la cuenta.
* **Métodos:**
  * `+ boolean iniciarSesion(String correoIngresado, String contrasenaIngresada)`: Valida las credenciales contra la base de datos.
  * `+ void cerrarSesion()`: Destruye el token o sesión activa.
  * `+ abstract void accederDashboard()`: Método abstracto puro. Obliga a las clases hijas a definir a qué pantalla/módulo son redirigidos tras un login exitoso.

### `Estudiante (extends Usuario)`
* **Atributos:**
  * `- String rut`: Identificador nacional.
  * `- String nombre` / `- String apellidos`
  * `- CVV perfilProfesional`: Composición (1:1). Instancia exclusiva del currículum de este estudiante.
* **Métodos:**
  * `+ void postular(OfertaLaboral oferta, String cartaPresentacion)`: Instancia un nuevo objeto de la clase asociativa `Postulacion`, vinculando este objeto `Estudiante` (this) con la `oferta` recibida.
  * `+ void crearCVV(CVV datosNuevos)`: Inicializa y asigna el objeto `CVV` al estudiante.
  * `@Override + void accederDashboard()`: Carga la vista de buscador de ofertas.

### `Empleador (extends Usuario)`
* **Atributos:**
  * `- String rutEmpresa`: Identificador tributario o interno de la universidad.
  * `- String razonSocial` / `- String descripcionInstitucional`
  * `- boolean estaValidadoPorAdmin`: Bandera de seguridad. Por defecto es `false`. Si es `false`, el sistema debe bloquear el uso de `publicarOferta()`.
* **Métodos:**
  * `+ void publicarOferta(OfertaLaboral nuevaOferta)`: Agrega la oferta a la base de datos vinculándola a este empleador (Composición 1:N).
  * `+ List<Postulacion> verPostulantes(OfertaLaboral oferta)`: Consulta a la base de datos por todas las instancias de `Postulacion` asociadas a esa oferta específica.
  * `+ ArchivoAdjunto descargarCVV(Estudiante postulante)`: Accede a los archivos adjuntos dentro del `CVV` del postulante.

### `Administrador (extends Usuario)`
* **Métodos:**
  * `+ void validarEmpleador(Empleador empleadorPendiente)`: Cambia la bandera `estaValidadoPorAdmin` a `true` en el objeto Empleador.
  * `+ void habilitarRecomendacionesParaEmpresa(OfertaLaboral oferta, boolean acceso)`: Permite al admin decidir si una empresa externa puede ver el listado generado por el `MotorDeRecomendacion`.

---

## 4. Entidades del Dominio (Datos Estructurales)

### `CVV (implements IFiltrable)`
* **Atributos:**
  * Colecciones (`List<String>`): `especialidades`, `rolesDeInteres`, `experienciasLaborales`, `logrosAcademicos`. Estructuras de datos para almacenar múltiples etiquetas.
  * `- int pretensionSueldoMinima`: Valor numérico para cruce matemático.
  * `- String disponibilidadJornada` / `- String preferenciaModalidad`: Variables categóricas.
  * `- List<ArchivoAdjunto> archivosAdicionales`: Agregación (1:N). Punteros a los archivos en el servidor.
  * `- String nivelDeVisibilidad`: Control de acceso (Ej: "EMPRESAS", "SOLO_FINIS").
* **Métodos:**
  * `+ void actualizarDatos(CVV datosModificados)`: Sobrescribe los atributos actuales con los del objeto recibido.
  * `@Override + boolean cumpleFiltros(Map<String, String> criterios)`: Implementación de la interfaz para buscar estudiantes desde el panel de admin.

### `OfertaLaboral (implements IFiltrable, IRecomendable)`
* **Atributos:**
  * Datos descriptivos: `tituloCargo`, `descripcionDetallada`, `funcionesAsociadas`, `ubicacionFisica`.
  * `- List<String> carrerasDirigidas`: Colección de carreras válidas para el puesto.
  * Rango salarial: `- int sueldoMinimo`, `- int sueldoMaximo`.
  * `- boolean estadoActivo`: Si es `false`, la oferta ya no aparece en las búsquedas ni acepta postulaciones.
  * `- List<ArchivoAdjunto> materialAdjunto`: Agregación (1:N) de archivos corporativos.
* **Métodos:**
  * `@Override + double calcularIndiceCompatibilidad(CVV perfilEstudiante)`: Algoritmo central. Compara sus requisitos (`carrerasDirigidas`, `sueldoMinimo`, `tipoJornada`) contra los atributos del `perfilEstudiante`.

### `ArchivoAdjunto`
* **Atributos:**
  * `- String rutaServidor`: Path real donde está guardado el archivo (Ej: `/var/www/uploads/cv.pdf` o una URL de un bucket de AWS/Supabase).
  * `- String tipoMime`: Extensión validada para renderizado web (Ej: `application/pdf`, `image/png`).

---

## 5. Clases Transaccionales y de Asociación

### `Postulacion` (Clase Asociativa)
Esta clase existe como consecuencia de la asociación (N:N) entre `Estudiante` y `OfertaLaboral`. Evita la redundancia de datos y permite guardar información específica del instante en que se hizo el vínculo.
* **Atributos:**
  * `- Estudiante candidato`: Referencia al estudiante que aplica.
  * `- OfertaLaboral vacante`: Referencia a la oferta aplicada.
  * `- Date fechaEnvio`: Timestamp exacto de la postulación.
  * `- String cartaPresentacion`: Texto opcional digitado al momento de postular.
  * `- String estadoProceso`: Máquina de estados (Ej: "RECIBIDA", "EN_REVISION", "ACEPTADA", "DESCARTADA").
* **Métodos:**
  * `+ void actualizarEstado(String nuevoEstado)`: Modifica el `estadoProceso`.

### `MotorDeRecomendacion`
Componente de servicio (Singleton o clase utilitaria) encargado de procesar la lógica de negocio pesada.
* **Atributos:**
  * `- List<Estudiante> cacheEstudiantesRevisados`: Memoria temporal para no re-consultar a la BD constantemente durante el procesamiento.
* **Métodos:**
  * `+ List<Recomendacion> procesarOferta(OfertaLaboral oferta)`: Obtiene a todos los estudiantes de la BD (o cache). Itera sobre ellos llamando a `oferta.calcularIndiceCompatibilidad(estudiante.getCVV())`. Si el índice supera un umbral mínimo, instancia un objeto `Recomendacion` y lo añade a la lista de retorno.

### `Recomendacion`
Representa el resultado final del cruce. Es una foto del nivel de compatibilidad en un momento dado.
* **Atributos:**
  * `- Estudiante estudianteSugerido` / `- OfertaLaboral ofertaAnalizada`
  * `- double porcentajeMatch`: El valor numérico final del cálculo.
  * `- Date fechaCalculo`: Cuándo se generó este cruce.

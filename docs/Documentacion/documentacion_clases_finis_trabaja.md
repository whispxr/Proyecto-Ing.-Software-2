# Documentación Técnica del Modelo de Clases: Proyecto "Finis Trabaja"

Esta documentación detalla la lógica, el propósito y las interconexiones de las clases diseñadas para el sistema de vinculación laboral de la Universidad Finis Terrae.

---

## 1. Contexto del Sistema
El modelo está diseñado para resolver la desorganización en la comunicación de vacantes laborales. Funciona como un ecosistema donde la **demanda** (empresas y departamentos de la universidad) y la **oferta** (estudiantes) se encuentran mediante un **Motor de Recomendación**. La arquitectura prioriza la seguridad de los datos, la escalabilidad mediante interfaces y la claridad en los roles de usuario.

---

## 2. Contratos de Comportamiento (Interfaces)

### `IFiltrable`
* **Propósito:** Define un estándar para que cualquier entidad pueda ser buscada mediante criterios específicos.
* **Relaciones:** Implementada por `CVV` y `OfertaLaboral`.
* **Variables de método:** * `Map<String, String> criteriosBusqueda`: Un diccionario de filtros (ej: "Sueldo" -> "500.000") que permite al sistema evaluar si el objeto cumple con lo solicitado por el usuario.

### `IRecomendable`
* **Propósito:** Permite que una entidad sea evaluada numéricamente por el algoritmo de emparejamiento.
* **Relaciones:** Implementada por `OfertaLaboral`.
* **Lógica:** Compara los requisitos técnicos de una vacante contra los datos de un perfil estudiantil.

---

## 3. Gestión de Identidad (Herencia de Usuarios)

### `Usuario` (Clase Abstracta)
* **Propósito:** Actúa como la plantilla base para cualquier persona que acceda al sistema. Centraliza la seguridad y los datos de acceso.
* **Atributos:**
    * `idUsuario`: Identificador único interno para la base de datos.
    * `correo`: Email institucional o corporativo; actúa como nombre de usuario.
    * `contrasena`: Almacena el hash de seguridad para la validación.
    * `fechaRegistro`: Fecha automática en la que se creó la cuenta.

### `Estudiante`
* **Contexto:** Representa al alumno que busca empleo o prácticas.
* **Atributos:**
    * `rut`, `nombre`, `apellidos`: Datos de identificación personal.
    * `perfilProfesional`: Instancia vinculada de la clase `CVV`.
* **Relación:** **Composición (1:1)** con `CVV`. Si el estudiante desaparece, su currículum también.

### `Empleador`
* **Contexto:** Representa al reclutador. Puede ser un "Headhunter" externo o un encargado de departamento dentro de la UFT.
* **Atributos:**
    * `rutEmpresa`: RUT comercial para externos o identificador interno para la universidad.
    * `razonSocial`: Nombre legal de la empresa o nombre del área (ej: "Biblioteca UFT").
    * `estadoCuenta`: Almacena el estado administrativo (`PENDIENTE`, `APROBADA`, `RECHAZADA`).
    * `esInterno`: Booleano crítico para omitir requisitos tributarios en departamentos universitarios.
* **Relación:** **Asociación (1:N)** con `OfertaLaboral`. Un empleador puede gestionar múltiples vacantes.

### `Administrador`
* **Contexto:** Personal de Vinculación con el Medio que supervisa la plataforma.
* **Lógica:** No posee atributos de dominio, sino métodos de control para validar a los empleadores y supervisar el sistema.

---

## 4. Estructuras de Datos y Dominio

### `CVV` (Currículum Vitae Virtual)
* **Contexto:** Es el corazón de la información del alumno. No es un documento estático, sino una entidad de datos para el motor de búsqueda.
* **Atributos:**
    * `especialidades`, `rolesDeInteres`: Listas de etiquetas para el motor de recomendación.
    * `pretensionSueldoMinima`: Número entero usado para filtrar ofertas por debajo de la expectativa del alumno.
    * `disponibilidadJornada`, `preferenciaModalidad`: Categorías para el cruce de datos (Remoto, Presencial, etc.).
    * `nivelDeVisibilidad`: Define si el perfil es público, solo para la universidad o privado.

### `OfertaLaboral`
* **Contexto:** Especificación de la vacante publicada.
* **Atributos:**
    * `tituloCargo`, `descripcionDetallada`, `funcionesAsociadas`: Textos informativos para el postulante.
    * `carrerasDirigidas`: Lista de títulos que pueden postular.
    * `sueldoMinimo`, `sueldoMaximo`: Rango económico para evaluar la afinidad con el estudiante.
    * `estadoActivo`: Booleano para ocultar ofertas cerradas.

### `ArchivoAdjunto`
* **Propósito:** Maneja la ubicación física de documentos (PDFs, imágenes corporativas).
* **Variables:** * `rutaServidor`: Ruta donde reside el archivo.
    * `tipoMime`: Formato para saber si es una imagen o un documento al abrirlo.

---

## 5. Lógica Transaccional y de Recomendación

### `Postulacion` (Clase Asociativa)
* **Relación:** Une a un `Estudiante` con una `OfertaLaboral`. 
* **Atributos:** * `fechaEnvio`: Registro de cuándo se aplicó.
    * `estadoProceso`: Rastrea el progreso del candidato (`RECIBIDA`, `REVISADA`, `FINALIZADA`).
    * `cartaPresentacion`: Texto personalizado enviado por el estudiante para esa vacante específica.

### `MotorDeRecomendacion`
* **Contexto:** Clase de servicio que ejecuta el algoritmo. No guarda datos permanentes, solo procesa información.
* **Relación:** Toma una `OfertaLaboral`, consulta la lista de estudiantes y genera objetos de tipo `Recomendacion`.

### `Recomendacion`
* **Propósito:** Es el resultado tangible del algoritmo. 
* **Atributos:** * `porcentajeMatch`: El número final de compatibilidad (ej: 85.5%).
    * `estudianteSugerido` / `ofertaAnalizada`: Punteros a las entidades originales que se compararon.

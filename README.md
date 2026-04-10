# Proyecto: Finis Trabaja
**Ingeniería de Software II - Entrega 1**

**Profesor:** Daniel Antonio Moreno Cordova  
**Contraparte:** [Dirección de Vinculación con el Medio, Universidad Finis Terrae](https://finis.cl/vinculacion-con-el-medio/)

---

## Equipo de Desarrollo

| Nombre | Correo | Rol Principal | Responsabilidad Documental |
|---|---|---|---|
| **Benjamín Loaiza** | bloaizay@uft.edu | Jefe de Proyecto y Diseño | Planificación metodológica, diagramas UML (casos de uso/clases) y coordinación general. |
| **Guido Guerrero** | gguerreror2@uft.edu | Frontend y UI/UX | Redacción de Requisitos de Usuario (RU), diseño de maquetas y documentación de interfaces. |
| **Miguel Obanos** | mobanosg@uft.edu | Arquitectura Backend y BD | Especificación técnica de los Requisitos del Sistema (RS), modelo de dominio y arquitectura. |
| **Eduardo Velasquez** | evelasquezg@uft.edu | Backend y Lógica de Negocio | Marco teórico, algoritmo de emparejamiento y redacción del plan de pruebas. |

---

## Introducción

### Contexto Operacional
En la Universidad Finis Terrae, el vínculo entre los alumnos y las vacantes laborales se gestiona a través de medios informales y poco estructurados, como correos masivos, carteles en el campus o grupos de mensajería. Si bien estos canales ayudan a difundir información, no garantizan que las ofertas lleguen a tiempo ni que logren llegar específicamente a los estudiantes que cumplen con el perfil buscado.

Esta situación perjudica tanto a estudiantes como empresas y departamentos de la universidad. Por una parte, los alumnos deben navegar por múltiples fuentes para encontrar una oportunidad, lo que consume mucho tiempo y los expone a datos irrelevantes o desactualizados. Además, las empresas tienen dificultades para contactar a los candidatos idóneos, lo que resta efectividad a sus búsquedas.

Las principales consecuencias de esto implican que los estudiantes corran el riesgo de perder ofertas valiosas y enfrenten procesos de búsqueda poco productivos. La universidad ve limitada su capacidad para impulsar la empleabilidad, mientras que las empresas deben invertir más recursos en reclutamiento sin asegurar resultados óptimos. Esto se traduce en una pérdida de tiempo y eficiencia para todos los involucrados.

### Problema a Solucionar
El propósito del sistema es abordar la falta de organización y eficiencia en el proceso de conexión entre estudiantes y oportunidades laborales dentro de la universidad. Actualmente, la información se encuentra dispersa y no existen herramientas que permitan gestionarla de manera estructurada ni facilitar su acceso según los intereses y perfiles de los usuarios.

En este contexto, se identifica la necesidad de contar con un sistema que permita centralizar y ordenar la información de las ofertas laborales, incorporando datos claros como el cargo, funciones, requisitos, modalidad de trabajo y rango de remuneración. Asimismo, se requiere que los estudiantes puedan crear perfiles más completos, donde incluyan su formación, intereses, habilidades y disponibilidad, manteniendo además control sobre la visibilidad de su información personal.

El sistema también debe facilitar la búsqueda y filtrado de ofertas, de manera que los estudiantes puedan acceder rápidamente a aquellas que sean relevantes para su perfil. A su vez, se espera mejorar la relación entre las características de las ofertas y los perfiles de los estudiantes, favoreciendo una mayor coherencia en el proceso de vinculación.

---

## Propósito y Propuesta de Solución

El objetivo central es superar las deficiencias comunicacionales actuales mediante la construcción de **Finis Trabaja**, una plataforma centralizada. Este sistema brindará a las empresas y unidades internas una herramienta estructurada para difundir sus vacantes de manera detallada. Paralelamente, permitirá a los alumnos exponer sus habilidades e intereses a través de un perfil digital. 

La principal innovación que se implementará será un algoritmo de emparejamiento que analizará automáticamente la compatibilidad entre los requerimientos del cargo y los datos del estudiante, facilitando un proceso de selección mucho más preciso. 

### Objetivo General

> Desarrollar e implementar una plataforma web centralizada **(Finis Trabaja)**, para modernizar y optimizar el proceso de vinculación laboral en la Universidad Finis Terrae, facilitando el encuentro eficiente entre las necesidades de las entidades empleadoras y las expectativas profesionales de los estudiantes, mediante la gestión de perfiles estructurados y un motor de recomendación algorítmica.

### Objetivos Específicos

* **Definir las especificaciones del sistema:** Establecer las restricciones funcionales, reglas de negocio y atributos de calidad bajo el estándar IEEE 29148 para garantizar que la solución satisfaga las necesidades de la universidad, las empresas y los estudiantes.
* **Estructurar la arquitectura lógica del proyecto:** Formular el modelo de dominio y la base arquitectónica que guiarán la implementación técnica, asegurando la trazabilidad desde el problema hasta el código.
* **Centralizar la gestión de oportunidades y perfiles:** Proveer un entorno digital unificado que permita a las empresas publicar vacantes detalladas y a los estudiantes autogestionar su Currículum Vitae Virtual (CVV).
* **Automatizar el emparejamiento laboral:** Incorporar un mecanismo de recomendación algorítmica que evalúe, filtre y ordene a los candidatos de forma automática según su grado de compatibilidad con cada oferta específica.
* **Asegurar la viabilidad técnica y operativa:** Comprobar el correcto funcionamiento de los flujos de postulación, la seguridad de los perfiles y el cumplimiento de los requisitos mediante la aplicación de un plan sistemático de pruebas.

---

## Marco Teórico

### LinkedIn
Red social orientada al uso empresarial y al empleo. Su sistema de emparejamiento se basa en un enfoque híbrido:
* **Filtrado Basado en Contenido (Content-Based Filtering):** Análisis de afinidad mediante Procesamiento de Lenguaje Natural (NLP) para extraer entidades clave.
* **Modelos de Aprendizaje Automático:** Utiliza la similitud de coseno y modelos de clasificación (*Learning to Rank*) para ordenar candidatos.
* **Retroalimentación (Implicit Feedback):** El algoritmo ajusta sugerencias en tiempo real basado en las interacciones del usuario (ej: clics, ofertas ignoradas).

### FirstJob
Plataforma HR Tech enfocada en talento joven. Elimina las barreras de entrada priorizando el potencial sobre la experiencia histórica:
* **Emparejamiento por Potencial:** Segmentación por carrera y avance curricular, filtrando ofertas para perfiles específicos (ej: prácticas vs. primer empleo).
* **Employer Branding:** Integra reputación corporativa para asegurar que las ofertas sean seguras y formativas.

### Tasky
Plataforma de la *Gig Economy* enfocada en micro-trabajo y resolución de tareas específicas de corta duración:
* **Emparejamiento Dinámico:** Prioriza la geolocalización y la disponibilidad inmediata.
* **Sistema de Reputación:** Ranking bilateral fuertemente influenciado por reseñas y tasas de finalización.
* **Micro-segmentación:** Utiliza etiquetas de habilidades muy precisas, ideal para trabajos part-time u oficios específicos.

---

## Borrador de Requisitos (IEEE 29148)

### REQ-01: Gestión de Ofertas Laborales
* **Requisito de Usuario (RU-01):** La empresa necesita publicar vacantes de trabajo detalladas e incluir material corporativo para captar el interés de los estudiantes universitarios.
* **Requisitos de Sistema Funcionales (RS-F):**
  * **RS-F01.1:** El **[usuario empresa validada]** debe poder **[crear y publicar una oferta laboral indicando cargo, sueldo y carrera]** dentro del **[módulo de gestión de vacantes]**.
  * **RS-F01.2:** El **[usuario empresa validada]** debe poder **[adjuntar archivos multimedia]** durante el **[proceso de creación de la oferta]**.
* **Requisitos de Dominio (RD):**
  * **RD-01.1:** Toda oferta laboral orientada a modalidad de "Práctica" debe cumplir y mostrar las **[normativas de prácticas profesionales vigentes de la Universidad Finis Terrae]**.
* **Requisitos No Funcionales (FURPS):**
  * **RN-01.1 (Usability):** La interfaz debe mantener consistencia visual y aplicar factores humanos para evitar errores de digitación en los montos de sueldo.
  * **RN-01.2 (Performance):** El sistema debe procesar la carga de archivos adjuntos sin bloquear el hilo principal de la aplicación.
* **Prueba de Requisito:**

| Escala | Medida | Mínimo | Máximo |
|---|---|---|---|
| Ratio (Tiempo) | Segundos requeridos para publicar oferta estándar. | 30s (deseable) | 180s (aceptable) |

### REQ-02: Creación de Perfil Profesional (CVV)
* **Requisito de Usuario (RU-02):** El estudiante necesita autogestionar su perfil profesional y controlar quién puede ver su información para proteger su privacidad.
* **Requisitos de Sistema Funcionales (RS-F):**
  * **RS-F02.1:** El **[usuario estudiante]** debe poder **[registrar sus datos académicos y preferencias laborales]** en la **[vista de configuración del CVV]**.
  * **RS-F02.2:** El **[usuario estudiante]** debe poder **[modificar el estado de visibilidad de su perfil a "Público", "Privado" o "Solo Universidad"]** desde el **[panel de privacidad]**.
* **Requisitos No Funcionales (FURPS):**
  * **RN-02.1 (Security):** Los datos personales sensibles deben estar encriptados en la base de datos.
  * **RN-02.2 (Reliability):** El sistema debe asegurar la exactitud de los datos guardados, previniendo la corrupción de información del perfil.
* **Prueba de Requisito:**

| Escala | Medida | Mínimo/Máximo |
|---|---|---|
| Nominal | Estado de configuración de privacidad del perfil. | 0 fallos al intentar acceder a un perfil "Privado" por un agente externo. |

### REQ-03: Emparejamiento Algorítmico y Postulación
* **Requisito de Usuario (RU-03):** La plataforma debe sugerir estudiantes idóneos para una vacante y permitirles aplicar con un solo clic.
* **Requisitos de Sistema Funcionales (RS-F):**
  * **RS-F03.1:** El **[sistema de recomendación]** debe **[generar un listado de estudiantes ordenados por porcentaje de compatibilidad]** cuando **[se publica o consulta una oferta]**.
  * **RS-F03.2:** El **[usuario estudiante]** debe poder **[confirmar su postulación adjuntando automáticamente su CVV]** en la **[vista de detalle de la vacante recomendada]**.
* **Requisitos No Funcionales (FURPS):**
  * **RN-03.1 (Performance):** El tiempo de respuesta del algoritmo de emparejamiento debe ser casi instantáneo.
  * **RN-03.2 (Testability):** El código del algoritmo debe estar construido de forma modular para permitir pruebas unitarias.
* **Prueba de Requisito (asociada a RN-03.1):**

| Escala | Medida | Mínimo | Máximo |
|---|---|---|---|
| Ratio (Tiempo) | Tiempo de respuesta del servidor (ms). | 100 ms | 2000 ms |

---

## Definiciones y Acrónimos

* **CVV:** Currículum Vitae Virtual.
* **IEEE:** *Institute of Electrical and Electronics Engineers*.
* **IEEE 29148:** Estándar internacional conjunto (ISO/IEC/IEEE) que especifica los procesos y productos para la ingeniería de requisitos en sistemas y software.

---

## Referencias

1. ISO/IEC/IEEE. (2018). *ISO/IEC/IEEE International Standard - Systems and software engineering -- Life cycle processes -- Requirements engineering (IEEE 29148-2018)*. Ginebra, Suiza.
2. Kenthapadi, K., Le, Q., & Ganesh, G. (2017). *Personalized job recommendation system at LinkedIn*. [Enlace a PDF](http://www-cs-students.stanford.edu/~kngk/papers/personalizedJobRecommendationSystemAtLinkedIn-RecSys2017.pdf)
3. FirstJob Research. (2024). *Employers for Youth (EFY) Chile*. [Sitio Web](https://www.efy.global/)
4. De Stefano, V. (2016). *The rise of the "just-in-time workforce": On-demand work, crowdwork, and labor protection in the "gig-economy"*. [Sitio Web](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2682602)

# Finis Trabaja

Repositorio para registrar progreso y participación en proyecto semestral de Ingeniería de Software 2.







### Contexto Operacional

En la universidad Finis Terrae, el vínculo entre lo alumnos y las vacantes laborales se gestiona a través de medios informales y poco estructurados, como correos masivos, carteles en el campus o grupos de mensajería. Si bien estos canales ayudan a difundir información, no garantizan que las ofertas lleguen a tiempo ni que logren llegar específicamente a los estudiantes que cumplen con el perfil buscado.

Esta situación perjudica tanto a estudiantes como empresas y departamentos de la universidad. Por una parte, los alumnos deben navegar por múltiples fuentes para encontrar una oportunidad, lo que consume mucho tiempo y los expone a datos irrelevantes o desactualizados. Además, las empresas tienen dificultades para contactar a los candidatos idóneos, lo que resta efectividad a sus búsquedas.

Las principales consecuencias de esto implica que los estudiantes corran el riesgo de perder ofertas valiosas y enfrenten procesos de búsquedas poco productivas. La universidad ve limitada su capacidad para impulsar la empleabilidad, mientras que las empresas deben invertir más recursos en reclutamiento sin asegurar resultados óptimo. Esto se traduce en una perdida de tiempo y eficiencia para todos los involucrados.

### Problema a solucionar

El propósito del sistema es abordar la falta de organización y eficiencia en el proceso de conexión entre estudiantes y oportunidades laborales dentro de la universidad. Actualmente, la información se encuentra dispersa y no existen herramientas que permitan gestionarla de manera estructurada ni facilitar su acceso según los intereses y perfiles de los usuarios.

En este contexto, se identifica la necesidad de contar con un sistema que permita centralizar y ordenar la información de las ofertas laborales, incorporando datos claros como el cargo, funciones, requisitos, modalidad de trabajo y rango de remuneración. Asimismo, se requiere que los estudiantes puedan crear perfiles mas completos, donde incluyan su formación, intereses, habilidades y disponibilidad, manteniendo además control sobre visibilidad de su información personal.

El sistema también debe facilitar la búsqueda y filtrado de ofertas, de manera que los estudiantes puedan acceder rápidamente a aquellas que sean relevantes para su perfil. A su vez, se espera mejorar la relación entre las características de las ofertas y los perfiles de los estudiantes, favoreciendo una mayor coherencia en el proceso de vinculación. 

### Objetivo general
Desarrollar e implementar una plataforma web centralizada **(Finis Trabaja)**, para modernizar y optimizar el proceso de vinculación laboral en la Universidad Finis Terrae, facilitando el encuentro eficiente entre las necesidades de las entidades empleadoras y las expectativas profesionales de los estudiantes, mediante la gestión de perfiles estructurados y un motor de recomendación algorítmica.

### Objetivos específicos

* **Definir las especificaciones del sistema:** Establecer las restricciones funcionales, reglas de negocio y atributos de calidad bajo el estándar IEEE 29148 para garantizar que la solución satisfaga las necesidades de la universidad, las empresas y los estudiantes.
* **Estructurar la arquitectura lógica del proyecto:** Formular el modelo de dominio y la base arquitectónica que guiarán la implementación técnica, asegurando la trazabilidad desde el problema hasta el código.
* **Centralizar la gestión de oportunidades y perfiles:** Proveer un entorno digital unificado que permita a las empresas publicar vacantes detalladas y a los estudiantes autogestionar su Currículum Vitae Virtual (CVV).
* **Automatizar el emparejamiento laboral:** Incorporar un mecanismo de recomendación algorítmica que evalúe, filtre y ordene a los candidatos de forma automática según su grado de compatibilidad con cada oferta específica.
* **Asegurar la viabilidad técnica y operativa:** Comprobar el correcto funcionamiento de los flujos de postulación, la seguridad de los perfiles y el cumplimiento de los requisitos mediante la aplicación de un plan sistemático de pruebas.

---

## Marco Teórico

### LinkedIn

***LinkedIn*** es una red social orientada al uso empresarial, a los negocios y al empleo. Fundada en 2002, su arquitectura está diseñada para conectar a profesionales, empresas y buscadores de empleo mediante la creación de una identidad digital profesional.

El sistema de emparejamiento de ***LinkedIn*** no se basa en una única técnica, sino en un enfoque híbrido que combina el análisis de datos estructurados y no estructurados para conectar candidatos con vacantes de manera eficiente.

#### Filtrado Basado en Contenido (Content-Based Filtering)
La base del sistema es el análisis de la afinidad entre el perfil del usuario (habilidades, educación, títulos de cargos anteriores) y la descripción del puesto de trabajo. ***LinkedIn*** utiliza técnicas de Procesamiento de Lenguaje Natural (NLP) para extraer entidades y conceptos clave, permitiendo que el sistema entienda que un "Desarrollador de Software" y un "Ingeniero de Sistemas" pueden ser perfiles compatibles aunque utilicen términos distintos.

#### Modelos de Aprendizaje Automático y Grafos
A diferencia de los portales de empleo tradicionales, ***LinkedIn*** aprovecha el "Economic Graph", una representación digital de la economía global que incluye datos sobre empresas, empleos y habilidades. El emparejamiento se realiza mediante:

* **Similitud de Coseno:** Para medir la distancia vectorial entre las competencias del candidato y los requisitos de la oferta.
* **Modelos de Clasificación (Learning to Rank):** El sistema no solo encuentra coincidencias, sino que ordena a los candidatos según la probabilidad de que la empresa los contrate y de que el candidato acepte la oferta.

#### El Rol de la Retroalimentación (Implicit Feedback)
El sistema de emparejamiento aprende constantemente de las interacciones. Si un usuario ignora ciertas recomendaciones o hace clic en otras, el algoritmo ajusta el peso de variables como el sueldo pretencioso, la ubicación geográfica y la modalidad de trabajo (presencial/remoto), optimizando las futuras sugerencias en tiempo real.


### FirstJob
***FirstJob*** es una plataforma de tecnología de recursos humanos (HR Tech) nacida en Chile, líder en Latinoamérica en la conexión entre estudiantes de educación superior y el mundo laboral. Su enfoque principal es eliminar las barreras de entrada para quienes no poseen experiencia previa.

#### Sistema de Emparejamiento Basado en Potencial
A diferencia de los sistemas tradicionales que priorizan la experiencia laboral histórica, el sistema de ***FirstJob*** utiliza un modelo de matching por competencias y afinidad académica:

* **Segmentación por Carrera y Semestre:** Filtra ofertas según el avance curricular del estudiante, asegurando que un alumno de cuarto año vea oportunidades distintas a uno recién egresado.
* **Filtros de Interés Específico:** Permite el emparejamiento basado en la modalidad (práctica profesional, primer empleo o trabajo Part-Time).

#### Employer Branding y Validación de Empresas
***FirstJob*** integra un componente de reputación corporativa (como el ranking *Employers for Youth*). En términos teóricos, la plataforma actúa como un filtro de calidad para asegurar que las ofertas sean seguras y formativas para los estudiantes.


### Tasky

***Tasky*** es un referente del modelo de Gig Economy y plataformas de trabajo bajo demanda (On-Demand Work). A diferencia de los portales de empleo tradicionales, ***Tasky*** se especializa en el "micro-trabajo" o la resolución de tareas específicas y de corta duración (denominadas gigs) que requieren una vinculación inmediata entre quien tiene una necesidad y quien tiene la habilidad para resolverla.

***Tasky*** basa su éxito en la reducción de la fricción entre la necesidad de un cliente y la disponibilidad de un prestador de servicios. Presenta las siguientes características:

#### Sistema de Emparejamiento
El sistema de matching de ***Tasky*** no solo analiza el "perfil" (como LinkedIn), sino variables dinámicas:

* **Geolocalización (Location-Based Matching):** Prioriza la cercanía física entre el oferente y el demandante para optimizar tiempos de respuesta.
* **Sistema de Reputación Bilateral:** El emparejamiento está fuertemente influenciado por el "rating" y los comentarios. Los algoritmos de ranking posicionan mejor a los usuarios con mayores tasas de finalización de tareas y mejores reseñas.
* **Matching Basado en Disponibilidad Real:** A diferencia de un portal de empleo donde la vacante puede estar abierta semanas, ***Tasky*** utiliza un sistema de "disponibilidad inmediata", similar a lo que tu proyecto podría requerir para trabajos part-time o de apoyo en eventos universitarios.

#### Micro-segmentación de Habilidades
***Tasky*** utiliza etiquetas de habilidades muy específicas (ej: "montaje de stands", "transcripción de textos", "soporte técnico básico"). Esto permite un emparejamiento de alta precisión para tareas que no requieren un título profesional completo, sino una competencia técnica puntual.

---

### Referencias

* **ISO/IEC/IEEE. (2018).** *ISO/IEC/IEEE International Standard - Systems and software engineering -- Life cycle processes -- Requirements engineering* (IEEE 29148-2018). Ginebra, Suiza: International Organization for Standardization.
* **Kenthapadi, K., Le, Q., & Ganesh, G. (2017).** *Personalized job recommendation system at LinkedIn*. En Proceedings of the 11th ACM Conference on Recommender Systems (RecSys). [http://www-cs-students.stanford.edu/~kngk/papers/personalizedJobRecommendationSystemAtLinkedIn-RecSys2017.pdf](http://www-cs-students.stanford.edu/~kngk/papers/personalizedJobRecommendationSystemAtLinkedIn-RecSys2017.pdf)
* **FirstJob Research. (2024).** *Employers for Youth (EFY) Chile: Tendencias en la contratación de talento joven*. [https://www.efy.global/](https://www.efy.global/)
* **De Stefano, V. (2016).** *The rise of the "just-in-time workforce": On-demand work, crowdwork, and labor protection in the "gig-economy"*. International Labour Office. [https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2682602](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2682602)


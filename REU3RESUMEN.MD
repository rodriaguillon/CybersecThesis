# Diseño de un Cyber Range Educativo para Análisis Forense Digital y Gestión de Incidentes

## Conceptos Fundamentales en Análisis Forense Digital y Gestión de Incidentes  

### Análisis forense digital  
- **Definición**: El uso de técnicas científicamente comprobadas para recolectar, fusionar, identificar, examinar, correlacionar, analizar y documentar evidencia digital proveniente de múltiples fuentes digitales que están procesando y transmitiendo activamente información, con el propósito de descubrir hechos relacionados con la intención planificada o el éxito medido de actividades no autorizadas destinadas a interrumpir, corromper o comprometer componentes del sistema, así como también de proporcionar información que asista en la respuesta o recuperación ante estas actividades. [5](#referencias)

- **Cadena de custodia**: Procedimiento formal para documentar cómo se recopilan, transfieren y almacenan las evidencias. Garantiza que la evidencia digital no sea manipulada y pueda usarse con validez legal. [6](#referencias)
- **Fuentes de evidencia**: Datos extraídos de sistemas de archivos (archivos en discos/endpoints), memoria RAM, tráfico de red (p.ej. capturas PCAP, registros de comunicaciones) y registros de aplicaciones, entre otros. Es crucial obtener copias forenses (imágenes bit a bit) de estos datos para preservar los originales. [6](#referencias)

- **Fases del análisis forense** (según NIST):

1. **Recopilación de datos**  
   Esta fase implica la adquisición segura de todas las evidencias digitales relevantes relacionadas con un incidente. Se prioriza la recolección siguiendo el **principio de volatilidad**: primero los datos más efímeros (memoria RAM, conexiones activas), luego los datos persistentes (discos, backups).  
   - El objetivo es preservar la integridad de la evidencia, garantizando que los originales no sean alterados en el proceso.
   - Se utilizan herramientas de adquisición forense certificadas que permiten generar copias bit a bit de dispositivos de almacenamiento y capturar imágenes de memoria.
   - Es fundamental documentar toda acción realizada sobre las evidencias para verificar que se esté manteniendo la  `cadena de custodia`.

2. **Examinar**  
   Una vez recolectados los datos, se realiza un primer análisis estructurado de los mismos para identificar posibles indicadores de compromiso (IoCs).  
   - Esta etapa implica **filtrar la información irrelevante** para enfocar el esfuerzo en artefactos que podrían revelar actividades maliciosas.
   - Ejemplos de análisis preliminar incluyen la búsqueda de:
     - Correos electrónicos de phishing.
     - Archivos alterados o inesperados.
     - Conexiones de red no autorizadas.
     - Modificaciones sospechosas en el registro de Windows o sistemas de archivos.
   - Se deben aplicar técnicas de hashing para verificar la integridad de los archivos recolectados.

3. **Análisis**  
   Es la fase más profunda, donde se correlaciona toda la información relevante para **reconstruir la narrativa completa del incidente**.  
   - Se busca responder preguntas clave:
     - ¿Cómo ocurrió el ataque? (vector de entrada).
     - ¿Qué vulnerabilidades fueron explotadas?
     - ¿Qué sistemas fueron comprometidos?
     - ¿Qué acciones realizó el atacante (movimiento lateral, exfiltración de datos, instalación de malware)?
     - ¿Qué información fue robada o alterada?
   - Se reconstruyen **líneas de tiempo forenses** a partir de metadatos, logs de eventos y huellas dejadas por el atacante.
   - Se pueden utilizar herramientas específicas para análisis de malware, análisis de tráfico de red, o correlación de eventos múltiples.
   - En algunos casos, se integran fuentes de **inteligencia de amenazas** (threat intelligence) para atribuir la actividad a grupos conocidos.

4. **Informe**  
   El análisis culmina en la elaboración de un **informe forense** detallado, que debe ser claro, estructurado y técnicamente sólido.  
   - El informe incluye:
     - Descripción del incidente y línea de tiempo reconstruida.
     - Evidencias halladas y su interpretación.
     - Impacto en los sistemas afectados.
     - Vulnerabilidades explotadas y debilidades identificadas.
     - Recomendaciones para prevenir incidentes similares en el futuro.
   - Además, se debe:
     - Explicar el proceso metodológico seguido (para asegurar reproducibilidad).
     - Evitar tecnicismos innecesarios si el informe será presentado ante audiencias no técnicas (ej.: alta dirección, abogados).
   - El informe puede ser utilizado como evidencia en procedimientos legales o auditorías regulatorias, por lo que su **precisión y formalismo** son fundamentales.

---
### Respuesta a incidentes (gestión de incidentes)  

- **Definición**: Conjunto de procedimientos y prácticas para detectar, contener y responder a incidentes de seguridad, minimizando su impacto. Su objetivo es **detener el ataque rápidamente, reducir el daño, recuperar sistemas** y aprender del evento. Una respuesta eficaz combina medidas técnicas y organizativas (comunicación, reporting, mejoras).  
- **Plan de respuesta**: Las organizaciones deben contar con un **plan de respuesta a incidentes (IRP)** que establezca pasos, roles y responsabilidades cuando ocurre una brecha de seguridad.
- **Fases del manejo de incidentes**:
 1. **Preparación** 
Uno de los componentes más críticos de la fase de preparación consiste en la elaboración de un Plan de Respuesta a Incidentes (IRP). Una vez que dicho plan se encuentra desarrollado e implementado, resulta esencial garantizar que el personal involucrado en tareas de respuesta a incidentes esté debidamente capacitado y cuente con una comprensión detallada y práctica de los procesos y procedimientos establecidos. Esta capacitación debe abarcar tanto los aspectos metodológicos como el uso de herramientas adicionales necesarias para llevar a cabo investigaciones forenses de manera efectiva.
Además de la formalización del plan, es indispensable la adquisición e integración de equipamiento especializado, incluyendo hardware forense y software de análisis, dentro del esquema general de preparación. Estos recursos deben estar disponibles y actualizados para ser utilizados de inmediato ante la ocurrencia de un incidente.
Por último, es fundamental que la organización lleve a cabo ejercicios de simulación de incidentes de forma periódica. Estas prácticas permiten evaluar la eficacia del plan, reforzar la familiaridad del personal con los procedimientos, identificar oportunidades de mejora, y asegurar que, llegado el momento, la respuesta se realice de forma ágil, coordinada y eficiente [1](#referencias).

2. **Detección**
Es el momento en que la organización identifica indicios de actividad maliciosa. Puede originarse en alertas de seguridad, reportes de usuarios o notificaciones externas (por ejemplo, de un ISP o de autoridades). El desafío principal es filtrar señales reales de una gran cantidad de eventos legítimos [1](#referencias).

3. **Análisis**
Una vez detectado un incidente, se recolecta evidencia (memoria, logs, conexiones de red) para reconstruir lo sucedido. Una vez que la información es recolectada, debe ser examinada. El objetivo principal del análisis es determinar la causa raíz del incidente y reconstruir las acciones que llevaron al actor maligno inicialmente a comprometer el sistema hasta su detección posterior [1](#referencias).

4. **Contención**
En esta fase, las organizaciones toman medidas para limitar las posibilidades que tiene el actor maligno de poder comprometer otras redes de tráfico, comunicarse mediante comandos y controlar las infraestructuras, o filtrando información confidencial. Las estrategias de contención pueden ir desde bloqueo de puertos e IPs en un firewall hasta simplemente quitar el cable de red de una máquina infectada [1](#referencias).

5. **Erradicación y Recuperación**
Durante la fase de erradicación, la organización quita al actor maligno de la red comprometida. En el caso de una infección mediante malware, la organización ejecuta soluciones anti-malware mejoradas. En otro caso, las máquinas son limpiadas y se rehacen sus imágenes. Otras actividades pueden incluir quitar o cambiar las cuentas de usuario comprometidas. Si una organización encuentra vulnerabilidades que están siendo explotadas, se aplican parches, o software updates correspondientemente. 
En esta fase del proceso, las organizaciones reinstalan con nuevos sistemas opertativos o aplicaciones. También restauran información en los sistemas locales desde sus backups. Como medida de diligencia, las organizaciones también auditarán sus cuentas de usuario y administrador existentes para garantizar que no haya cuentas que hayan sido habilitadas por actores malignos. Finalmente, un comprensivo análisis de vulnerabilidades es llevado a cabo para que la organización esté segura que cualquier vulnerabilidad que fue explotada previamente ya no existe más actualmente [1](#referencias).

6. **Post-Incident Activity**
Una revisión exhaustiva de lo sucedido, evaluando qué medidas funcionaron y cuáles no. Se documenta todo el proceso, se identifican mejoras para fortalecer la postura de seguridad, y se preparan reportes claros para públicos técnicos y no técnicos [1](#referencias).


# Componentes Fundamentales de un Incident Response Plan (IRP)

Un **Incident Response Plan (IRP)** es un documento formal, aprobado a nivel ejecutivo, que guía a una organización antes, durante y después de un incidente de ciberseguridad. Su objetivo es **clarificar roles y responsabilidades**, **organizar las comunicaciones** y **establecer protocolos de actuación** frente a incidentes confirmados o sospechados.

Según las guías de **CISA** y **NIST**, los elementos esenciales de un IRP incluyen [13](#referencias):

## Antes de un incidente

- **Entrenamiento de Personal**: Todos los miembros deben conocer su rol en la seguridad de la organización y saber cómo reportar incidentes sospechosos.
- **Revisión Legal**: El IRP debe ser revisado por un asesor legal para asegurar que se alinea a las mejores prácticas legales y regulatorias.
- **Contactos Estratégicos**: Establecer relaciones previas con CISA, agencias de aplicación de la ley (LEA), y otros stakeholders clave.
- **Impresión Física de Documentos**: Asegurar la disponibilidad de copias impresas del IRP y de las listas de contactos en caso de interrupción digital.
- **Planificación de Roles y Comunicación**: Definir claramente qué personas deben ser notificadas durante un incidente (por ejemplo, directores, inversores, socios estratégicos).
- **Revisión Periódica**: El IRP debe ser revisado al menos trimestralmente para asegurar su vigencia.
- **Preparación de Comunicaciones Públicas**: Disponer de comunicados preventivos para responder a consultas de prensa.
- **Selección de Proveedores Técnicos Externos**: Anticipar quiénes serán los investigadores externos si se requiere asistencia.
- **Simulaciones de Incidentes (Tabletop Exercises)**: Realizar ejercicios prácticos de simulación para evaluar la preparación organizacional.

## Durante un incidente

- **Asignación de Roles Críticos**:
  - **Incident Manager (IM)**: Responsable de coordinar la respuesta, sin realizar tareas técnicas. El IM debe asegurarse de que las acciones se ejecuten sin que el "time dilation" (percepción distorsionada del tiempo en crisis) afecte el ritmo de respuesta.
  - **Technical Manager (TM)**: Experto técnico que lidera la investigación y la ejecución de medidas técnicas.
  - **Communications Manager (CM)**: Encargado de la interacción con medios de comunicación, stakeholders externos y redes sociales.

## Después del incidente

- **Reunión Retrospectiva Formal**:
  - Reconstrucción de la **línea de tiempo** del incidente.
  - Discusión abierta, **sin culpas individuales** ("blameless post-mortem").
  - Análisis de fallas en personas, procesos y tecnologías.
- **Actualización de Políticas y Procedimientos**: Incorporar las lecciones aprendidas en el IRP y en las prácticas de seguridad.
- **Comunicación Interna de Resultados**: Informar a todo el personal sobre el incidente, reforzando la cultura de seguridad organizacional

--- 

# Los Tres Grandes Enfoques del Análisis Forense Digital

Durante el análisis forense de incidentes, existen tres categorías principales de aproximación al estudio de la forensia digital, cada una enfocándose en distintos tipos de datos y técnicas [5](#referencias) [6](#referencias):

## 1. Media Analysis (Análisis de Medios)

El **Media Analysis** implica examinar el **medio físico** en el que se almacenan los datos (por ejemplo: discos duros, memorias USB, discos SSD, cintas de backup).

- **Objetivo**: Encontrar evidencia de actividad maliciosa o no autorizada directamente en los dispositivos de almacenamiento.
- **Tareas típicas**:
  - Recuperar archivos eliminados.
  - Identificar particiones ocultas o sistemas de archivos anómalos.
  - Analizar los metadatos de archivos para entender modificaciones y accesos.
  - Buscar artefactos forenses como logs de navegación, historial de ejecución de programas, entre otros.
- **Desafíos**:
  - Limitaciones de herramientas que muchas veces están diseñadas para sistemas operativos específicos (ej., Windows vs Linux).
  - Dificultades para interpretar medios cifrados o dañados.
  - Escalabilidad ante discos de gran tamaño y múltiples formatos de archivos.

## 2. Code Analysis (Análisis de Código)

El **Code Analysis** se centra en **examinar programas y software sospechoso** para identificar comportamiento malicioso.

- **Objetivo**: Entender si un archivo ejecutable, script o aplicación contiene componentes maliciosos y cómo opera.
- **Tareas típicas**:
  - Análisis estático: inspeccionar el código fuente o el binario sin ejecutarlo, buscando firmas conocidas de malware o patrones sospechosos.
  - Análisis dinámico: ejecutar el programa en un entorno controlado (sandbox) para observar su comportamiento (como conexiones salientes, modificaciones en el sistema, etc.).
  - Ingeniería inversa de binarios maliciosos para extraer payloads, identificar C2 (Command & Control servers) o encontrar vulnerabilidades explotadas.
- **Desafíos**:
  - Los atacantes pueden usar técnicas de ofuscación, cifrado o empaquetado de código para dificultar el análisis.
  - Alta especialización: requiere conocimientos profundos de arquitectura de sistemas, programación y técnicas de reversing.

## 3. Network Analysis (Análisis de Red)

El **Network Analysis** se enfoca en el **tráfico de red** y en los **registros de comunicaciones** para detectar actividades sospechosas o maliciosas.

- **Objetivo**: Identificar intrusiones, comunicaciones con servidores maliciosos, movimientos laterales y exfiltración de datos.
- **Tareas típicas**:
  - Capturar y analizar paquetes de red (por ejemplo, usando Wireshark o Zeek).
  - Inspeccionar registros de firewall, proxies, VPNs y sistemas IDS/IPS.
  - Identificar patrones anómalos de tráfico (volumen inusual, protocolos sospechosos, conexiones a IPs o dominios peligrosos).
  - Reconstruir sesiones de ataque o exfiltraciones de información.
- **Desafíos**:
  - Gran volumen de datos que deben ser procesados y filtrados rápidamente.
  - Encriptación del tráfico (por ejemplo, HTTPS) que limita la visibilidad.
  - Necesidad de sincronizar registros entre múltiples fuentes para reconstruir actividades.

# Propuesta para abordar: Catalogar grandes áreas de respuesta a incidentes forenses y mapear habilidades y procesos

## 1. Definir las **Grandes Áreas** del Análisis Forense de Incidentes

| Área principal | Descripción resumida | Ejemplo de tareas |
|:---------------|:---------------------|:------------------|
| **Recopilación de Datos** | Adquirir de manera segura toda la evidencia digital relevante, priorizando según la volatilidad de los datos. | Capturar imágenes de memoria RAM, hacer copias forenses bit a bit de discos, recolectar tráfico de red, asegurar cadena de custodia. |
| **Examen** | Filtrar y organizar los datos recolectados para identificar elementos relevantes que puedan indicar compromiso. | Buscar archivos alterados, conexiones sospechosas, correos maliciosos, eventos anómalos en logs, verificar integridad con hashes. |
| **Análisis** | Correlacionar la información para reconstruir la narrativa completa del incidente. | Reconstruir líneas de tiempo, identificar vectores de ataque, determinar movimientos del atacante, analizar malware o tráfico de red. |
| **Informe** | Documentar el proceso y los hallazgos en un informe formal técnico-legal, asegurando claridad, precisión y trazabilidad. | Redactar un informe estructurado, explicar el proceso seguido, describir hallazgos, impactos, y realizar recomendaciones. |

---

## 2. Catalogar las **Habilidades** necesarias en cada Área

| Área | Habilidades clave |
|:-----|:-----------------|
| **Recopilación de Datos** | Aplicar técnicas de adquisición forense de memoria y disco respetando cadena de custodia. Manejar herramientas certificadas. Priorizar adquisición según principio de volatilidad. |
| **Examen** | Filtrar datos irrelevantes. Identificar artefactos sospechosos (IoCs). Analizar eventos en registros de sistemas, tráfico de red y sistemas de archivos. Verificar integridad de evidencias con hashing. |
| **Análisis** | Correlacionar múltiples fuentes de evidencia. Reconstruir cronologías de ataque. Detectar técnicas de movimiento lateral y exfiltración. Integrar información de inteligencia de amenazas si aplica. |
| **Informe** | Redactar informes claros, reproducibles y técnicamente sólidos. Estructurar líneas de tiempo de incidentes. Adaptar el nivel técnico del reporte según audiencia (técnica, gerencial, legal). Garantizar precisión y formalismo. |

## Escenarios de los cyber range

Consideramos un posible escenario en el cual, para evaluar el desempeño del estudiante en sus tareas de análisis Blue Team, se le solicite reconstruir, en la medida de sus capacidades, una línea de tiempo completa del ataque. Esta reconstrucción debe abarcar el vector de entrada, las acciones realizadas por el atacante dentro de la infraestructura y los datos comprometidos durante el incidente.

La calidad y profundidad de esta línea de tiempo formarán parte integral de la documentación final de hallazgos elaborada por el estudiante.
En este contexto, la cantidad y precisión de los elementos identificados que pueden ser aquellos tales como eventos, compromisos, movimientos laterales, persistencias y exfiltraciones, que constituirán criterios objetivos de evaluación para puntuar el desempeño en el laboratorio.

De esta manera, se fomenta una evaluación que no solo considera la detección puntual de incidentes, sino también la capacidad analítica integral del estudiante para reconstruir, entender y documentar el ciclo completo del ataque.

La justificación de esta forma de evaluación puede venir dada por el mero hecho de que promueve un aprendizaje profundo y significativo: el estudiante no solo debe identificar hechos aislados, sino también comprender su secuencia, causalidad y contexto técnico. Esto obliga a integrar conocimientos de adquisición forense, análisis de logs, tráfico de red y comportamiento de sistemas, consolidando las habilidades prácticas esenciales en DFIR.

Cada escenario debe contar con **métricas de éxito claras**: Es buena idea asignar **banderas (_flags_) únicas por grupo** en el escenario final u otros, para fomentar la competencia sana y evitar que simplemente copien respuestas. Por ejemplo, se puede ocultar un hash o string único en un archivo de cada entorno que solo descubren si completan el análisis; de esta manera cada grupo reportará un flag distinto.

## Uso de Tectonic para Crear, Personalizar y Monitorear Escenarios  
La plataforma **Tectonic** será la base del cyber range. Tectonic es un cyber range académico de código abierto desarrollado por la Universidad de la República (Uruguay) que permite desplegar **escenarios de ciberseguridad personalizados** mediante virtualización, con capacidades de **monitoreo en tiempo real y simulación automatizada de ataques**.

<!-- - **Infraestructura como Código (IaC)**: Tectonic emplea un enfoque declarativo para describir los escenarios. Cada laboratorio se define mediante archivos de configuración, principalmente un archivo YAML que especifica la **topología de red, máquinas virtuales, imágenes de base, redes y servicios** del escenario. Esta descripción de alto nivel es **interpretada automáticamente** por Tectonic, que utiliza herramientas IaC subyacentes (Terraform, Packer, etc.) para crear las VMs y la red según el diseño. La ventaja de este enfoque es que los escenarios son **versionables, reutilizables y compartibles** fácilmente entre instructores e instituciones. Por ejemplo, podríamos tener un archivo `escenario_ransomware.yaml` que define 1 VM atacante (Kali Linux), 3 VMs víctimas (Windows Server, Windows 10, Linux) en una red interna, y un servidor de logística (por si simulamos un dominio AD). Este archivo describe recursos (CPU, RAM), redes (segmento interno, segmento externo), etc., todo lo necesario para levantar el entorno completo de laboratorio de forma reproducible. 

- **Personalización con Ansible**: Para configurar el contenido dentro de las máquinas (usuarios, archivos, configuración de software, etc.), Tectonic integra **playbooks de Ansible** como parte de la especificación del escenario. Se definen típicamente dos playbooks:
  - **`base_config.yml`**: se ejecuta al crear la imagen base de cada máquina (tiene Internet disponible). Aquí se instalan las herramientas necesarias en las VM (por ejemplo, utilidades forenses como `sleuthkit`, `Wireshark`, o incluso plantar cierto malware señuelo).  
  - **`after_clone.yml`**: se ejecuta después de clonar la máquina para cada instancia del lab (sin internet). Aquí se pueden realizar personalizaciones finales, como desplegar una *flag* específica, iniciar o programar servicios maliciosos (p.ej. lanzar un script de ataque simulado), crear cuentas de usuarios alumnos, etc. 

  Tectonic automáticamente genera el inventario Ansible con los hosts del escenario (agrupados por rol, p. ej. `attacker` o `victim`), de modo que el instructor puede escribir tareas apuntando a grupos lógicos. Por ejemplo, se puede tener en `after_clone.yml` algo como: *“en todas las máquinas `victim`, copiar el archivo `evidencia.txt` que contiene la flag del grupo”*. Esto se aplicará a cada instancia de ese tipo de VM, usando variables proporcionadas por Tectonic como el número de instancia (para generar diferencias por grupo). En resumen, Ansible permite **un alto grado de personalización** de los escenarios de forma automatizada y consistente.

- **Despliegue y gestión sencilla**: Una vez definido el escenario (YAML + playbooks + otros recursos), Tectonic facilita comandos para **crear las imágenes base** (`tectonic ... create-images`) y **desplegar las instancias** (`tectonic ... deploy`). Por ejemplo, el instructor podría ejecutar `tectonic -c config.ini lab_escenario8.yml deploy --images` para generar y levantar el escenario final para, digamos, 5 grupos de estudiantes simultáneamente. Tectonic se encarga de clonar las máquinas para cada instancia de grupo, aplicar los playbooks y **habilitar el acceso de los estudiantes** (creando usuarios de acceso SSH/VNC según se configure). Asimismo, es fácil **destruir** los entornos (`tectonic ... destroy`) para liberar recursos al terminar un ejercicio, o re-desplegarlos limpios para otro grupo/clase. Esta agilidad es crucial para manejar múltiples prácticas durante un determinado curso.

- **Monitoreo y acceso administrativo**: Tectonic permite que los instructores tengan acceso administrativo a las VMs de los escenarios. Mediante claves SSH configuradas para los profesores, el instructor puede entrar a cualquier máquina durante el laboratorio, ya sea para observar el progreso de un grupo, inyectar algún fallo adicional en vivo, o prestar ayuda técnica si algún estudiante tiene problemas con una herramienta. El monitoreo en tiempo real de Tectonic también se integra con herramientas como Elastic; es decir, se pueden recopilar logs y métricas de las máquinas del escenario mientras están en ejecución. Por ejemplo, el tráfico de red de las VMs se puede capturar mediante Packetbeat (parte del Elastic Stack) para ver en vivo qué comunicaciones ocurren. Tectonic tiene una sección de configuración específica para Elastic Security que, al activarla, automáticamente desplegará componentes de **Elasticsearch/Kibana** en el entorno y aplicará políticas de recopilación de datos (por ejemplo, instalar un agente en las VMs o usar Packetbeat para monitorear redes). De esta manera, el instructor cuenta con **visibilidad centralizada** de la actividad en cada instancia de laboratorio.

- **Ataques automatizados (Caldera)**: Otro punto fuerte de Tectonic es que soporta la integración de **MITRE Caldera** para simular ciberataques de forma automatizada. Si el escenario lo contempla, Tectonic puede desplegar un servidor Caldera y agentes en las VMs víctimas/atacantes. El instructor podría entonces cargar un perfil de adversario (basado en MITRE ATT&CK) y lanzarlo dentro del entorno. Esto facilita recrear *tácticas, técnicas y procedimientos (TTPs)* de atacantes reales sin requerir que un humano juegue el rol de atacante durante la clase. Por ejemplo, Caldera podría ejecutar automáticamente una secuencia: enumeración de la red, robo de credenciales, movimiento lateral, etc., imitando un **attack chain** completo mientras los estudiantes intentan detectarlo y responder. Todo esto se puede realizar controladamente, ajustando la dificultad (ej., un adversario “moderado” que comete errores detectables). Esta funcionalidad de ataques automatizados estaba entre los objetivos de diseño de Tectonic, ya que provee *“simulaciones de ataque automatizadas”* que complementan la experiencia práctica.

Concluyendo, **usar Tectonic** implica primero describir el escenario (qué máquinas, qué software, qué conexiones), luego personalizar su contenido con Ansible (evidencias, compromisos, cuentas), y finalmente desplegarlo con un comando. Durante la ejecución, la plataforma ofrece mecanismos de **seguimiento** tanto manual (acceso directo) como centralizado (vía Elastic) para que el docente evalúe el progreso de los alumnos. Al finalizar, los entornos se destruyen o se reciclan fácilmente. 

Tectonic ha sido probada en cursos de grado y posgrado en ciberseguridad, mostrando ser apta para este tipo de entrenamientos. Su enfoque modular y automatizado reduce la carga administrativa de preparar laboratorios, permitiendo iterar o escalar los escenarios (p. ej. aumentar el número de instancias si crece la matrícula, o compartir escenarios con otras instituciones). Además, al ser de código abierto, se puede extender con nuevas plantillas de escenarios que encajen exactamente con las necesidades del posgrado.

## Integración de Elastic, Caldera y Ansible para Mejorar la Experiencia y Evaluación  
Para enriquecer el cyber range y facilitar tanto el aprendizaje como la evaluación de los estudiantes, integraremos varias herramientas en la plataforma:

- **Elastic Stack (Elastic Security)**: La pila Elastic (Elasticsearch, Kibana, Beats) se usará como plataforma de **monitorización y SIEM** dentro de los escenarios. Activando Elastic en Tectonic, se despliega un servidor Elasticsearch/Kibana que recopilará logs y métricas de las máquinas del laboratorio. Por ejemplo, podemos instalar *Beats* en las VMs: Filebeat para enviar logs del sistema (eventos de Windows, syslogs de Linux), Packetbeat para capturar el tráfico de red entre máquinas, o Auditbeat para registrar acciones en los endpoints. Esto tiene varios beneficios:
  - **Experiencia de SOC/SIEM**: Los estudiantes pueden usar Kibana (interfaz web) para buscar indicadores en tiempo real, crear visualizaciones de tráfico o incluso emplear las funciones de detección de Elastic Security (reglas predefinidas para detectar actividades sospechosas). De este modo, aprenden a manejar una herramienta SIEM ampliamente usada en la industria mientras resuelven el escenario práctico. Por ejemplo, en el escenario de la semana 4-5, Kibana podría mostrar alertas de detección (reglas tipo "múltiples intentos de autenticación fallidos" o "ejecución de `vssadmin.exe delete shadows` que indica ransomware) si previamente configuramos esas reglas.
  - **Seguimiento del progreso**: Desde el lado del instructor, Elastic facilita ver qué están haciendo los alumnos. Supongamos que cada grupo debe encontrar un archivo "flag.txt" en su VM; podríamos configurar Auditbeat para enviar un evento cuando alguien abra ese archivo. El instructor, monitorizando Kibana, sabrá en tiempo real qué grupos ya accedieron a la evidencia (flag) y cuáles no. Así, Elastic se convierte en una herramienta de **evaluación automática**: ciertas consultas o dashboards pueden revelar qué tan avanzados van los equipos (¿ya detuvieron el proceso malicioso? ¿ya extrajeron la memoria RAM? – detectado, por ejemplo, por la ejecución de cierto comando). Tectonic soporta cargar *políticas de Elastic preconfiguradas* en el escenario, de forma que todas estas recolecciones y alertas estén listas al iniciar el lab.
  - **Registro histórico para debriefing**: Todos los logs almacenados permiten que, tras el ejercicio, los estudiantes re-examinen lo ocurrido con calma. Podrán revisar la cronología exacta de eventos (tanto sus acciones como las del adversario simulado) y aprender de ello. También permite al instructor realizar una evaluación forense de las acciones de los alumnos (*process mining* de la actividad, como lo han investigado los creadores de Tectonic en trabajos posteriores.

  En la práctica, para implementarlo, se habilita Elastic en la configuración del lab (`elastic_settings.enable: yes` en Tectonic) y se definen qué datos recolectar. Quizá usemos un contenedor Packetbeat en el host para capturar tráfico de la red virtual interna (monitor_type: “traffic”), y agentes Elastic en cada VM para logs. Con esto logramos un **aprendizaje orientado a datos**, donde los estudiantes no solo investigan la evidencia directamente en las máquinas, sino que también ven la perspectiva agregada en un SIEM.

- **MITRE Caldera (Emulación de adversarios)**: Como se mencionó, Caldera es una plataforma para **automatizar la emulación de ciberataques** de manera escalable. Integrarlo en los escenarios proporcionará un *“enemigo virtual”* que ejecuta acciones maliciosas realistas. Ventajas y usos específicos:
  - **Ataques reproducibles y personalizables**: Podemos diseñar distintos *profiles* de adversario en Caldera que correspondan a los escenarios. Por ejemplo, un adversario tipo *APT* que hace movimiento lateral lentamente, u otro más destructivo (ransomware). Caldera permite **construir perfiles de amenaza específicos y lanzarlos en la red para ver por dónde puede moverse**. Esto ayuda a entrenar al Blue Team (nuestros estudiantes) en cómo detectar amenazas particulares. En un contexto educativo, el instructor puede programar el ataque para que ocurra en cierto momento o bajo ciertas condiciones, obligando a los alumnos a estar alerta.
  - **Cobertura de técnicas ATT&CK**: Caldera viene con una biblioteca de técnicas de ATT&CK que se pueden ejecutar mediante sus agentes. Así nos aseguramos de cubrir en la práctica varias técnicas que los estudiantes deben aprender a reconocer: uso de `Mimikatz` para dumping de credenciales, movimiento lateral con `PsExec`, exfiltración mediante DNS tunneling, etc. Por ejemplo, se podría ejecutar un plan donde el agente (en la máquina víctima) intente extraer credenciales y moverse a otra máquina; los alumnos tendrían que notar ese comportamiento inusual en los logs o en la red. La posibilidad de **automatizar pruebas de defensas** es precisamente uno de los enfoques de Caldera, y acá lo usamos para evaluar las habilidades defensivas de los estudiantes.
  - **Evaluación continua y segura**: Al no depender de un atacante humano improvisado, garantizamos que cada grupo se enfrenta al mismo reto de manera equivalente. Además, se evita exponer malware real descontrolado: Caldera utiliza agentes controlados, por lo que los “ataques” están contenidos y son reversibles. Esto mantiene el entorno seguro. 
  - **Extensibilidad**: En caso de requerir algún comportamiento específico, Caldera es extensible mediante plugins. Por ejemplo, podríamos crear un plugin que haga que el agente coloque un archivo de flag en el sistema una vez completada cierta fase del ataque, o envíe una señal a Elastic. Esto podría integrarse con las métricas de evaluación (por ejemplo, marcar tiempo que tardó el Blue Team en detectarlo).

  En resumen, Caldera añade **realismo y dinámica** a los escenarios, obligando a los estudiantes a reaccionar a un oponente activo. Combina bien con Elastic: los movimientos del adversario generan logs y tráfico que los alumnos deben interceptar. Implementar Caldera en Tectonic es tan sencillo como habilitarlo (`caldera_settings.enable: yes`) y proveer los “artifacts” (scripts/operaciones) que se importarán al servidor Caldera en el despliegue. 

- **Ansible**: Además de su rol en la preparación del entorno (instalando software, evidencias, etc.), Ansible se puede aprovechar para mejorar la evaluación y la equidad entre grupos:
  - **Flags únicas por grupo**: Usando variables en Ansible es posible generar contenido único por instancia. Tectonic proporciona una variable de **semilla aleatoria** (`random_seed`) para generar parámetros aleatorios en cada despliegue. Por ejemplo, en el playbook podríamos tener una tarea que genere un string aleatorio basado en `{{ random_seed }}` y lo escriba en el archivo `flag.txt` de ese grupo. Así, cada grupo tiene un flag distinto que encontrar. Esto fomenta que cada equipo realice realmente el análisis (no vale compartir respuestas), y el instructor puede llevar control de quién reporta su flag correctamente.
  - **Orquestación de resets/checks**: Con Ansible, el profesor podría lanzar tareas durante o después del ejercicio. Por ejemplo, un playbook de *“colecta final”* que junte automáticamente ciertos archivos de las máquinas de todos los grupos (los informes generados, o las flags halladas) para calificación. O restaurar configuraciones rápidamente si algún alumno cambió algo que impida continuar (volviendo a un snapshot o re-ejecutando parte del playbook en esa VM). Esta capacidad de *control central* ahorra tiempo en la gestión de la clase.
  - **Inserción de pistas dinámicas**: Si se ve que todos los grupos están estancados, el instructor podría, vía Ansible, soltar un “hint” en las máquinas (por ejemplo, agregar un log llamativo en el SIEM que los redirija). Sería como un **“empujón” programático** para ayudar sin tener que intervenir manualmente en cada máquina.

Integrar estas herramientas convierte el cyber range en un **ecosistema completo de entrenamiento**: los alumnos actúan como analistas SOC/forenses utilizando Elastic para ver lo que sucede, mientras un atacante automatizado (Caldera) genera actividad maliciosa, todo orquestado y observado por el instructor mediante Tectonic/Ansible. La evaluación se puede hacer en base a **indicadores objetivos** (flags encontradas, alertas detectadas, tiempo de respuesta) además de las entregas escritas. 

Por ejemplo, supongamos que en el escenario final cada grupo debe identificar 3 evidencias clave (cada una es una flag). Podríamos tener una visualización en Kibana que muestre, para cada instancia de grupo, cuántas de las 3 evidencias han sido abiertas en su sistema (asumiendo registramos esos eventos). Así el profesor sabrá en vivo qué grupos están rezagados y quizás dar ayuda puntual. Al final, esas mismas métricas pueden usarse para calificar parte de la nota práctica, complementando el informe que presenten.

Desde el punto de vista de los estudiantes, la integración de estas tecnologías los expone a **herramientas industriales**: un SIEM (Elastic) para monitoreo, frameworks de ataque (Caldera) similares a los empleados en red teaming, y la noción de automatización con Ansible que es muy útil también en respuesta a incidentes (por ejemplo, para **contención automatizada** en entornos reales se usan orquestaciones similares). Esto enriquece su formación más allá del caso puntual, dándoles habilidades transferibles a su vida profesional.


En conclusión, el diseño propuesto se alinea con las mejores prácticas internacionales y locales en educación de ciberseguridad. Al adoptar Tectonic como plataforma, con su enfoque declarativo y herramientas integradas, aprovechamos una solución robusta ya probada en ambientes académicos. La integración de Elastic para monitoreo y Caldera para simulación de adversarios aporta modernidad y realismo, tal como lo hacen instituciones punteras. Y fundamentar los contenidos en estándares como NIST garantiza que enseñamos lo correcto. Con todo ello, este cyber range educativo brindará a los estudiantes una **experiencia de aprendizaje práctica, envolvente y progresiva** en análisis forense digital y gestión de incidentes, preparándolos para afrontar ciberataques reales de forma competente y metódica. -->

## Ejemplos e Inspiración en Otras Instituciones  
Varios centros educativos y organizaciones ya emplean enfoques similares de cyber ranges y laboratorios prácticos para enseñar DFIR, lo que brinda confianza y modelos a seguir para nuestro diseño:

- **Uso de Tectonic en educación local**: La plataforma Tectonic misma ha sido utilizada en cursos universitarios de grado y posgrado en ciberseguridad, así como en entrenamientos profesionales, en Uruguay y Latinoamérica. Por ejemplo, en 2024 se llevó a cabo un taller "Train the Trainers" en Uruguay donde instructores de la región aprendieron a crear escenarios en Tectonic y compartieron metodologías. Esto indica que existe ya una comunidad activa intercambiando *best practices* y escenarios. Nuestro posible planteamiento de mezclar tráfico benigno/malicioso y usar Elastic/Caldera encaja perfectamente con la filosofía de Tectonic, pues justamente esas capacidades fueron motivo de su desarrollo. Se pueden revisar los escenarios de ejemplo incluidos en Tectonic (por ejemplo, uno llamado “Password Cracking” con dos máquinas, atacante y víctima, para un ejercicio de cracking de contraseñas) como base para diseñar los nuestros adaptados a DFIR. [15](#referencias)

- **Currículum escalonado (ejemplo Carnegie Mellon)**: La Universidad Carnegie Mellon (a través del CERT/SEI) ofrece un track de *Cyber Forensics and Incident Response (CyFIR)* que sirve de inspiración sobre cómo organizar contenidos. En dicho programa, los estudiantes toman cursos de **Forense en Hosts**, **Forense de Red** y luego un **Capstone de Respuesta a Incidentes** integrador. Esta estructura refleja la progresión de enseñar primero análisis forense en entornos controlados (equipos individuales, redes pequeñas) y después combinarlo todo en un ejercicio complejo de respuesta a incidentes. Nuestra idea de cyberrange puede llegar a seguir una idea bastante similar a la planteada en este caso. El éxito de programas como el de CMU sugiere que esta progresión pedagógica es eficaz para cementar habilidades DFIR [11](#referencias).

- **Cyber ranges académicos internacionales**: Instituciones como el Rochester Institute of Technology (RIT) cuentan con cyber ranges para entrenamiento avanzado donde simulan crisis de ciberseguridad a gran escala. El Cyber Range del ESL Global Cybersecurity Institute en RIT, por ejemplo, ofrece entrenamientos de respuesta a incidentes que incluyen escenarios de **ataques de Denegación de Servicio y Ransomware**. Ellos destacan la combinación de teoría con práctica interactiva y el valor de la enseñanza inmersiva (“real world feel of responding to a cybersecurity crisis”). Incluso recaban *datos de la experiencia de usuario y logs técnicos para fines de investigación*, lo cual es paralelo a nuestra idea de usar Elastic para seguimiento y análisis post-ejercicio en el caso que optemos por un escenario similar. Si bien nuestro contexto es un curso académico más que entrenamiento corporativo, podemos inspirarnos en estos escenarios utilizados en RIT para afinar la relevancia de los casos propuestos. [10](#referencias).

- **Competiciones y desafíos CTF**: Aunque nuestro enfoque es educativo y no competitivo per se, vale la pena mencionar que muchas competencias universitarias de ciberseguridad (como el National Collegiate Cyber Defense Competition en EE.UU. o desafíos estilo CTF) incorporan elementos de DFIR. En ellos, los equipos deben mantener operativa la infraestructura mientras responden a inyecciones de ciberataques en tiempo real, obteniendo puntos por restaurar servicios y resolver inyects forenses. Estas experiencias refuerzan la idea de *aprendizaje bajo presión* y la gamificación. Podemos emular parcialmente ese modelo al incluir el componente de “capturar flags” por grupo en el escenario final, creando un ambiente que motive y recompense el descubrimiento de evidencias. La literatura muestra que la gamificación en cyber ranges puede aumentar el compromiso de los alumnos y simular el estrés de un incidente real de forma controlada. [7](#referencias)

- **Recursos abiertos y documentación**: Existen organizaciones y proyectos que han publicado guías y contenido aprovechable. Por ejemplo, el **NICE Challenge Project** (NIST/NICE) desarrolló escenarios prácticos gratuitos orientados a roles de ciberseguridad, algunos relacionados con respuesta a incidentes, que podríamos revisar para obtener ideas de desafíos técnicos a incluir. Asimismo, ENISA (Agencia Europea de Ciberseguridad) y organismos como la OAS (Organización de Estados Americanos) han publicado manuales de ejercicios y *checklists* para cyber ranges y entrenamiento en CSIRT que podrían ser útiles.  Priorizar fuentes oficiales nos llevó a basar los conceptos en NIST, MITRE, etc., pero también en casos de estudio reales: por ejemplo, podríamos basar un laboratorio en un incidente público conocido (como la infección de Wannacry) para darle relevancia y luego mostrar en clase cómo lo resolvió la industria. [14](#referencias)


## Referencias

1. Johansen, G. – *Digital Forensics and Incident Response* (Second Edition).
2. Johansen, G. – *Digital Forensics and Incident Response* (First Edition) (an intelligent way to respond to attacks).
3. Sheward, M. – *Hands-on Incident Response and Digital Forensics*.
4. Xu, W., Deng, L., & Xu, D. – *Towards Designing Shared Digital Forensics Instructional Materials* (University of Baltimore, Towson University, University of Missouri – Kansas City).
5. Digital Forensic Research Workshop (DFRWS). (2001). *A Road Map for Digital Forensic Research*. The Digital Forensic Research Conference, DFRWS 2001 USA, Utica, NY.
6. Kent, K., Chevalier, S., Grance, T., & Dang, H. (2006). *Guide to Integrating Forensic Techniques into Incident Response* (NIST Special Publication 800-86). [Ver paper](https://csrc.nist.gov/publications/detail/sp/800-86/final).
7. Guerrero, G., Betarte, G., & Campo, J. D. – *Tectonic: An Academic Cyber Range* (IEEE Argencon 2024).
8. Tectonic (Universidad de la República) – Documentación oficial y repositorio GitHub ([Ver repositorio](https://github.com/GSI-Fing-Udelar/tectonic)).
9. MITRE Caldera – Página oficial (adversary emulation platform) ([Ver sitio](https://caldera.mitre.org/)).
10. RIT ESL Cyber Range – Descripción de entrenamientos avanzados (IR, ransomware) ([Más información](https://www.rit.edu/cybersecurity/cyber-range)).
11. Carnegie Mellon (CERT) – Track CyFIR y cursos ([Ver programa](https://www.cmu.edu/ini/academics/cyfir.html)).
12. Grupo GSI FING-UdelaR – Presentaciones y talleres Tectonic en educación ([Ver página](https://www.fing.edu.uy/inco/proyectos/tectonic)).
13. Cybersecurity and Infrastructure Security Agency. (n.d.). *Incident Response Plan Basics*. [Ver documento](https://www.cisa.gov/sites/default/files/publications/Incident-Response-Plan-Basics_508c.pdf).
14. NICE Challenge Project. (s.f.). *The workforce experience before the workforce*. https://nice-challenge.com/ ([NICE Challenge Project](https://nice-challenge.com/))
15. Grupo GSI FING-UdelaR – Presentaciones y talleres Tectonic en educación (Train the Trainers 2024) ([Tectonic](https://www.fing.edu.uy/inco/proyectos/tectonic#:~:text=This%20workshop%20took%20place%20in,of%20this%20cyber%20range%2C%20training))  

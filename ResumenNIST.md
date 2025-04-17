# **NIST Article**

## **Fases del Proceso Forense Digital**

El proceso forense digital se estructura en cuatro fases secuenciales: **Colección**, **Examinación**, **Análisis** y **Reporte**. Cada etapa cumple una función específica que transforma los elementos progresivamente desde **medios físicos** hasta **evidencia forense estructurada**, pasando por datos y luego información.

### 1. **Colección (Collection)**

Esta fase inicial implica la **identificación, etiquetado, registro y adquisición de datos** desde las fuentes potenciales relacionadas con el evento investigado. Se deben emplear procedimientos que garanticen la integridad de los datos desde el momento de su recolección, aplicando un estricto control de **cadena de custodia**.

#### Componentes clave:
- **Identificación de fuentes**: Computadoras, laptops, servidores, dispositivos móviles, medios extraíbles, routers.
- **Planificación de adquisición**:
  - *Valor probable de los datos*.
  - *Volatilidad* (ej. RAM o sesiones activas).
  - *Esfuerzo requerido* (logístico, técnico y legal).
- **Adquisición**: Uso de herramientas forenses para obtener datos volátiles y no volátiles, ya sea localmente o vía red.
- **Verificación de integridad**: Comparación de hash entre original y copia (por ejemplo, SHA-256 o MD5) para asegurar que no hubo modificaciones.

> Es fundamental decidir, previo a la adquisición, si el objetivo es generar evidencia legal. En tal caso, la recolección debe ser conservadora, documentada y legalmente admisible.

---

### 2. **Examinación **

En esta fase se procede al **procesamiento técnico del conjunto de datos recolectado**, con el fin de identificar y extraer información relevante, siempre resguardando su integridad.

#### Actividades principales:
- Empleo de herramientas automatizadas y técnicas manuales para filtrar y localizar datos de interés.
- Superación de mecanismos de ocultamiento como compresión, cifrado o controles de acceso.
- Clasificación y filtrado mediante búsquedas por patrón, firmas digitales, tipo de contenido, y uso de bases de datos de archivos conocidos.

> Esta etapa requiere habilidades analíticas y técnicas avanzadas para reducir el volumen de datos y focalizarse en aquellos elementos relevantes.

---

### 3. **Análisis**

El análisis implica **interpretar la información extraída** para construir una narrativa coherente de los hechos, respondiendo a las preguntas que motivaron la investigación.

#### Enfoque metodológico:
- Correlación entre múltiples fuentes (logs, IDS, sistemas, usuarios, timestamps).
- Determinación de relaciones causa-efecto entre personas, eventos y sistemas.
- Uso de herramientas como SIEMs, sistemas de auditoría y líneas base del sistema para identificar alteraciones.

> El análisis debe ser riguroso, imparcial y respaldado por evidencia técnica, permitiendo identificar autores, medios y fines, o reconocer la imposibilidad de llegar a una conclusión certera.

---

### 4. **Reporte **

El reporte es la **síntesis formal del análisis realizado**, documentando el proceso, las evidencias, las herramientas utilizadas y los resultados obtenidos.

#### Aspectos clave del reporte:
- **Claridad en los hechos** y documentación de las técnicas empleadas.
- **Audiencia objetivo**: desde técnicos a gerencia o autoridades legales. El lenguaje debe adaptarse en complejidad y detalle.
- **Hipótesis alternativas**: cuando existan múltiples explicaciones plausibles, todas deben ser consideradas.
- **Recomendaciones**: Incluyen mejoras de seguridad, acciones correctivas, o sugerencias para futuras investigaciones.

> La utilidad del reporte depende de su claridad, consistencia y adecuación a los destinatarios.

---

## **Recomendaciones Finales**

- Aplicar este proceso de forma consistente, documentada y estandarizada.
- Preparar al equipo para creonocer fuentes de datos menos evidentes y recolectarlas de forma proactiva.
- Priorizar la integridad de la evidencia por sobre la velocidad o conveniencia.
- Evaluar regularmente los procedimientos a la luz de nuevas tecnologías, normativas o lecciones aprendidas de incidentes pasados.


## **Capítulo 4 – Fundamentos y Procesos de Análisis de Archivos en Forense Digital**

#### **4.1.1 Medios de Almacenamiento de Archivos**

Los archivos pueden almacenarse en una amplia variedad de medios, que incluyen desde discos duros y CD-ROMs hasta memorias flash, tarjetas SD, dispositivos móviles. Estos medios deben ser **particionados y formateados** antes de su uso, creando volúmenes lógicos sobre los cuales se arman los sistemas de archivos.

#### **4.1.2 Filesystems**

Los sistemas de archivos son responsables de **organizar y localizar archivos** dentro de los medios de almacenamiento. Ejemplos incluyen: FAT12/16/32, NTFS, ext2/ext3, HFS/HFS+, UFS, ISO 9660, y UDF.

- Los archivos se almacenan en **unidades de asignación** (clusters o bloques), y cada entrada en el sistema de archivos contiene metadatos que describen nombre, ubicación, permisos, y tiempos.
- Es importante notar que los sistemas de archivos **no eliminan físicamente los datos** al borrar un archivo, sino que marcan su espacio como disponible.

#### **4.1.3 Espacios Residuales de Datos**

- **Archivos eliminados**: aún pueden recuperarse si no han sido sobrescritos.
- **Slack space**: espacio no utilizado dentro de una unidad de asignación, puede contener fragmentos de otros archivos.
- **Free space**: sectores sin asignar que pueden contener datos residuales.

---

### **4.2 Recolección de Archivos**

#### **4.2.1 Técnicas de Copiado FUNDAMENTALES**

- **Backup lógico**: copia archivos visibles, omite archivos eliminados y slack space.
- **Bit stream imaging**: copia bit a bit del medio, incluyendo todos los sectores (ideal para uso legal).

> Para investigaciones forenses legales, siempre debe utilizarse una **imagen bit a bit**, conservando el original como evidencia y trabajando sobre copias.

#### **4.2.2 Verificación de Integridad**

- Uso de **write-blockers** para evitar modificaciones al medio original en el cual se va a realizar el analisis forense.
- Verificación mediante **hashes (SHA-1 preferentemente sobre MD5)** antes y después de copiar la imagen.

#### **4.2.3 Tiempos MAC (Modificación, Acceso, Creación)**

Estos metadatos pueden estar alterados o no ser precisos. La sincronización de sistemas con **NTP (Network Time Protocol)** y la documentación del entorno temporal son esenciales para una correcta interpretación.

#### **4.2.4 Desafíos Técnicos**

- **Wiping** o destrucción física del medio puede imposibilitar la recuperación.
- **Datos ocultos**: archivos ocultos, particiones invisibles, Host Protected Area (HPA), Alternate Data Streams (ADS).
- **RAID striping**: requiere reconstrucción de todos los discos para examinar correctamente el volumen.

- *RAID*: redundant array of independent disks 

---

### **4.3 Examen de Archivos**

#### **4.3.1 Localización y Extracción de Archivos**

Una vez creada la imagen, se deben ubicar los archivos relevantes:
- Archivos visibles, eliminados, fragmentos en slack/free space, archivos ocultos.
- Archivos comprimidos, cifrados, protegidos por contraseña o esteganografia.

#### **4.3.2 Herramientas y Técnicas Forenses**

- **Viewers**: permiten previsualizar sin usar la aplicación original.
- **Descompresión temprana** para incluir contenido en el análisis.
- **Exploración visual de estructuras de directorio** para entender uso y perfiles de usuario.
- **Identificación de archivos conocidos** con hash sets como NSRL.
- **Búsqueda de cadenas y patrones**, incluso con lógica difusa, conceptos y sinónimos.
- **Extracción de metadatos** para inferir información de creación, modificaciones, software utilizado, y configuraciones del dispositivo (por ejemplo, EXIF en imágenes).

---

### **4.4 Análisis**

Una vez extraída la información, el analista debe correlacionar datos y eventos, prestando atención a los MAC times y su consistencia.

- Es clave comprender cómo las herramientas acceden, modifican o interpretan los tiempos de archivo.
- El uso de sistemas con **bloqueo de escritura** reduce la posibilidad de alteraciones, pero **la caché del sistema operativo puede afectar la precisión** del acceso a MAC times.

---

## **Recomendaciones Clave**

- Trabajar siempre con copias, **nunca con los originales**.
- Verificar integridad mediante hash, **usar SHA-1** para cumplimiento con FIPS.
- No confiar exclusivamente en las extensiones de archivos. Validar tipo de contenido.
- Contar con un **conjunto de herramientas forenses especializado** para extracción, visualización, análisis y búsqueda.
- Documentar rigurosamente todo el proceso para garantizar **la cadena de custodia** y la reproducibilidad del análisis.

---

## **Capítulo 5 – Análisis Forense del Sistema Operativo**

El sistema operativo es una fuente de información crítica en el análisis forense digital. Sus datos se dividen en **no volátiles** y **volátiles**. La adquisición y análisis de estos datos requiere técnicas específicas que garanticen la preservación de su integridad y su validez como evidencia.

---

### **5.1 Fundamentos del Sistema Operativo**

#### **5.1.1 Datos No Volátiles**

Los datos no volátiles permanecen almacenados incluso luego de que el sistema ha sido apagado. Las principales fuentes incluyen:

- **Sistemas de archivos**: Contienen la mayor parte de la información persistente, incluyendo archivos de configuración, usuarios y contraseñas, registros de eventos y archivos de datos.
- **Archivos de configuración**: Definen parámetros del sistema y las aplicaciones (por ejemplo, servicios que se inician automáticamente, rutas de logs).
- **Usuarios, grupos y contraseñas**: Información sobre cuentas, privilegios y credenciales.
- **Logs**: Registro de eventos del sistema, auditorías, errores, accesos y actividades de las aplicaciones.
- **Historial de comandos y archivos recientes**: Pistas sobre acciones de usuarios.
- **Swap Files**: Archivos que extienden la memoria RAM, pueden contener datos sensibles.
- **Hibernation/Dump Files**: Capturan el estado de memoria ante errores o suspensión del sistema.
- **Archivos temporales**: Contienen datos residuales de instalaciones, ejecuciones o actualizaciones.
- **BIOS**: Información de hardware, configuraciones de seguridad, y dispositivos conectados.

#### **5.1.2 Datos Volátiles**

Los datos volátiles existen solo mientras el sistema está encendido. Incluyen:

- **Contenido de RAM**: Información sensible como comandos recientes, contraseñas, procesos activos.
- **Slack y free space de memoria**: Fragmentos residuales no asignados pueden contener datos útiles.
- **Conexiones de red**: Detalles sobre conexiones activas y recientes.
- **Procesos en ejecución**: Servicios del sistema y aplicaciones activas.
- **Archivos abiertos**: Incluyen datos sobre qué procesos están accediendo a qué archivos.
- **Sesiones de login activas**: Información de usuarios conectados y sesiones anteriores.
- **Configuración de red** y **hora del sistema**: Clave para correlacionar eventos y entender el entorno de ejecución.

---

### **5.2 Recolección de Datos del OS**

#### **5.2.1 Recolección de Datos Volátiles**

Debe realizarse **antes de apagar el sistema**, idealmente mediante un conjunto de herramientas forenses contenidas en un medio externo (USB, CD, entre otros). Se recomienda:

- Usar solo herramientas confiables y forenses.
- Ejecutar los comandos desde el medio externo para minimizar la alteración de RAM.
- Priorizar la recolección en el siguiente orden (IMPORTANTE):
  1. Conexiones de red
  2. Sesiones activas
  3. RAM (memoria volátil)
  4. Procesos
  5. Archivos abiertos
  6. Configuración de red
  7. Hora del sistema

> El uso de herramientas como `netstat`, `ps`, `lsof`, `w`, `date`, `ifconfig/ipconfig` es común en Unix/Linux.

#### **Consideraciones Técnicas:**
- Riesgo de alteración de datos volátiles al ejecutar herramientas.
- Presencia de **rootkits** que pueden alterar o falsear información.
- **Protecciones de acceso** como pantallas bloqueadas, autenticación biométrica.
- **Remapeo de teclas**: Puede ejecutar acciones destructivas no intencionadas.

#### **Apagado del Sistema:**
- **Graceful Shutdown**: Cierra archivos y procesos, pero puede borrar datos sensibles como archivos temporales o swap.
- **Power-Off directo**: Conserva más datos, pero puede corromper archivos abiertos.

---

### **5.2.2 Recolección de Datos No Volátiles**

Se recomienda realizar **bit stream imaging** antes de cualquier modificación del sistema. Además:

- Evitar alterar el sistema.
- Verificar integridad con hashes (SHA-1).
- Registrar todos los datos del medio (modelo, capacidad, número de serie).

> En caso de que no se pueda apagar adecuadamente, se puede retirar el disco y montarlo en un entorno forense con **write-blockers**.

---

### **5.3 Examen y Análisis de Datos del OS**

El análisis de los datos recolectados implica:

- Usar herramientas de integridad como **checksums (SHA-1)** para detectar cambios en archivos del OS.
- Verificar logs y eventos del sistema, incluyendo accesos, errores, e intentos fallidos de ingreso.
- Analizar **swap files y RAM dumps** usando herramientas automáticas o editores hexadecimales.
- Inspeccionar procesos en ejecución y sus descripciones para detectar software malicioso disfrazado (e.g., `calculator.exe` como troyano).
- Considerar técnicas anti-forenses como ocultamiento de logs, sobreescritura, y cifrado.

---

### **Recomendaciones Clave**

- **Preservar y documentar datos volátiles** antes de apagar el sistema.
- Usar **kits forenses confiables** y ejecutar desde medios externos.
- Priorizar la recolección según criticidad y riesgo de pérdida.
- Entender los **efectos del shutdown** sobre la persistencia de evidencia.


## **Capítulo 6 – Análisis Forense de Tráfico de Red**

El análisis forense de red se enfoca en la recolección, examen y análisis del tráfico que circula por una red de computadoras. Debido a su complejidad y volumen, este tipo de análisis requiere conocimientos profundos del modelo TCP/IP, múltiples fuentes de datos y herramientas especializadas.

---

### **6.1 Fundamentos del Tráfico de Red**

#### **6.1.1 Capa de Aplicación**

La capa de aplicación permite la transferencia de datos entre aplicaciones cliente-servidor mediante protocolos como HTTP, DNS, FTP, SMTP, y SNMP. El tráfico generado por estas aplicaciones puede ser utilizado para detectar usos indebidos, ataques, filtraciones de datos o actividades maliciosas.

#### **6.1.5 Relevancia de las Capas en Forense de Red**

Las cuatro capas del modelo TCP/IP (física, red, transporte y aplicación) aportan datos críticos. Por ejemplo:

- La dirección **MAC** identifica el dispositivo físico.
- La dirección **IP** identifica el host lógico.
- Los **puertos y protocolos** indican el tipo de servicio o aplicación.
- El contenido en la **capa de aplicación** puede confirmar el propósito o naturaleza del tráfico.

El análisis forense se basa en correlacionar estos datos entre sí para identificar hosts, eventos y rutas de ataque.

---

### **6.2 Fuentes de Datos de Tráfico de Red**

#### **6.2.1 Firewalls y Routers**

Capturan intentos de conexión, paquetes denegados, direcciones IP, y puertos. Su valor es limitado para eventos específicos, pero útil para observar tendencias generales o bloqueos reiterados.

#### **6.2.2 Sniffers y Analizadores de Protocolos**

- Sniffers colocan la NIC en **modo promiscuo** para capturar todo el tráfico visible.
- Protocol analyzers **reensamblan y decodifican** flujos, incluso desde archivos preexistentes.
- Herramientas como Wireshark permiten visualizar sesiones y contenido de protocolos específicos.

#### **6.2.3 Sistemas de Detección de Intrusos (IDS)**

- Pueden ser de red (NIDS) o de host (HIDS).
- Registran detalles de eventos sospechosos: IPs, puertos, comandos, tipos de ataques, estado, y firmas.
- Algunos IDS incluyen funciones de **prevención de intrusiones (IPS)** y pueden almacenar paquetes completos del evento.

#### **6.2.4 Acceso Remoto y VPNs**

Registros de gateways de acceso remoto pueden mostrar conexiones externas hacia sistemas internos. Son clave para identificar accesos no autorizados.

#### **6.2.5 Security Event Management (SEM)**

Software que correlaciona logs de IDS, firewalls, proxies, etc., en una interfaz unificada. Realiza **normalización de datos**, pero puede generar errores; por tanto, siempre se deben conservar los datos originales.

#### **6.2.6 Herramientas de Análisis Forense de Red (NFAT)**

Software que combina funciones de sniffer, analizador de protocolos y SEM. Permiten:

- Reproducción de sesiones.
- Visualización geográfica y topológica del tráfico.
- Creación de perfiles de comportamiento.
- Búsqueda de contenido específico (e.g., “confidential”).

#### **6.2.7 Otras Fuentes**

- **Servidores DHCP**: Asignan IPs a MACs, útil para rastrear equipos.
- **ISPs**: Pueden ofrecer datos bajo orden judicial.
- **Software cliente/servidor**: Puede registrar intentos de conexión, IPs, puertos, y resultados.
- **Logs de host**: Incluyen puertos escuchando, conexiones recientes, y configuraciones.

---

### **6.3 Recolección de Tráfico de Red**

#### **6.3.1 Consideraciones Legales**

- Captura accidental de contenido sensible (contraseñas, emails).
- Violación de políticas de retención si se almacena información privada.
- Importancia de **advertencias de monitoreo** y políticas claras.
- Preservar logs originales cuando haya análisis forense posterior.

#### **6.3.2 Problemas Técnicos Comunes**

- **Almacenamiento insuficiente**: Puede llevar a la pérdida de registros.
- **Tráfico cifrado**: Limita visibilidad (IPSec, SSL, SSH).
- **Puertos inesperados**: Servicios legítimos en puertos atípicos pueden pasar desapercibidos.
- **Puntos de acceso alternativos**: Atacantes pueden evadir controles entrando por caminos no vigilados.
- **Fallos de monitoreo**: Uso de redundancia y múltiples capas de monitoreo es recomendable.

---

### **6.4 Examen y Análisis de Tráfico de Red**

#### **6.4.1 Identificación de Eventos de Interés**

El análisis comienza cuando se detecta una actividad anómala, ya sea por una alerta automática (IDS, firewall) o por una revisión manual.

#### **6.4.2 Evaluación del Valor de las Fuentes**

- **IDS**: Punto de partida frecuente. Puede incluir capturas, pero requiere validación por falsos positivos.
- **SEM**: Útil si correlaciona adecuadamente. Depende de la calidad de las fuentes.
- **NFAT**: Ideal para reconstruir sesiones y detectar patrones visuales.
- **DHCP y NAT**: Importantes para vincular IPs públicas con dispositivos internos.
- **Sniffers**: Fuente más rica en detalle técnico.

#### **6.4.2.2 Herramientas de Examen y Análisis**

Los analistas deben elegir herramientas según el tipo de fuente y evento:

- **Wireshark** para reensamblado y análisis de paquetes.
- **Tcpdump** para capturas livianas.
- **Snort/Suricata** como IDS/IPS.
- **Bro/Zeek** como plataforma de monitoreo avanzada.
- **Splunk, ELK, Graylog** como SEMs.

#### **6.4.3 Conclusiones**

El análisis debe ser **metódico y sustentado en evidencia concreta**. Rara vez se dispone de todos los datos, por lo que se deben formular hipótesis sobre datos faltantes basadas en conocimiento técnico.

#### **6.4.4 Identificación de Atacantes**

- No suele ser la prioridad inmediata.
- Se pueden usar **WHOIS**, logs de ISPs (que se pueden mirar unicamente bajo orden judicial), e inferencias por contenido de capa de aplicación.
- **IP spoofing** y **DDoS distribuidos** complican la atribución.
- En muchos casos, se prefiere **detener el ataque y restaurar sistemas** antes que identificar al atacante, por tema de costos que involucra el encontrar al atacante propiamente dicho.

---

### **6.5 Recomendaciones Clave**

- Definir políticas de privacidad y monitoreo de red.
- Conservar logs originales y configurar almacenamiento adecuado.
- Elegir herramientas y fuentes apropiadas para cada caso.
- Priorizar restauración de servicios y contención de incidentes.
- Validar siempre los datos interpretados (SEM, IDS) contra fuentes crudas.

## **Capítulo 7 – Uso de Datos de Aplicaciones en Análisis Forense**

### **7.1 Componentes Clave de las Aplicaciones**

- **Configuración**: Se almacena en archivos de texto, binarios propietarios, parámetros de ejecución o incluso en el código fuente (en apps open source).
- **Autenticación**: Puede ser interna, externa (LDAP, Active Directory), pasiva (pass-through), o heredada del entorno del sistema operativo.
- **Logs**: Las aplicaciones registran eventos, errores, auditorías, instalación y depuración. Estos logs pueden estar distribuidos entre host local y servidores remotos.
- **Datos**: Todas las aplicaciones manipulan datos; pueden generarlos, transferirlos o almacenarlos.
- **Archivos de soporte**: Incluyen documentación, enlaces, íconos o gráficos relevantes para la funcionalidad y análisis.
- **Arquitectura**:
  - *Local*: Todo en el equipo del usuario.
  - *Cliente/Servidor*: Datos centralizados, configuración y logs distribuidos.
  - *P2P*: Comunicación directa entre nodos; difícil trazabilidad si no hay servidor intermedio.

---

### **7.2 Tipos de Aplicaciones Relevantes**

- **Correo electrónico**: Encabezados revelan rutas, clientes usados, importancia, adjuntos.
- **Web**: Navegadores y apps web usan HTTP(S); pueden generar mucha evidencia a través de sus logs, cookies, cachés.
- **Comunicación interactiva**: Chat grupal (IRC), mensajería instantánea, VoIP. Su arquitectura varía (P2P o C/S).
- **Compartición de archivos**: Protocolos estándar (FTP, SMB) o P2P descentralizados.
- **Documentos**: Pueden tener metadatos incriminatorios.
- **Aplicaciones de seguridad**: Firewalls, antivirus, HIDS pueden registrar comportamientos sospechosos.
- **Herramientas de ocultamiento**: Criptografía, esteganografía, limpiadores de sistema; los analistas deben saber detectarlas.

---

### **7.3 Fuentes de Datos para Aplicaciones**

- **Sistema de archivos**: Ejecutables, configuraciones, logs, datos y documentación.
- **Datos volátiles**: Procesos activos, conexiones de red, archivos abiertos.
- **Tráfico de red**: Conexiones entre componentes distribuidos, DNS lookups, impresiones remotas.

---

### **7.5 Recomendaciones**

- **Centralizar el análisis**: Correlacionar eventos entre múltiples fuentes (archivos, red, OS) para reconstruir actividades.
- **Buscar en todas las capas**: Las aplicaciones dejan huellas en archivos, memoria, red y logs.
- **Analizar desde la funcionalidad de la app**: Entender cómo funciona permite identificar evidencias atípicas o sospechosas.

--- 

# Por aca vamos cerrando el gran articulo del NIST, va workshop aca abajito
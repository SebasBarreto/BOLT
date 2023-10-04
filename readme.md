Ethical Hacking: Reto BOLT
Descripción

Este repositorio documenta el análisis y explotación de la máquina virtual BOLT como parte de un ejercicio de Ethical Hacking. El objetivo del reto fue identificar y explotar vulnerabilidades en los servicios de la máquina objetivo, con el fin de obtener las banderas (flags) ocultas dentro del sistema. El ejercicio abarca desde las fases de reconocimiento, explotación de vulnerabilidades y escalación de privilegios, hasta la obtención de las banderas y la posterior recomendación de medidas para mitigar los riesgos de seguridad encontrados.

El informe que se detalla en este repositorio muestra un enfoque práctico sobre cómo un atacante podría comprometer un sistema, con el objetivo de aprender a proteger redes y sistemas frente a estas amenazas.
Objetivos del Proyecto

    Reconocimiento de la máquina objetivo: Identificar las direcciones IP, puertos abiertos y servicios vulnerables en el sistema.
    Análisis de vulnerabilidades: Explorar los servicios activos en busca de debilidades explotables.
    Explotación de servicios vulnerables: Realizar ataques para obtener acceso no autorizado a los servicios y sistemas de la máquina objetivo.
    Escalación de privilegios: Utilizar técnicas para elevar privilegios y obtener acceso completo al sistema.
    Obtención de banderas: Localizar las banderas ocultas en el sistema que prueban el éxito del ataque.

Herramientas Utilizadas

Las siguientes herramientas fueron utilizadas a lo largo del proceso para realizar la explotación y escalación de privilegios:

    Reconocimiento y escaneo de red:
        ifconfig: Para obtener la IP de la máquina atacante.
        arp-scan: Para identificar dispositivos en la red local.
        nmap: Para realizar un escaneo exhaustivo de puertos y detectar servicios vulnerables.

    Análisis web:
        Dirbuster: Para realizar la exploración de directorios ocultos y encontrar archivos o rutas sensibles en el servidor web.
        Burp Suite: Para realizar ataques de fuerza bruta y otros análisis de seguridad en aplicaciones web.

    Explotación:
        hydra: Para realizar ataques de fuerza bruta en contraseñas.
        ssh: Para realizar acceso remoto al sistema con credenciales obtenidas.
        nc (netcat): Para establecer una shell reversa y obtener acceso al sistema.

    Escalación de privilegios:
        Técnicas de escalación de privilegios mediante la manipulación de scripts automatizados.
        Exploit Sudo: Para aprovechar configuraciones incorrectas en la ejecución de comandos con privilegios elevados.

Proceso
Paso 1: Reconocimiento

El primer paso en el ataque fue realizar un escaneo de la red para identificar la máquina objetivo y los servicios disponibles. Utilizando nmap, se identificaron puertos abiertos, incluyendo servicios de FTP, SSH y HTTP. Esto permitió determinar las posibles vías de explotación.

    Identificación de la máquina objetivo:
    Se utilizó arp-scan para detectar dispositivos en la red y se encontró la dirección IP de la máquina objetivo.

    Escaneo de puertos con nmap:
    Se escanearon los puertos abiertos de la máquina objetivo, encontrando los siguientes servicios:
        21/tcp (FTP)
        22/tcp (SSH)
        80/tcp (HTTP)

Paso 2: Análisis de Vulnerabilidades

En esta fase, se enumeraron los servicios activos en la máquina objetivo y se analizaron posibles vulnerabilidades:

    FTP:
    Se descubrió que el servicio FTP estaba accesible sin autenticación en algunos casos, lo que permitía la carga de archivos. Se realizó un análisis más detallado para identificar configuraciones incorrectas.

    SSH:
    El servicio SSH estaba protegido por contraseña, por lo que se intentó realizar un ataque de fuerza bruta utilizando hydra.

    HTTP:
    A través de Dirbuster, se identificaron directorios sensibles en el servidor web, como /admin y /backup, lo que proporcionó pistas para la siguiente fase de explotación.

Paso 3: Explotación

Se emplearon diversas técnicas de explotación para obtener acceso no autorizado a la máquina.

    Acceso a través de FTP:
    Se explotó el servicio FTP para cargar un archivo malicioso, permitiendo el acceso inicial al sistema.

    Ataque de fuerza bruta en SSH:
    Utilizando hydra, se realizó un ataque de fuerza bruta sobre el servicio SSH, lo que permitió descubrir las credenciales de acceso.

    Explotación de la web:
    Mediante el acceso a los directorios encontrados en la exploración de HTTP, se aprovechó una vulnerabilidad en la configuración de la página de administración para obtener credenciales adicionales.

Paso 4: Escalación de Privilegios

Una vez obtenida la accesibilidad básica al sistema, se intentó escalar privilegios para obtener acceso root:

    Modificación de scripts automatizados:
    Se identificó que el sistema ejecutaba un script con privilegios elevados cada cierto intervalo de tiempo. Se modificó este script para incluir comandos maliciosos que otorgaran acceso root al sistema.

    Exploit Sudo:
    Se encontró que el usuario tenía acceso incorrecto a ciertos comandos con privilegios elevados sin la debida restricción, lo que permitió ejecutar comandos como root sin autorización.

Paso 5: Obtención de las Banderas

Para confirmar el éxito del ataque, se localizó y extrajo las banderas del sistema utilizando el siguiente comando:

find / -name bandera*.txt 2>/dev/null

Se obtuvieron dos banderas, confirmando que el sistema había sido comprometido con éxito.
Recomendaciones de Seguridad

A partir de las vulnerabilidades encontradas en este reto, se proponen las siguientes recomendaciones para mejorar la seguridad en un entorno real:

    Deshabilitar servicios innecesarios: Desactivar FTP y otros servicios de red innecesarios en la máquina para reducir el número de vectores de ataque.
    Uso de contraseñas seguras: Evitar el uso de contraseñas débiles y credenciales predeterminadas, especialmente en servicios críticos como SSH.
    Revisar configuraciones de servicios: Es esencial revisar las configuraciones de servicios como SSH y FTP para prevenir accesos no autorizados.
    Monitoreo de scripts automatizados: Se debe asegurar que los scripts ejecutados por el sistema no tengan configuraciones que permitan la escalación de privilegios de manera inapropiada.
    Auditorías periódicas de seguridad: Realizar auditorías de seguridad regulares para detectar configuraciones inseguras y vulnerabilidades que puedan ser explotadas.

Contribuciones

Este ejercicio es parte de un reto práctico de Ethical Hacking, cuyo objetivo es proporcionar una experiencia realista en la identificación y explotación de vulnerabilidades. Las contribuciones y mejoras en el proceso de explotación, así como la automatización de técnicas de escaneo y explotación, son bienvenidas.
Ethical Hacking: Reto NAVIGATOR
Descripción

Este repositorio documenta el análisis y explotación de la máquina NAVIGATOR, parte de un ejercicio práctico de Ethical Hacking. El objetivo del reto fue identificar y explotar vulnerabilidades en los servicios de la máquina, con el fin de obtener las "banderas" (flags) ocultas en el sistema. Este ejercicio simula un escenario de penetration testing que cubre fases de reconocimiento, explotación de vulnerabilidades, escalación de privilegios y la obtención de las banderas.

A lo largo del proceso, se utilizaron diversas herramientas y técnicas manuales de explotación para comprometer el sistema y obtener acceso completo, mientras se analizan las vulnerabilidades encontradas y las medidas de seguridad para mitigarlas.
Objetivos del Proyecto

    Reconocimiento de la máquina objetivo: Identificar la dirección IP y los puertos abiertos en la máquina objetivo y examinar los servicios disponibles.
    Análisis de vulnerabilidades: Explorar los servicios identificados para encontrar debilidades explotables.
    Explotación de vulnerabilidades: Utilizar técnicas manuales para obtener acceso no autorizado a los servicios.
    Escalación de privilegios: Aprovechar configuraciones incorrectas o vulnerabilidades para ganar privilegios elevados.
    Obtención de las banderas: Localizar y extraer las banderas ocultas para completar el reto.

Herramientas Utilizadas

Las siguientes herramientas fueron clave para realizar el reconocimiento, análisis y explotación durante el reto:

    Reconocimiento y escaneo de red:
        ifconfig: Para obtener la IP de la máquina atacante.
        nmap: Para escanear puertos y servicios en la máquina objetivo.
        arp-scan: Para detectar dispositivos en la red local y verificar la conectividad con la máquina objetivo.
    Análisis web:
        Dirbuster: Para explorar directorios y archivos ocultos en la máquina web.
        Burp Suite: Para realizar análisis de seguridad de aplicaciones web y ataques de fuerza bruta.
    Explotación:
        hydra: Para ejecutar ataques de fuerza bruta sobre credenciales de servicios SSH y FTP.
        netcat: Para establecer una conexión de shell reverso y obtener acceso al sistema.
        ssh: Para acceder al sistema una vez obtenidas las credenciales correctas.
    Escalación de privilegios:
        Sudo Exploits: Para aprovechar configuraciones incorrectas de sudo y obtener acceso root.
        Manipulación de scripts automatizados: Aprovechamiento de scripts ejecutados con privilegios elevados.

Proceso
Paso 1: Reconocimiento

En la fase de reconocimiento, el objetivo fue identificar la máquina objetivo y obtener información clave sobre los servicios en ejecución.

    Identificación de la máquina objetivo:
    Se utilizó arp-scan para detectar la dirección IP de la máquina objetivo, que resultó ser 192.168.1.15.

    Escaneo de puertos:
    Utilizando nmap, se realizó un escaneo exhaustivo para identificar puertos abiertos:

    nmap -sV -sVC 192.168.1.15

    Puertos abiertos identificados:
        21/tcp (FTP): Posible punto de entrada para obtener acceso al sistema.
        22/tcp (SSH): Requiere autenticación, pero susceptible a ataques de fuerza bruta.
        80/tcp (HTTP): Servidor web activo, se realizó un análisis adicional para buscar posibles vulnerabilidades.

Paso 2: Análisis de Vulnerabilidades

Una vez identificados los servicios, se procedió a analizar sus configuraciones y posibles vulnerabilidades.

    FTP:
    Se observó que el servicio FTP estaba configurado sin autenticación en algunos directorios, lo que permitió la carga de archivos. Esto permitió la creación de un archivo malicioso en el sistema.

    SSH:
    Aunque SSH requería autenticación, se utilizó hydra para ejecutar un ataque de fuerza bruta, lo que permitió obtener las credenciales del servicio SSH.

    HTTP (Servidor web):
    Se utilizó Dirbuster para realizar un escaneo de directorios en el servidor web. Se identificaron directorios ocultos como /admin y /private, lo que abrió más puertas para la explotación.

Paso 3: Explotación

En esta fase, las vulnerabilidades identificadas fueron explotadas para obtener acceso no autorizado al sistema.

    Acceso inicial (FTP):
    Se explotó la vulnerabilidad en el servicio FTP para cargar un archivo malicioso. A través de esto, se logró ejecutar comandos remotos en el sistema.

    Ataque de fuerza bruta en SSH:
    Utilizando hydra, se ejecutó un ataque de fuerza bruta para obtener credenciales SSH (usuario: admin, contraseña: 12345). Este acceso permitió el ingreso al servidor con privilegios limitados.

    Acceso al servidor web:
    A través de la explotación de directorios ocultos en el servidor web, se obtuvo acceso a información sensible que permitió avanzar en la explotación.

Paso 4: Escalación de Privilegios

Una vez obtenido acceso básico al sistema, se procedió a elevar los privilegios para obtener acceso completo al sistema.

    Exploits de sudo:
    Se descubrió que el usuario con el que se tenía acceso tenía configuraciones incorrectas en sudo. Esto permitió ejecutar comandos como root sin ser desautorizado.

    Manipulación de scripts:
    Se identificó un script ejecutado con privilegios de root cada 60 segundos, que podía ser modificado para ejecutar comandos maliciosos. Esto permitió escalar privilegios y obtener control total del sistema.

Paso 5: Obtención de las Banderas

Una vez obtenido acceso completo al sistema, se buscó y extrajo las banderas utilizando el siguiente comando:

find / -name bandera*.txt 2>/dev/null

Las banderas fueron localizadas y confirmadas con éxito:

    Bandera 1: ~/bandera1.txt
    Bandera 2: /root/bandera2.txt

Ambas banderas confirmaron el éxito del ataque y la explotación exitosa de las vulnerabilidades del sistema.
Recomendaciones de Seguridad

Basado en las vulnerabilidades explotadas durante el reto, se proponen las siguientes recomendaciones para mejorar la seguridad de los sistemas en entornos reales:

    Deshabilitar servicios innecesarios:
    Desactivar servicios como FTP cuando no sean necesarios, y asegurar que cualquier servicio expuesto esté debidamente configurado y protegido.

    Uso de contraseñas fuertes:
    Evitar el uso de contraseñas simples y predecibles. Implementar políticas de contraseñas robustas en todos los servicios críticos, como SSH y FTP.

    Revisión de configuraciones de sudo:
    Es fundamental revisar y restringir el acceso a sudo para evitar la escalación de privilegios. Ningún usuario debe tener acceso a privilegios elevados sin una necesidad justificada.

    Monitoreo de scripts automatizados:
    Los scripts que se ejecutan con privilegios elevados deben ser monitoreados y auditados periódicamente para prevenir modificaciones no autorizadas.

Contribuciones

Este reto forma parte de un ejercicio educativo de Ethical Hacking. Las contribuciones para mejorar la metodología de explotación, la automatización de la explotación de vulnerabilidades, y la mejora de la seguridad en general son bienvenidas. Puedes realizar pull requests o abrir issues para discutir posibles mejoras.
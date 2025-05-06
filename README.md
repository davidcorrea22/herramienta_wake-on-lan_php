# HERRAMIENTA WAKE ON LAN + PHP
Esta es una herramienta online creada para encender equipos de forma remota utilizando el protocolo Wake-on-LAN y los lenguajes PHP y Python.
La herramienta crea una página web que actúa de panel de control a la que se puede acceder desde el equipo local y desde otros dispositivos de la misma red.
Se recomienda que el servidor sea un equipo con Windows 10 o Windows 11.

# REQUISITOS
1. Instalar Docker Desktop: https://www.docker.com/products/docker-desktop

2. Tener al menos dos equipos:
    - Uno como servidor: Donde se hace la instalación de la herramienta.
    - Al menos un cliente: No necesitan ninguna instalación.
- El cliente debe estar configurado para recibir páquetes mágicos: https://www.xataka.com/basics/wake-on-lan-que-como-configurarlo-windows-10

3. Para acceder a la herramienta desde otros equipos de la red, habilita el puerto 80 con este comando: 
    - netsh advfirewall firewall add rule name="Abrir puerto 80" dir=in action=allow protocol=TCP localport=80

# INSTALACIÓN
1. Se recomienda descomprimir la herramienta en la raiz del sistema.
2. ⚠ PARA QUE LA HERRAMIENTA FUNCIONE. MODIFIQUE EL VALOR DE LA VARIABLE "BROADCAST_IP" EN EL ARCHIVO docker-compose.yml. ESPECIFIQUE AHÍ LA DIRECCIÓN BROADCAST DE SU RED. ⚠
3. Asegurese que los servicios Docker estén activos.
4. Abra una terminal CMD en la carpeta principal de la herramienta y levante el Docker usando: docker compose up --build
5. Si todo se ha instalado correctamente. Acceda a http://localhost o http://{ip_del_equipo_servidor} desde cualquier equipo

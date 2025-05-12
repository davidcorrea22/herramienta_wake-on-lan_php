# HERRAMIENTA WAKE ON LAN + PHP + PYTHON
Esta es una herramienta online creada para encender equipos de forma remota usando el protocolo Wake-on-LAN y los lenguajes PHP y Python.
La herramienta crea una página web en el puerto 80 que actúa como panel de control, esta es accesible desde todos los equipos con conectividad al servidor.
Esto incluye también dispositivos móviles.
Se recomienda que el servidor sea un equipo con Windows 10 o Windows 11 y que la carpeta zip se descomprima en C:\PROYECTO_WOL.

# REQUISITOS
- Docker Desktop: https://www.docker.com/products/docker-desktop
- Al menos dos equipos físicos (no máquinas virtuales):
    - Uno como servidor: Donde se hace la instalación de la herramienta.
    - Al menos un cliente: No necesitan ninguna instalación.
    - El cliente debe estar configurado para recibir páquetes mágicos: https://www.xataka.com/basics/wake-on-lan-que-como-configurarlo-windows-10

- Habilite el puerto 80 en el equipo servidor. Puede usar este comando: netsh advfirewall firewall add rule name="Abrir puerto 80" dir=in action=allow protocol=TCP localport=80
- Aseguresé de instalar este repositorio: git clone https://github.com/davidcorrea22/herramienta_wake-on-lan_php

# INSTALACIÓN
- ⚠ PARA QUE LA HERRAMIENTA FUNCIONE. CAMBIE EL VALOR DE "BROADCAST_IP" EN EL ARCHIVO docker-compose.yml (línea 29). ESPECIFIQUE AHÍ LA DIRECCIÓN BROADCAST DE SU RED. ⚠
- Asegurese que Docker esté activo.
- Abra una terminal CMD, dirigase a C:\PROYECTO_WOL y levante el Docker usando: docker compose up --build
- Acceda a http://localhost o http://{ip_del_equipo_servidor} desde cualquier equipo, debería ver el panel de control.
- El usuario y la contraseña inicial son "administrador". Se recomienda eliminar este usuario una vez se haya añadido otro.

# CARACTERISTICAS
- Panel de control interactivo
- Herramientas para añadir, borrar y editar equipos
- Función para programar un encendido global
- Administración de usuarios
- Se puedes crean más usuarios, administradores o estándar.

# ADVERTENCIA
- Esta heramienta está diseñada para ser instalada en equipos servidores que no vayan a apagarse con frecuencia. Si se reinicia el equipo servidor, REINICIE los contenedores, vuelva a levantarlos con docker compose up --build o ejecute manualmente el archivo init.sh o script_bucle.php para que la programación automática de encendido de equipos vuelva a funcionar.

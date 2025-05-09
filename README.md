# HERRAMIENTA WAKE ON LAN + PHP + PYTHON
Esta es una herramienta online creada para encender equipos de forma remota con el protocolo Wake-on-LAN y los lenguajes PHP y Python.
La herramienta crea una página web en el puerto 80 que actúa como panel de control.
Se recomienda que el servidor sea un equipo con Windows 10 o Windows 11 y que la carpeta zip se descomprima en C:\PROYECTO_WOL.

# REQUISITOS
1. Docker Desktop: https://www.docker.com/products/docker-desktop

2. Al menos dos equipos:
    - Uno como servidor: Donde se hace la instalación de la herramienta.
    - Al menos un cliente: No necesitan ninguna instalación.
    - El cliente debe estar configurado para recibir páquetes mágicos: https://www.xataka.com/basics/wake-on-lan-que-como-configurarlo-windows-10

3. Habilite el puerto 80 en CMD con este comando: netsh advfirewall firewall add rule name="Abrir puerto 80" dir=in action=allow protocol=TCP localport=80

4. Aseguresé de instalar este repositorio: git clone https://github.com/davidcorrea22/herramienta_wake-on-lan_php

# INSTALACIÓN
1. ⚠ PARA QUE LA HERRAMIENTA FUNCIONE. CAMBIE EL VALOR DE "BROADCAST_IP" EN EL ARCHIVO docker-compose.yml (línea 29). ESPECIFIQUE AHÍ LA DIRECCIÓN BROADCAST DE SU RED. ⚠

2. Asegurese que Docker esté activo.

3. Abra una terminal CMD, dirigase a C:\PROYECTO_WOL y levante el Docker usando: docker compose up --build

4. Si todo se ha instalado correctamente. Acceda a http://localhost o http://{ip_del_equipo_servidor} desde cualquier equipo, debería ver el panel de control.

5. El usuario y la contraseña inicial son "administrador". Se recomienda eliminar este usuario una vez se haya añadido otro.

# CARACTERISTICAS
- Panel de control interactivo
- Herramientas para añadir, borrar y editar equipos
- Función para programar un encendido global
- Administración de usuarios
- Se puedes crean más usuarios, administradores o estándar.

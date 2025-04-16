GUÍA COMPLETA para conectar tu repositorio local a GitHub y subir archivos
✅ Paso 1: Crear el repositorio en GitHub
Iniciá sesión en GitHub:
👉 https://github.com/login

En la esquina superior derecha, hacé clic en el botón "+" → seleccioná "New repository".

Completá el formulario así:

Repository name: syslinux-guide

Descripción (opcional): Guía paso a paso para instalar SYSLINUX en un dispositivo USB

Visibility: Marcá Public

❌ No marques las opciones de README, .gitignore ni license.

Hacé clic en el botón verde "Create repository".

Una vez creado, GitHub te mostrará la URL del repositorio. Va a ser algo así como:

bash
Copy
Edit
https://github.com/war132812/syslinux-guide.git
✅ Paso 2: Conectar tu repositorio local al repositorio remoto en GitHub
Abrí tu terminal y ubicáte en la carpeta donde tenés tu guía (por ejemplo, /home/war13):

bash
Copy
Edit
cd /home/war13
Ahora ejecutá este comando para agregar el remoto:

bash
Copy
Edit
git remote add origin https://github.com/war132812/syslinux-guide.git
Si querés verificar que se haya agregado correctamente, usá:

bash
Copy
Edit
git remote -v
✅ Paso 3: Subir tu guía con Git
Si aún no lo hiciste, asegurate de que guia-syslinux.md esté en esa carpeta.

Inicializá el repositorio local (si no lo habías hecho):

bash
Copy
Edit
git init
Agregá el archivo:

bash
Copy
Edit
git add guia-syslinux.md
Hacé el primer commit:

bash
Copy
Edit
git commit -m "Añadir guía paso a paso para instalar SYSLINUX en un dispositivo USB"
Subí los archivos a GitHub:

bash
Copy
Edit
git push --set-upstream origin master
🔐 ¿Qué pasa cuando Git pide usuario y contraseña?
Como GitHub ya no permite contraseñas normales, debés usar un Token Personal de Acceso (PAT).

¿Cómo obtener un token?
Entrá a https://github.com/settings/tokens

Hacé clic en el botón "Generate new token"

Elegí permisos básicos:

repo ✅

Copiá ese token y guardalo (es como tu contraseña)

💡 ¡No lo compartas! Ni lo pegues en público, ni aquí.

Cuando Git te lo pida:
Usuario: tu usuario de GitHub (ej. war132812)

Contraseña: el token que generaste

✅ Paso 4 (opcional): Recordar tu token en el sistema
Para no tener que escribirlo cada vez:

bash
Copy
Edit
git config --global credential.helper cache
🎉 ¡Listo! Ahora tu archivo ya está subido a GitHub
Podés entrar a tu repo y ver el archivo en línea en:
👉 https://github.com/war132812/syslinux-guide

Guía Paso a Paso para Utilizar SYSLINUX

SYSLINUX es un gestor de arranque diseñado para sistemas Linux en medios FAT (USB, disquetes, discos duros). Esta guía cubre su instalación, configuración y uso.



1. ¿Qué es SYSLINUX?
SYSLINUX es un cargador de arranque que permite iniciar Linux desde:
    • Disquetes FAT (SYSLINUX).
    • CD/DVD (ISOLINUX).
    • Red PXE (PXELINUX).
    • Particiones ext2/3/4 (EXTLINUX).
Ventajas:
    • No requiere instalación en el MBR.
    • Configuración simple mediante syslinux.cfg.
    • Soporte para menús gráficos (vesamenu.c32).

2. Instalación de SYSLINUX
Requisitos:
    • Un dispositivo con Instalación en Windowssistema de archivos FAT (USB, disco, etc.).
    • Kernel de Linux (vmlinuz) y initrd (si es necesario).




Pasos para Instalar SYSLINUX en un USB (Linux)
    1. Formatear el USB en FAT32:
       sudo mkfs.vfat -F32 /dev/sdX
       (Reemplaza /dev/sdX con tu dispositivo USB, verifica con lsblk).
       
    2. Montar el USB:
       sudo mount /dev/sdX /mnt
       
    3. Instalar SYSLINUX:
       sudo syslinux --install /dev/sdX
       (Para versiones modernas, usa --directory si necesitas una ruta personalizada).
       
    4. Copiar archivos necesarios:
       cp /ruta/al/kernel/vmlinuz /mnt/
       cp /ruta/al/initrd.img /mnt/
       
    5. Desmontar:
       sudo umount /mnt









Instalación en Windows
    1. Descarga syslinux.exe desde syslinux.org.
    2. Ejecuta en CMD (ejemplo para unidad E:):
       syslinux.exe -m -a -d /boot/syslinux E:

3. Configuración de syslinux.cfg
Crea o edita el archivo syslinux.cfg en la raíz del dispositivo (o en /boot/syslinux/).
Ejemplo Básico:
plaintext
DEFAULT linux
LABEL linux
  KERNEL vmlinuz
  APPEND root=/dev/sda1 ro initrd=initrd.img
Opciones Avanzadas:
    • Menú Gráfico (vesamenu.c32):
      plaintext
      
      UI vesamenu.c32
      MENU TITLE Menú de Arranque
      LABEL Debian
        MENU LABEL Debian 12
        KERNEL vmlinuz
        APPEND root=/dev/sda1 ro initrd=initrd.img
      LABEL Rescue
        MENU LABEL Modo Rescate
        KERNEL vmlinuz
        APPEND root=/dev/sda1 single
    • Tiempo de espera:
      plaintext
    • TIMEOUT 50  # 5 segundos
    • Consola Serial:
      plaintext
      
      SERIAL 0 115200


4. Personalización

Módulos Útiles:
Módulo
Descripción
menu.c32
Menú básico.
vesamenu.c32
Menú gráfico (requiere VESA).
chain.c32
Arranque en cadena (Windows).
Ejemplo con Módulos:
plaintext

UI vesamenu.c32
MENU BACKGROUND splash.png
LABEL Windows
  COM32 chain.c32
  APPEND hd0 1














5. Solución de Problemas
Errores Comunes:
    1. "Could not find kernel image":
        ◦ Verifica que vmlinuz esté en la ruta correcta.
        ◦ Usa rutas absolutas en syslinux.cfg (ej: /boot/vmlinuz).
    2. "Invalid or corrupt kernel image":
        ◦ Asegúrate de que el kernel sea compatible (bzImage).
    3. Problemas con BIOS/UEFI:
        ◦ Para UEFI, usa syslinux-efi o GRUB.
        ◦ En BIOS antiguas, usa -s (modo seguro):
          
          syslinux -s /dev/sdX

6. Comandos Útiles
Comando
Descripción
syslinux --install
Instala SYSLINUX en el dispositivo.
syslinux --update
Actualiza una instalación existente.
syslinux --stupid
Modo compatible con BIOS antiguas.





Conclusión
SYSLINUX es una herramienta poderosa para crear medios de arranque personalizados. Con esta guía, puedes:
    1. Instalar SYSLINUX en USB/disquetes.
    2. Configurar syslinux.cfg para múltiples opciones de arranque.
    3. Personalizar menús y ajustes avanzados.
Recursos:
    • Documentación Oficial
    • Ejemplos de Configuración


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


<p align="center">
  <img src="https://github.com/BalantryFernando/guia-personalizacion-terminal-linux/blob/main/banner.png?raw=true" alt="Mi Banner Profesional" width="1200">
</p>

# Guía Completa para Personalizar tu Terminal en Linux 🐧✨

## ¡Hola! 👋 ¿Cansado de la típica terminal en blanco y negro? En esta guía, te mostraré cómo transformar tu aburrida terminal en un entorno de trabajo potente, visualmente atractivo y, sobre todo, **tuyo**.

Pasaremos por tres niveles de personalización:
1.  **Banner de Bienvenida con Arte ASCII**: Un toque personal para recibirte cada vez que abres la terminal.
2.  **Potenciar la Shell con Oh My Bash**: Llevaremos la funcionalidad al siguiente nivel con temas, plugins y más.
3.  **Fondo de Pantalla y Transparencia**: La guinda del pastel para una integración perfecta con tu escritorio.

![Ejemplo de Terminal Personalizada](URL_DE_TU_IMAGEN_TERMINAL_FINAL.png)
*(Reemplaza la URL de arriba con un enlace a tu captura de pantalla final)*

---

## Parte 1: El Banner de Bienvenida (Arte ASCII)

Esta es la forma más sencilla de darle un toque único a tu terminal.

### Paso 1: Identificar tu Archivo de Configuración

Primero, necesitas saber qué shell estás usando para localizar el archivo de configuración correcto. Ejecuta:

```bash
echo $SHELL
```

El resultado te dirá qué shell usas. Los archivos más comunes son:
* Si la salida es `/bin/bash` o similar, tu archivo es `~/.bashrc`.
* Si la salida es `/bin/zsh` o similar, tu archivo es `~/.zshrc`.
* Si usas Fish, el archivo será `~/.config/fish/config.fish`.

### Paso 2: Generar tu Arte ASCII

Ahora viene la parte divertida. Convierte cualquier texto o incluso imágenes en arte ASCII usando estas herramientas online:

* **Para Texto**: [**patorjk.com/software/taag**](https://patorjk.com/software/taag/#p=display&h=0&v=0&f=Colossal&t=Activos%20%0A%20%20%20%20%20%2024%2F7%20)
* **Para Imágenes**: [**convertcase.net/ascii-art-generator**](https://convertcase.net/ascii-art-generator/)

Diseña tu banner, ajústalo a tu gusto y copia el resultado.

### Paso 3: Preparar el Código para la Terminal

Tu arte ASCII es solo texto. Para que la terminal lo imprima línea por línea, debes añadir el comando `echo` al principio de cada una.

**Ejemplo:**
Si tu arte es:
```
  _   _
 | \ | |
 |  \| |
```

Debes transformarlo en:
```bash
echo "   _   _  "
echo "  | \ | | "
echo "  |  \| | "
```

> **💡 Consejo de Automatización**: Hacer esto manualmente es tedioso para diseños grandes. Usa la función de buscar y reemplazar de tu editor de código (como VS Code). Para evitar la tediosa **iteración** de añadir `echo` manualmente, puedes buscar el inicio de cada línea (`^`) y reemplazarlo por `echo "`. Luego, añade una comilla `"` al final de cada línea.

### Paso 4: Añadir el Banner a tu Configuración

Abre tu archivo de configuración (`.bashrc`, `.zshrc`, etc.) con un editor como `nano`:

```bash
nano ~/.bashrc
```

Desplázate hasta el **final del archivo** y pega todas las líneas con `echo` que preparaste. 
<p align="center">
  <img src="https://github.com/BalantryFernando/guia-personalizacion-terminal-linux/blob/main/comamds.png?raw=true" alt="Mi Banner Profesional" width="1200">
</p>
Guarda los cambios (**Ctrl + O**) y sal del editor (**Ctrl + X**).
¡La próxima vez que abras una terminal, verás tu banner!

---

## Parte 2: Potenciando la Shell con Oh My Bash y Powerline

Si quieres ir más allá de la estética y mejorar la funcionalidad, **Oh My Bash** es para ti.

### Paso 1: Instalar Prerrequisitos (Git y Curl)

Asegúrate de tener `git` y `curl` instalados.

```bash
# Comprobar si existen
git --version
curl --version

# Si no, instalarlos (para sistemas basados en Debian/Ubuntu)
sudo apt update
sudo apt install git curl -y
```

### Paso 2: Instalar Oh My Bash

Usa el script oficial de instalación. Pega y ejecuta el siguiente comando en tu terminal:

```bash
bash -c "$(curl -fsSL [https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh](https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh))"
```

Esto instalará Oh My Bash y creará una copia de seguridad de tu `.bashrc` actual.

### Paso 3: Instalar las Fuentes Powerline

El tema que usaremos, **Agnoster** (emulado con `powerline`), necesita fuentes especiales para mostrar correctamente los iconos y símbolos.

```bash
# 1. Clonar el repositorio de fuentes
git clone [https://github.com/powerline/fonts.git](https://github.com/powerline/fonts.git) --depth=1

# 2. Entrar al directorio y ejecutar el instalador
cd fonts
./install.sh

# 3. Limpiar los archivos descargados
cd ..
rm -rf fonts
```

### Paso 4: Activar el Tema Powerline

Ahora, edita tu archivo `.bashrc` para establecer el nuevo tema.

```bash
nano ~/.bashrc
```

Busca la línea que dice `OSH_THEME="..."` (normalmente está cerca del principio) y cámbiala por:

```bash
OSH_THEME="powerline"
```

Guarda (**Ctrl + O**) y sal (**Ctrl + X**). Reinicia tu terminal para ver los cambios.
<p align="center">
  <img src="https://github.com/BalantryFernando/guia-personalizacion-terminal-linux/blob/main/banner.png?raw=true" alt="Mi Banner Profesional" width="1200">
</p>
---

## Parte 3: Fondo de Pantalla y Transparencia con Tilix (Para Ubuntu y otros SO)

Si tu entorno de escritorio no es KDE Plasma, la forma más sencilla de añadir un fondo de pantalla y gestionar la transparencia es usando un emulador de terminal avanzado como **Tilix**.

### Paso 1: Instalar Tilix

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install tilix -y
```

### Paso 2: Habilitar la Configuración de Fondo en Tilix

Para que Tilix pueda manejar fondos, a veces es necesario un pequeño ajuste.

1.  **Identifica el script de VTE**: Mira qué archivo de configuración de terminal tienes disponible.
    ```bash
    ls /etc/profile.d/
    ```
    Busca un archivo como `vte-2.91.sh` o `vte.sh`. Anota el nombre exacto.

2.  **Edita tu `.bashrc`**: Abre el archivo `nano ~/.bashrc` y añade el siguiente bloque de código **al principio del todo**.
    ```bash
    if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
        source /etc/profile.d/vte-2.91.sh
    fi
    ```
    *Asegúrate de reemplazar `vte-2.91.sh` por el nombre de archivo que encontraste en el paso anterior.*

3.  **Guarda y cierra** el archivo.

> **❓ ¿No encuentras el archivo `vte`?** Si el primer comando no devuelve nada, reinstala la librería VTE con `sudo apt install --reinstall libvte-2.91-common` y vuelve a intentarlo.

### Paso 3: Configurar la Apariencia en Tilix

1.  Abre **Tilix**.
2.  Haz clic derecho en cualquier parte de la terminal y ve a `Perfiles` -> `Editar Perfil`.
3.  Ve a la pestaña `Apariencia`.
4.  Aquí puedes:
    * Activar la opción **"Usar imagen de fondo"** y seleccionar el archivo que quieras.
    * Ajustar el control deslizante de **"Transparencia"** para que el fondo de tu escritorio sea visible.

¡Y listo! Ya tienes una terminal completamente personalizada, funcional y con un aspecto increíble.

---
Si te ha gustado esta guía, ¡dale una ⭐ al repositorio!

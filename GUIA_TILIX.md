# Guía: Fondo de Pantalla y Transparencia con Tilix 🖼️

Este documento es un anexo a la [Guía Completa para Personalizar tu Terminal en Linux](README.md). Aquí nos centraremos exclusivamente en cómo instalar y configurar el emulador de terminal **Tilix** para añadir una imagen de fondo y ajustar la transparencia, especialmente en entornos de escritorio como GNOME (Ubuntu), XFCE o Cinnamon, donde no es una opción nativa sencilla.

**Tilix** es un potente emulador de terminal que ofrece funcionalidades avanzadas, como la división de paneles (tiling) y una personalización profunda.

![Ejemplo de Tilix con fondo](URL_DE_TU_IMAGEN_DE_TILIX.png)
*(Reemplaza la URL de arriba con un enlace a tu captura de pantalla de Tilix)*

---

## Paso 1: Instalación de Tilix

Si aún no lo tienes, puedes instalar Tilix fácilmente desde los repositorios oficiales de la mayoría de las distribuciones. Para sistemas basados en Debian/Ubuntu:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install tilix -y
```

Una vez instalado, puedes abrirlo desde tu menú de aplicaciones.

## Paso 2: Habilitar el Soporte para Fondos de Pantalla

En algunas configuraciones, Tilix necesita que se cargue un script específico al iniciar la shell para que la opción de fondo de pantalla funcione correctamente.

### 1. Identificar el script de VTE
Primero, vamos a comprobar qué archivo de configuración de VTE (la librería gráfica sobre la que se construyen muchas terminales) tienes en tu sistema.

Abre una terminal y ejecuta:
```bash
ls /etc/profile.d/
```
Busca en la lista un archivo que empiece por `vte`. Los nombres más comunes son:
* `vte-2.91.sh` (muy común en versiones recientes de Ubuntu)
* `vte.sh`

Apunta el nombre exacto que te aparece.

### 2. Editar el archivo `.bashrc`
Ahora, vamos a decirle a tu terminal que cargue ese script al iniciar.

Abre el archivo `.bashrc` con un editor de texto:
```bash
nano ~/.bashrc
```
Añade el siguiente bloque de código **al principio del todo** en el archivo. Es muy importante que esté al inicio.

```bash
if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
    source /etc/profile.d/[NOMBRE_DEL_ARCHIVO_QUE_ENCONTRASTE]
fi
```
**Importante**: Reemplaza `[NOMBRE_DEL_ARCHIVO_QUE_ENCONTRASTE]` por el nombre que encontraste en el paso anterior. Por ejemplo, si encontraste `vte-2.91.sh`, el bloque debe quedar así:
```bash
if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
    source /etc/profile.d/vte-2.91.sh
fi
```

### 3. Guardar y Finalizar
Dentro de `nano`, presiona **Ctrl + O** para guardar y luego **Enter** para confirmar. Presiona **Ctrl + X** para salir del editor.

Cierra completamente todas las ventanas de Tilix y vuelve a abrirlo para que los cambios surtan efecto.

> **❓ ¿Qué hago si no encuentro ningún archivo `vte`?**
> Si en el primer paso no aparece ningún archivo llamado `vte.sh` o similar, significa que la librería no instaló correctamente su script de perfil. Ejecuta este comando para reinstalarla y crearlo:
> ```bash
> sudo apt install --reinstall libvte-2.91-common
> ```
> Después de que termine, vuelve al punto 1 y verás que el archivo ya existe. Luego, continúa con el resto de la guía.

## Paso 3: Aplicar el Fondo y la Transparencia en Tilix

Con la configuración ya lista, aplicar los cambios visuales es muy sencillo:

1.  Abre una nueva ventana de **Tilix**.
2.  Haz **clic derecho** en cualquier parte de la terminal.
3.  En el menú contextual, ve a `Perfiles` -> `Editar Perfil`.
4.  Se abrirá una ventana de configuración. Ve a la pestaña **`Apariencia`**.
5.  Aquí encontrarás las opciones:
    * **Fondo**: Marca la casilla **"Usar imagen de fondo"** y selecciona el archivo de imagen que deseas usar.
    * **Transparencia**: Mueve el deslizador de **"Transparencia"** hasta encontrar el nivel que más te guste.
      ##👀  Cambiar la transparencia aveces es necesario para que se muestre tu imagen de fondo 👀## 

¡Y eso es todo! Has configurado Tilix para tener una apariencia totalmente personalizada e integrada con tu escritorio.

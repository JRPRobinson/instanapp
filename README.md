# Instanapp ![Estado](https://img.shields.io/badge/estado-BETA-orange)

Instalación y configuración de apps externas por medio del terminal.

> **Proyecto en fase BETA**
> Instanapp todavía no tiene todas las funcionalidades previstas. Por ahora cuenta con pocas opciones, y las iré desarrollando poco a poco. Puede haber cambios en el uso y en las opciones disponibles entre versiones.

Instanapp es un script en Bash que toma un archivo comprimido de una aplicación (por ejemplo, Postman descargado como `.tar.gz`), lo instala en `/opt` y crea automáticamente el lanzador `.desktop`. Así la app aparece en el menú de aplicaciones de tu escritorio sin que tengas que configurar nada a mano.

## Características

- Extrae archivos `.zip`, `.tar.gz`, `.tar.xz`, `.tar.bz2` y `.tar`.
- Instala la aplicación en `/opt/<NombreApp>`.
- Detecta automáticamente el ejecutable principal. Si hay varios candidatos, te deja elegir uno.
- Busca un icono (`.png` o `.svg`) dentro de la app y usa el de mayor tamaño.
- Crea el archivo `.desktop` en `~/.local/share/applications`.
- Si no indicas la ruta completa, busca el archivo en `~/Downloads`.

## Requisitos

- Linux con entorno de escritorio (GNOME, KDE, XFCE, etc.)
- `bash`
- `sudo`
- `unzip`
- `tar`
- `file`
- `update-desktop-database` (paquete `desktop-file-utils`)

## Instalación

```bash
git clone https://github.com/JRPRobinson/instanapp.git
cd instanapp
chmod +x instanapp.sh
```

> Cambia `instanapp.sh` por el nombre real de tu script si es otro.

## Uso

```bash
./instanapp.sh [-i archivo] [-u] [-h]
```

| Opción | Descripción |
|--------|-------------|
| `-i archivo` | Instala la aplicación en `/opt` y crea el `.desktop` |
| `-u` | Busca actualizaciones *(aún no implementada)* |
| `-h` | Muestra la ayuda |

### Ejemplos

Instalar una app desde un archivo en `~/Downloads`:

```bash
./instanapp.sh -i postman-linux-x64.tar.gz
```

Instalar usando una ruta completa:

```bash
./instanapp.sh -i /ruta/a/mi-app.zip
```

## ¿Cómo funciona?

1. **Localiza el archivo**: usa la ruta indicada o lo busca en `~/Downloads`.
2. **Detecta el tipo** de archivo y lo extrae en una carpeta temporal.
3. **Mueve la app a `/opt`**: si el archivo trae una sola carpeta, usa su nombre. Si no, deduce el nombre a partir del archivo (por ejemplo, `postman-linux-x64.tar.gz` pasa a ser `Postman`).
4. **Busca el ejecutable** cuyo nombre coincida con el de la app. Si hay varios candidatos, te pide elegir.
5. **Busca el icono** más grande dentro de la carpeta de la app.
6. **Genera el `.desktop`** en `~/.local/share/applications` y actualiza la base de datos de lanzadores.

## Notas

- Se usa `sudo` para escribir en `/opt`, por lo que te pedirá tu contraseña.
- Si ya existe una app con el mismo nombre en `/opt`, será reemplazada.
- Los tipos de archivo no soportados se rechazan con un mensaje de error.

## Estado del proyecto

Instanapp se encuentra en **BETA**: las opciones disponibles son limitadas y el proyecto seguirá creciendo con nuevas funcionalidades.

**Disponible:**
- [x] Instalación desde archivos comprimidos (`-i`)
- [x] Creación automática del lanzador `.desktop`
- [x] Ayuda (`-h`)

**En desarrollo / planeado:**
- [ ] Comprobación de actualizaciones (`-u`) *(la opción existe, pero aún no hace nada)*
- [ ] Desinstalación de apps
- [ ] Listado de apps instaladas
- [ ] Soporte para AppImage y `.deb`

Si tienes ideas o encuentras errores, puedes abrir un [issue](https://github.com/JRPRobinson/instanapp/issues).

## Contribuir

1. Haz un fork del proyecto
2. Crea una rama (`git checkout -b feature/mi-mejora`)
3. Haz commit de tus cambios (`git commit -m "Agrega mi mejora"`)
4. Haz push (`git push origin feature/mi-mejora`)
5. Abre un Pull Request

## Licencia

Distribuido bajo la licencia MIT. Consulta el archivo `LICENSE` para más información.

## Autor

**JRPRobinson** - [GitHub](https://github.com/JRPRobinson)

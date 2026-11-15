# Instanapp ![Estado](https://img.shields.io/badge/estado-BETA-orange)

Instalación y configuración de apps externas por medio del terminal.

> **Proyecto en fase BETA**
> Instanapp todavía no tiene todas las funcionalidades previstas. Por ahora cuenta con pocas opciones, y las iré desarrollando poco a poco. Puede haber cambios en el uso y en las opciones disponibles entre versiones.

Instanapp es un script en Bash que toma un archivo comprimido de una aplicación (por ejemplo, Postman descargado como `.tar.gz`), lo instala en `/opt` y crea automáticamente el lanzador `.desktop`. Así la app aparece en el menú de aplicaciones de tu escritorio sin que tengas que configurar nada a mano. También puede listar las apps que instaló y purgarlas cuando ya no las necesites.

## Características

- Extrae archivos `.zip`, `.tar.gz`, `.tar.xz`, `.tar.bz2` y `.tar`.
- Instala la aplicación en `/opt/<NombreApp>`.
- Detecta automáticamente el ejecutable principal. Si hay varios candidatos, te deja elegir uno.
- Busca un icono (`.png` o `.svg`) dentro de la app y usa el de mayor tamaño.
- Crea el archivo `.desktop` en `~/.local/share/applications`.
- Si no indicas la ruta completa, busca el archivo en `~/Downloads`.
- Lleva un registro de las apps instaladas con Instanapp (`~/.local/share/instanapp/instanapp_apps.txt`).
- Lista las apps instaladas y permite purgarlas (elimina la carpeta de `/opt` y su lanzador).

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
./instanapp.sh [-i archivo] [-l] [-p nombre] [-h]
```

| Opción | Descripción |
|--------|-------------|
| `-i archivo` | Instala la aplicación en `/opt` y crea el `.desktop` |
| `-l` | Lista las apps instaladas con Instanapp |
| `-p nombre` | Purga la app indicada (borra su carpeta en `/opt` y su `.desktop`) |
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

Ver las apps instaladas con Instanapp:

```bash
./instanapp.sh -l
```

Purgar una app (usa el nombre tal como aparece en `-l`, que coincide con su carpeta en `/opt`):

```bash
./instanapp.sh -p Postman
```

## ¿Cómo funciona?

1. **Localiza el archivo**: usa la ruta indicada o lo busca en `~/Downloads`.
2. **Detecta el tipo** de archivo y lo extrae en una carpeta temporal.
3. **Mueve la app a `/opt`**: si el archivo trae una sola carpeta, usa su nombre. Si no, deduce el nombre a partir del archivo (por ejemplo, `postman-linux-x64.tar.gz` pasa a ser `Postman`).
4. **Busca el ejecutable** cuyo nombre coincida con el de la app. Si hay varios candidatos, te pide elegir.
5. **Busca el icono** más grande dentro de la carpeta de la app.
6. **Genera el `.desktop`** en `~/.local/share/applications` y actualiza la base de datos de lanzadores.
7. **Registra la app** en la lista de Instanapp, para poder listarla o purgarla después.

## Notas

- Se usa `sudo` para escribir y borrar en `/opt`, por lo que te pedirá tu contraseña.
- Si ya existe una app con el mismo nombre en `/opt`, será reemplazada.
- Los tipos de archivo no soportados se rechazan con un mensaje de error.
- Solo se pueden purgar las apps que fueron instaladas con Instanapp (las que aparecen en `-l`).
- La purga es definitiva: elimina la carpeta completa de la app en `/opt`.

## Estado del proyecto

Instanapp se encuentra en **BETA**: las opciones disponibles son limitadas y el proyecto seguirá creciendo con nuevas funcionalidades.

**Disponible:**
- [x] Instalación desde archivos comprimidos (`-i`)
- [x] Creación automática del lanzador `.desktop`
- [x] Listado de apps instaladas (`-l`)
- [x] Purga de apps instaladas (`-p`)
- [x] Ayuda (`-h`)

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

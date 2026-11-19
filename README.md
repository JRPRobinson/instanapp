<p align="center">
  <img src="assets/logo.svg" alt="Logo de instanapp" width="320">
</p>

<h1 align="center">Instanapp</h1>

<p align="center">
  <img src="https://img.shields.io/badge/versión-1.0.0-brightgreen" alt="Versión">
  <img src="https://img.shields.io/badge/licencia-MIT-blue" alt="Licencia">
</p>

<p align="center">Instalación y configuración de apps externas desde la terminal.</p>

> **🚧 En desarrollo activo**
> Instanapp ya es usable, pero el script se irá modificando poco a poco ya que me encuentro trabajando y tengo poco tiempo para el desarrollo.

Instanapp es un script en Bash que toma el archivo comprimido de una aplicación (por ejemplo, Postman descargado como `.tar.gz`), la instala en `/opt` y crea automáticamente el lanzador `.desktop`. Así la app aparece en el menú de aplicaciones sin configurar nada a mano. También lista las apps que instaló y las purga cuando ya no las necesites.

## Características

- Extrae archivos `.zip`, `.tar.gz`, `.tar.xz`, `.tar.bz2` y `.tar`.
- Muestra una barra de progreso estilo pacman durante la extracción.
- Instala la aplicación en `/opt/<NombreApp>`.
- Detecta el ejecutable principal; si hay varios candidatos, te deja elegir.
- Busca el icono (`.png` o `.svg`) más grande dentro de la app.
- Crea el `.desktop` en `~/.local/share/applications`.
- Si no das la ruta completa, busca el archivo en `~/Downloads`.
- Registra lo que instala en `~/.local/share/instanapp/instanapp_apps.txt`.

## Requisitos

- Linux con entorno de escritorio (GNOME, KDE, XFCE, etc.)
- `bash`, `sudo`, `unzip`, `tar`, `file`
- `desktop-file-utils` (para `update-desktop-database`)

## Instalación

```bash
git clone https://github.com/JRPRobinson/instanapp.git
cd instanapp
chmod +x instanapp
```

Opcional, para usarlo desde cualquier carpeta:

```bash
sudo install -Dm755 instanapp /usr/local/bin/instanapp
```

## Uso

```bash
instanapp [-i archivo] [-l] [-p nombre] [-h]
```

| Opción | Descripción |
|--------|-------------|
| `-i archivo` | Instala la aplicación en `/opt` y crea el `.desktop` |
| `-l` | Lista las apps instaladas con Instanapp |
| `-p nombre` | Purga la app (borra su carpeta en `/opt` y su `.desktop`) |
| `-h` | Muestra la ayuda |

### Ejemplos

```bash
# Instalar desde ~/Downloads
instanapp -i postman-linux-x64.tar.gz

# Instalar con ruta completa
instanapp -i /ruta/a/mi-app.zip

# Ver las apps instaladas
instanapp -l

# Purgar una app (usa el nombre que muestra -l)
instanapp -p Postman
```

Si no lo instalaste en el `PATH`, usa `./instanapp` en lugar de `instanapp`.

## ¿Cómo funciona?

1. Localiza el archivo (ruta indicada o `~/Downloads`).
2. Detecta su tipo y lo extrae en una carpeta temporal.
3. Lo mueve a `/opt`: si trae una sola carpeta usa su nombre; si no, lo deduce del archivo (`postman-linux-x64.tar.gz` → `Postman`).
4. Busca el ejecutable y el icono, y genera el `.desktop`.
5. Registra la app para poder listarla o purgarla después.

## Notas

- Usa `sudo` para escribir y borrar en `/opt`, así que te pedirá la contraseña.
- Si ya existe una app con el mismo nombre en `/opt`, será reemplazada.
- Solo se pueden purgar las apps instaladas con Instanapp (las de `-l`).
- La purga es definitiva: elimina la carpeta completa de la app.

## Contribuir

¿Ideas o errores? Abre un [issue](https://github.com/JRPRobinson/instanapp/issues).

## Licencia

Distribuido bajo la licencia MIT. Consulta el archivo `LICENSE`.

## Autor

**JRPRobinson** · [GitHub](https://github.com/JRPRobinson)

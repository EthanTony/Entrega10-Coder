# Preentrega 10 – Blog Django

Aplicación web desarrollada con Django que permite administrar publicaciones mediante operaciones CRUD (crear, consultar, actualizar y eliminar), incluyendo la carga y visualización de imágenes.

Este proyecto forma parte de las actividades del curso de Python y continúa el desarrollo de las entregas anteriores, conservando funcionalidades como autenticación de usuarios, permisos, búsqueda, paginación y administración desde Django Admin.

## Tecnologías utilizadas

- Python 3.14.7
- Django 5.2.18
- SQLite
- Pillow 13.0.0
- python-decouple
- Bootstrap 5.3.3
- HTML, CSS y JavaScript
- Git y GitHub

## Funcionalidades

### Gestión de publicaciones (CRUD)

- **Crear:** registrar nuevas publicaciones.
- **Consultar:** visualizar el listado y el detalle de cada publicación.
- **Actualizar:** modificar la información y la imagen de una publicación existente.
- **Eliminar:** borrar publicaciones mediante una pantalla de confirmación.

Cada publicación contiene título, contenido, autor, estado, fecha de creación e imagen opcional.

### Gestión de imágenes

El modelo `Post` incorpora el campo:

```python
image = models.ImageField(
    upload_to="posts/",
    blank=True,
    null=True,
    verbose_name="Imagen"
)
```

El campo `image` permite adjuntar una imagen a cada publicación. Su carácter opcional (`blank=True` y `null=True`) permite crear y conservar publicaciones sin necesidad de cargar una imagen.

Las imágenes se almacenan dentro de la carpeta `media/posts/`.

Para gestionar imágenes se utiliza **Pillow**, biblioteca de Python que permite a Django trabajar con archivos de imagen mediante `ImageField`.

### Configuración de archivos multimedia

En `settings.py` se definen las siguientes configuraciones:

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

- `MEDIA_URL`: establece la ruta URL desde la que se accede a los archivos multimedia.
- `MEDIA_ROOT`: define el directorio del sistema de archivos donde Django almacena los archivos multimedia cargados.

Durante el desarrollo, los archivos multimedia se sirven mediante la configuración de URLs cuando `DEBUG=True`.

En un entorno de producción es necesario configurar un servidor o servicio especializado para servir estos archivos.

### Otras funcionalidades

- Registro, inicio y cierre de sesión.
- Autenticación de usuarios.
- Permisos de edición y eliminación para autores y administradores.
- Gestión de publicaciones mediante estados: borrador, publicado y archivado.
- Búsqueda de publicaciones.
- Paginación del listado.
- Administración de modelos desde Django Admin.
- Páginas de inicio y acerca de.
- Mensajes de confirmación y retroalimentación al usuario.

## Instalación y configuración

### 1. Clonar el repositorio

Una vez publicado el proyecto en GitHub:

```bash
git clone <URL-DEL-NUEVO-REPOSITORIO>
cd <CARPETA-DEL-PROYECTO>
```

### 2. Crear y activar el entorno virtual

En Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

Pillow se instala junto con las demás dependencias del proyecto.

### 4. Configurar las variables de entorno

Crear un archivo `.env` en la raíz del proyecto y configurar las variables necesarias, tomando como referencia `.env.example`.

Por ejemplo:

```env
SECRET_KEY=tu_clave_secreta
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

No se debe publicar el archivo `.env` ni compartir sus claves privadas.

### 5. Aplicar migraciones

```bash
python manage.py migrate
```

### 6. Crear un superusuario

```bash
python manage.py createsuperuser
```

### 7. Iniciar el servidor

```bash
python manage.py runserver
```

La aplicación estará disponible en:

`http://127.0.0.1:8000/`

## Uso de la aplicación

### Crear una publicación con imagen

1. Iniciar sesión con una cuenta registrada.
2. Acceder a la opción para crear una publicación.
3. Completar el título y el contenido.
4. Seleccionar el estado de la publicación.
5. Elegir una imagen desde el equipo.
6. Guardar el formulario.

El formulario utiliza `enctype="multipart/form-data"` para permitir el envío de archivos al servidor.

También es posible crear una publicación sin imagen, ya que el campo `image` es opcional.

### Visualizar publicaciones e imágenes

1. Acceder al listado de publicaciones.
2. Seleccionar una publicación para consultar su detalle.
3. Cuando existe una imagen asociada, esta se muestra en la página de detalle.

Las publicaciones sin imagen pueden consultarse normalmente.

### Editar una publicación

1. Iniciar sesión con la cuenta propietaria de la publicación o con una cuenta administradora.
2. Acceder al detalle de la publicación.
3. Seleccionar la opción de edición.
4. Modificar los campos necesarios.
5. Cargar una imagen nueva si se desea reemplazar la anterior.
6. Guardar los cambios.

### Eliminar una publicación

1. Acceder al detalle de la publicación.
2. Seleccionar la opción de eliminar.
3. Revisar la pantalla de confirmación.
4. Confirmar la eliminación.

### Búsqueda y paginación

El listado permite buscar publicaciones mediante los campos habilitados en el formulario de búsqueda. Los resultados se presentan de manera paginada para facilitar su consulta.

### Administración

Django Admin permite administrar los registros del modelo `Post` y gestionar el contenido del sitio desde el panel administrativo.

Para acceder:

`http://127.0.0.1:8000/admin/`

Se requiere una cuenta con permisos administrativos.

## Pruebas

Para verificar la configuración del proyecto:

```bash
python manage.py check
```

Para ejecutar las pruebas automatizadas:

```bash
python manage.py test
```

Se recomienda comprobar manualmente los siguientes escenarios:

- Crear una publicación con imagen.
- Crear una publicación sin imagen.
- Consultar una publicación con imagen.
- Consultar una publicación sin imagen.
- Editar una publicación y reemplazar su imagen.
- Eliminar una publicación mediante la confirmación correspondiente.
- Verificar la búsqueda y paginación.
- Comprobar los permisos de edición y eliminación.

## Estructura general del proyecto

```text
blog_django/
│
├── blog_project/
│   ├── settings.py
│   └── urls.py
│
├── posts/
│   ├── migrations/
│   ├── static/
│   ├── templates/
│   ├── forms.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── media/
│   └── posts/
│
├── templates/
├── manage.py
├── requirements.txt
├── .env.example
└── README.md
```

## Autor

Proyecto desarrollado como parte del curso de Python – Preentrega 10.
# DeClase - Gestor de Conflictos Laborales

**DeClase** es una aplicación web sencilla diseñada para registrar, visualizar y gestionar información sobre conflictos laborales. Permite llevar un seguimiento detallado de cada conflicto, las entidades involucradas (sindicatos, empresas, etc.), las personas clave y las acciones que se llevan a cabo a lo largo del tiempo.

La aplicación se compone de dos vistas principales:
1.  **Vista Pública (`index.html`)**: Un panel visual e interactivo para explorar los conflictos y sus cronologías.
2.  **Panel de Administración (`admin.html`)**: Una interfaz para gestionar todos los datos de la aplicación.

## Características Principales

### Vista Pública (`index.html`)

-   **Listado de Conflictos**: Muestra los conflictos ordenados por la acción más reciente.
-   **Listado de Acciones**: Presenta una cronología de todas las acciones registradas en todos los conflictos.
-   **Ficha de Conflicto**: Vista detallada de un conflicto, que incluye:
    -   Descripción completa.
    -   Duración en días.
    -   Ubicación en un mapa (OpenStreetMap).
    -   Partes involucradas.
    -   Cronología de acciones relacionadas.
-   **Ficha de Acción**: Muestra los detalles de una acción específica y su fuente (si está disponible).
-   **Diseño Responsivo**: Adaptado para visualización en dispositivos móviles y de escritorio.

### Panel de Administración (`admin.html`)

-   **Gestión CRUD completa**: Permite Crear, Leer, Actualizar y Eliminar (CRUD) todos los elementos de la base de datos:
    -   **Conflictos**: Título, descripción, fecha de inicio, estado, ubicación, etc.
    -   **Entidades**: Nombre, tipo (sindicato, empresa, gobierno), logo.
    -   **Personas**: Nombre, rol y entidad asociada.
    -   **Acciones**: Tipo de acción, fecha, descripción, conflicto y entidades asociadas.
-   **Importación de Datos**: Facilita la carga masiva de información a través de un campo para pegar datos en formato JSON.
-   **Guardado Centralizado**: Los cambios se guardan directamente en la base de datos de JSONbin.

## Cómo Funciona

La aplicación es un **sitio web estático** (HTML, CSS y JavaScript) que no requiere un backend propio. Toda la información se almacena y se gestiona a través de la API de **JSONbin.io**, que actúa como una base de datos NoSQL simple.

-   **Lectura de datos**: La vista pública (`index.html`) realiza una petición `GET` a JSONbin para obtener todos los datos y mostrarlos.
-   **Escritura de datos**: El panel de administración (`admin.html`) utiliza peticiones `PUT` para actualizar el archivo JSON completo en JSONbin con los cambios realizados.

## Uso

1.  **Visualizar Conflictos**: Simplemente abre el archivo `index.html` en un navegador web. La aplicación cargará automáticamente los datos más recientes.
2.  **Administrar Datos**: Abre el archivo `admin.html`. Desde allí, puedes navegar por las diferentes secciones (Conflictos, Entidades, etc.) para añadir, editar o eliminar registros.

**Importante**: Para que los cambios realizados en el panel de administración se guarden permanentemente, es necesario hacer clic en el botón **"Guardar Todos los Cambios"**.

## Estructura de Datos

La base de datos es un único objeto JSON que contiene cuatro arrays principales: `conflictos`, `entidades`, `personas` y `acciones`. A continuación se muestra un ejemplo de la estructura de cada objeto.

### Conflicto
```json
{
  "id": 1,
  "titulo": "Huelga en la fábrica de textiles",
  "subtitulo": "Trabajadores exigen mejores condiciones salariales.",
  "descripcion": "Descripción detallada del conflicto...",
  "fecha_inicio": "2023-01-15",
  "fecha_fin": null,
  "estado": "activo",
  "ubicacion": "Parque Industrial, Ciudad Gótica",
  "link_ubicacion": "https://maps.google.com/...",
  "entidades_involucradas": [101, 201]
}
```

### Entidad
```json
{
  "id": 101,
  "nombre": "Sindicato de Obreros Textiles",
  "tipo": "sindicato",
  "logo": "url_al_logo.png"
}
```

### Persona
```json
{
  "id": 301,
  "nombre": "Juan Pérez",
  "rol": "Delegado sindical",
  "entidad_id": 101
}
```

### Acción
```json
{
  "id": 401,
  "id_conflicto": 1,
  "fecha": "2023-01-20",
  "tipo_accion": "medida",
  "descripcion": "Corte de ruta en la entrada de la fábrica.",
  "fuente": "url_a_la_noticia.com",
  "entidades_involucradas": [101]
}
```

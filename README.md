# ExploraNica 🇳🇮

ExploraNica es una **Progressive Web App (PWA)** diseñada para descubrir, explorar y planificar visitas a los destinos turísticos de Nicaragua. Su objetivo es ofrecer una experiencia fluida, rápida y accesible desde cualquier dispositivo, incluso sin conexión.

## Instalación y ejecución

ExploraNica es una aplicación de un solo archivo (`index.html`), sin dependencias externas ni procesos de compilación.  
Para ejecutarla, basta con clonar o descargar el repositorio, abrir el archivo `index.html` directamente en cualquier navegador y listo.  
No requiere servidor ni instalación adicional.  

Versión desplegada:  
👉 **https://jesus8895rodriguez-cpu.github.io/ExploraNica/**

## Tecnologías utilizadas

El proyecto está construido con tecnologías web modernas y servicios en la nube:  
HTML5, CSS3 y JavaScript ES6+ puro (sin frameworks), Firebase Firestore para base de datos en tiempo real y persistencia offline, Leaflet junto con OpenStreetMap para mapas interactivos, Open-Meteo para información climática, Firebase Auth para autenticación sin contraseña mediante enlace mágico por correo, y Manifest + Service Worker para instalación como PWA.

## Seguridad y roles del sistema

La aplicación define tres roles con permisos diferenciados.  
El **Usuario visitante** se identifica mediante enlace mágico enviado a su correo y puede explorar, valorar, comentar, marcar favoritos, crear itinerarios y enviar negocios o fotos para revisión.  
El **Administrador** tiene acceso restringido a funciones de gestión y moderación de contenido, incluyendo la creación, edición y eliminación de lugares o eventos, así como la aprobación o rechazo de negocios y fotos enviadas.  
El **Auditor** cuenta con acceso de solo lectura, limitado a estadísticas y revisión de colas de negocios o fotos.  
Ambos roles administrativos inician sesión desde el mismo botón “🔐 Admin” del encabezado, y el sistema asigna el rol según las credenciales ingresadas.

## Modelo de datos

El modelo de datos se organiza de manera sencilla y clara, relacionando lugares, eventos, valoraciones, comentarios, negocios y fotos enviadas por visitantes:

## Funcionalidades principales

ExploraNica ofrece una experiencia completa para el usuario:  
- Búsqueda avanzada con filtros por categoría, departamento o popularidad  
- Mapa interactivo con clima en tiempo real  
- Itinerarios personalizados con distancia y tiempo estimado entre paradas  
- Recomendaciones según categorías favoritas  
- Sistema de logros y gamificación  
- Directorio de negocios cercanos y galería de fotos moderadas  
- Notificaciones internas de contenido nuevo  
- Interfaz bilingüe en español e inglés  

## Contribuciones

ExploraNica es un proyecto de código abierto.  
Para colaborar, se recomienda hacer un fork del repositorio, crear una rama nueva, realizar los cambios y enviar un pull request para revisión.

## Licencia

El proyecto está bajo la licencia **MIT**, lo que permite su uso, modificación y distribución libre con atribución.

## Autoría

Desarrollado por **el grupo explora Nica**, estudiante de Contabilidad y Finanzas en la UNAN-Managua, apasionado por el desarrollo web y las aplicaciones PWA.

```mermaid
classDiagram
  class Lugar {
    +String id
    +String name
    +String dept
    +float lat
    +float lng
    +String[] categories
    +int views
  }

  class Evento {
    +String id
    +String name
    +String date
    +String dept
  }

  class Valoracion {
    +String placeId
    +int estrellas
  }

  class Comentario {
    +String placeId
    +String texto
    +String tipo
  }

  class Negocio {
    +String id
    +String name
    +String type
    +String phone
    +boolean approved
  }

  class FotoVisitante {
    +String id
    +String placeId
    +boolean approved
  }

  Lugar "1" --> "*" Valoracion : recibe
  Lugar "1" --> "*" Comentario : recibe
  Lugar "1" --> "*" Negocio : tiene cerca
  Lugar "1" --> "*" FotoVisitante : tiene 

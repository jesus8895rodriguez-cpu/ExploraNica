# ExploraNica 🇳🇮

**Progressive Web App** para descubrir, explorar y planificar visitas a los destinos turísticos de Nicaragua.

## Instalación y ejecución

ExploraNica es una aplicación de un solo archivo (`index.html`), sin dependencias que instalar.

1. Cloná o descargá este repositorio  
2. Abrí `index.html` directamente en cualquier navegador — no requiere servidor ni build  
3. Versión desplegada: **https://[tu-usuario].github.io/ExploraNica/**

## Tecnologías utilizadas

| Capa | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript ES6+ puro — sin frameworks |
| Base de datos | Firebase Firestore (tiempo real, persistencia offline) |
| Mapa | Leaflet + OpenStreetMap |
| Clima | Open-Meteo |
| Autenticación | Firebase Auth — enlace de acceso por correo, sin contraseña |
| PWA | Manifest + Service Worker, instalable |

## Seguridad y roles del sistema

La aplicación define **tres roles** con permisos diferenciados:

| Rol | Acceso | Permisos |
|---|---|---|
| **Usuario** (visitante) | Se identifica con su correo (enlace mágico, sin contraseña) | Explorar, valorar, comentar, favoritos, itinerario, enviar negocios/fotos para revisión |
| **Administrador** | Todo lo del Usuario, más: crear/editar/eliminar lugares y eventos, aprobar o rechazar negocios y fotos enviadas, ver estadísticas |
| **Auditor** | Solo lectura: ver estadísticas y las colas de negocios/fotos (pendientes y publicados) — **sin** botones de crear, editar, aprobar ni eliminar en ningún lado |

Ambos roles (Admin/Auditor) inician sesión desde el mismo botón "🔐 Admin" del encabezado; el sistema reconoce cuál contraseña se ingresó y asigna el rol correspondiente.

## Modelo de datos

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

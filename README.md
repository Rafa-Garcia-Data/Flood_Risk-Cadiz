# Flood Risk - Cádiz

Proyecto de práctica de QGIS + Python para el tratamiento de datos geoespaciales. EL proyecto consta de un mapa interactivo con leyenda que permite visualizar el riesgo de inundaciones del municipio de Cádiz.
Es un proyecto simple con cero fricción para el usuario ya que el producto final solo consta de un archivo html. 
Es totalmente escalable a cualquier región y tipo de datos ya que se pueden mostrar nombres de calles o zonas del municipio afectadas, puntos críticos afectados ( hospitales, colegios, etc ) , entre muchos otros.

## Tecnologías

<img width="112" height="20" alt="image" src="https://github.com/user-attachments/assets/1ad60109-8306-42be-859e-984bc0cda445" /> <img width="74" height="20" alt="image" src="https://github.com/user-attachments/assets/71e22524-8798-444f-b309-f362bf0ba891" /> <img alt="Static Badge" src="https://img.shields.io/badge/rasterio-bib-blue?style=plastic&logo=numpy"> <img alt="Static Badge" src="https://img.shields.io/badge/geopandas-bib-white?style=plastic&logo=geopandas"> <img alt="Static Badge" src="https://img.shields.io/badge/QGIS-red?style=plastic&logo=Qgis"> <img alt="Static Badge" src="https://img.shields.io/badge/rasterstats-bib-black?style=plastic&logo=python"> <img alt="Static Badge" src="https://img.shields.io/badge/folium-bib-green?style=plastic&logo=folium">


[![My Skills](https://skillicons.dev/icons?i=python,vscode,html,css&theme=light)](https://skillicons.dev)

## Como funciona
--EN CONSTRUCCIÓN--
1. **Accede al mapa interactivo:** Abre la aplicación directamente desde el navegador web sin necesidad de instalar ningún software GIS (a través del enlace de la demo).
2. **Explora la leyenda de riesgos:** En la esquina inferior izquierda consulta la escala de colores que categoriza los edificios según su cota sobre el nivel del mar ($\le 2\text{m}$ para *Riesgo Alto*, $2\text{m} - 5\text{m}$ para *Riesgo Medio*, y $> 5\text{m}$ para *Riesgo Bajo*).
3. **Navega e inspecciona la zona:** Utiliza el zoom y el desplazamiento para explorar distintas áreas del municipio de Cádiz (casco histórico, paseo marítimo, zona franca, etc.).
4. **Consulta la ficha técnica de cada inmueble:** Haz clic o pasa el cursor sobre cualquier edificio para desplegar la información detallada:
   * **Cota mínima ($m$):** Altitud del punto más bajo del terreno del edificio.
   * **Cota media ($m$):** Elevación promedio sobre el nivel del mar.

### Requisitos

-Navegador 

## Arquitectura

```text
Usuario (Navegador Web)
    │  Abre index.html (GitHub Pages)
    ▼
Leaflet.js Engine + CartoDB Positron Tiles
    │  Carga el mapa base vectorial ligero
    ▼
GeoJSON Overhead Layer (Folium Output)
    │  Renderiza los 5,163 polígonos de edificios reproyectados (EPSG:4326)
    ▼
CSS Dynamic Style Function
    │  Aplica la escala cromática de riesgo según la cota relativa (≤2m, 2m-5m, >5m)
    ▼
Branca MacroElement (Leyenda & Tooltips)
    │  Inyecta la leyenda flotante DOM y despliega métricas ZonalStats al hacer hover/click
    ▼
Web UI (Visualización del mapa interactivo final con fichas por inmueble)

- **Sin scraping**: datos oficiales obtenidos del CNIG https://centrodedescargas.cnig.es/CentroDescargas/home
- **Sin dependencias pesadas**: sin instalaciones previas, solo abre el enlace del mapa. 

## Estructura del proyecto

```
Notibrief/
├── server.py              # Servidor FastAPI + web UI
├── resumidor.py           # Resumen extractivo (TF-IDF)
├── captured_posts.json    # Posts capturados
├── Dockerfile             # Imagen Docker
├── docker-compose.yml     # Servicio Docker
├── start.bat              # Lanzador one-click
├── stop.bat               # Detener servidor
├── requirements.txt       # Dependencias Python
└── extension/             # Extension Chrome
    ├── manifest.json
    ├── content.js
    ├── background.js
    └── icons/
```

## API

| Endpoint | Metodo | Descripcion |
|---|---|---|
| `/api/status` | GET | Estado del servidor |
| `/api/posts` | GET | Lista de posts capturados |
| `/api/capture` | POST | Capturar un post nuevo |
| `/api/posts/{index}/summarize` | POST | Resumir un post |
| `/api/summarize-all` | POST | Resumir todos los posts |
| `/api/posts/{index}` | DELETE | Eliminar un post |
| `/api/clear` | POST | Limpiar todos los posts |
| `/api/shutdown` | POST | Apagar el servidor |

## Resultados
- <ins>Disminuye</ins> tu <ins>tiempo</ins> haciendo scrolling en la red social, seleccionando sólo las publicaciones que te interesen
- <ins>Click</ins> derecho del ratón
- Proyecto de mejora de una base previa dedicado a portales de noticias generales, ahora <ins>centrado en LinkedIn</ins>
- Mejora la <ins>calidad de la <ins>información</ins> que recibes

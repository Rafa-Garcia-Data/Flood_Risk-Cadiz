 # Flood Risk - Cádiz :ocean:

Proyecto de práctica de QGIS + Python para el tratamiento de datos geoespaciales. EL proyecto consta de un mapa interactivo con leyenda que permite visualizar el riesgo de inundaciones del municipio de Cádiz.
Es un proyecto simple con cero fricción para el usuario ya que el producto final solo consta de un archivo html. 
Es totalmente escalable a cualquier región y tipo de datos ya que se pueden mostrar nombres de calles o zonas del municipio afectadas, puntos críticos afectados ( hospitales, colegios, etc ) , entre muchos otros.
Se han usado datos oficiales del [CNIG](https://centrodedescargas.cnig.es/CentroDescargas/home) con mapa del terreno de alta definición a fecha de 2020.

:world_map:[MAPA INTERACTIVO](https://rafa-garcia-data.github.io/Flood_Risk-Cadiz/)

## Tecnologías :zap:

<img width="112" height="20" alt="image" src="https://github.com/user-attachments/assets/1ad60109-8306-42be-859e-984bc0cda445" /> <img width="74" height="20" alt="image" src="https://github.com/user-attachments/assets/71e22524-8798-444f-b309-f362bf0ba891" /> <img alt="Static Badge" src="https://img.shields.io/badge/rasterio-bib-blue?style=plastic&logo=numpy"> <img alt="Static Badge" src="https://img.shields.io/badge/geopandas-bib-white?style=plastic&logo=geopandas"> <img alt="Static Badge" src="https://img.shields.io/badge/QGIS-red?style=plastic&logo=Qgis"> <img alt="Static Badge" src="https://img.shields.io/badge/rasterstats-bib-black?style=plastic&logo=python"> <img alt="Static Badge" src="https://img.shields.io/badge/folium-bib-green?style=plastic&logo=folium">

[![My Skills](https://skillicons.dev/icons?i=python,vscode,html,css&theme=light)](https://skillicons.dev)

## Cómo funciona :bulb:

1. **Accede al mapa interactivo:** Abre la aplicación directamente desde el navegador web sin necesidad de instalar ningún software GIS (a través del enlace de la demo).
2. **Explora la leyenda de riesgos:** En la esquina inferior izquierda consulta la escala de colores que categoriza los edificios según su cota sobre el nivel del mar ($\le 2\text{m}$ para *Riesgo Alto*, $2\text{m} - 5\text{m}$ para *Riesgo Medio*, y $> 5\text{m}$ para *Riesgo Bajo*).
3. **Navega e inspecciona la zona:** Utiliza el zoom y el desplazamiento para explorar distintas áreas del municipio de Cádiz (casco histórico, paseo marítimo, zona franca, etc.).
4. **Consulta la ficha técnica de cada inmueble:** Haz clic o pasa el cursor sobre cualquier edificio para desplegar la información detallada:
   * **Cota mínima ($m$):** Altitud del punto más bajo del terreno del edificio.
   * **Cota media ($m$):** Elevación promedio sobre el nivel del mar.

### Requisitos

-Navegador 

## Arquitectura :building_construction:

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
```

- **Sin scraping**: datos oficiales obtenidos del CNIG https://centrodedescargas.cnig.es/CentroDescargas/home
- **Zero Backend**: Renderizado 100% en el cliente (Client-side Leaflet.js) sin necesidad de servidor ni base de datos activa.
- **Carga optimizada**: Capa geoespacial vectorizada y optimizada para una navegación fluida sin sobrecargar la memoria del navegador.
- **Sin dependencias GIS**: Permite la inspección técnica completa de elevaciones desde cualquier dispositivo o navegador web.



## Estructura del proyecto

```text
Flood_Risk-Cadiz/
├── .gitignore                     # Configuración de exclusiones de Git
├── README.md                      # Documentación principal del repositorio
├── cadiz_boundary.gpkg            # Capa vectorial del límite municipal de Cádiz
├── cadiz_riesgo_inundacion.qgz    # Proyecto de QGIS montado con simbología y capas
├── edificios_cadiz_clip.gpkg      # Huellas urbanas de edificios recortadas
├── edificios_riesgo_cadiz.gpkg    # GeoPackage final procesado con estadísticas zonales
├── index.html                     # Visor web interactivo desplegado en GitHub Pages
├── main.ipynb                     # Notebook de Jupyter con el pipeline ETL (Python)
├── mdt_cadiz.tif                  # Modelo Digital del Terreno (Raster 2m del CNIG)
└── vias_cadiz_clip.gpkg           # Capa de viario urbano recortada de Cádiz
```
## Resultados
- <ins>Visualización</ins> rápida para previsión o previsiones futuras de lluvias o subidas del nivel del mar ( escalable a todo tipo de desastres naturales ).
- Un solo <ins>enlace</ins> para la demostración del proyecto. 
- Proyecto de estudio y práctica sobre conocimientos de datos geoespaciales y QGIS y entornos de trabajos de python orientados a <ins>geodata</ins>.
- Leyenda y escala de colores intuitivos e información sobre el inmueble por donde se pasa el <ins>cursor</ins>.

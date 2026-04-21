# KINE - Buscador de Centros de Kinesiología UP

## Descripción del Proyecto
KINE es una aplicación web interactiva desarrollada para encontrar y comparar rápidamente centros de kinesiología disponibles según su proximidad a una dirección de referencia. 

El sistema utiliza algoritmos de cálculo de distancias sobre mapas interactivos para recomendarle al afiliado o paciente qué consultorio le resulta más conveniente, ordenando la lista desde el más cercano hasta el más lejano.

## Funcionalidades Principales
- **Autocompletado y Geocodificación:** El sistema cuenta con un motor de búsqueda que traduce direcciones físicas ingresadas por el usuario a coordenadas GPS exactas utilizando el proveedor cartográfico OpenStreetMap (Nominatim).
- **Cálculo de Rutas en Línea Recta:** Usando fórmulas sobre coordenadas espaciales, detecta la distancia euclidiana entre el usuario y toda la red de profesionales del centro médico en milisegundos.
- **Interfaz Híbrida (Lista + Mapa):** La pantalla se divide en un menú de resultados ordenados (destacando en verde el centro óptimo) y un mapa visual donde se trazan líneas de conexión entre tu ubicación y todos los centros.
- **Autoenfoque interactivo:** Al hacer clic en la tarjeta del profesional, el mapa se desplaza suavemente centrándolo.

## Tecnologías Utilizadas
- **HTML5 y CSS3 nativo:** Para lograr una carga veloz y adaptable sin depender de frameworks pesados de diseño. Variables CSS para personalización de colores institucionales (`#0767A7`).
- **Vanilla JavaScript:** Toda la lógica asincrónica (fetching del archivo JSON de centros) y manipulación del DOM se maneja con el motor nativo del navegador.
- **Leaflet.js:** Una de las bibliotecas open-source más populares para la renderización del mapa y proyección de marcadores, popups interactivos y geometrías en pantalla.
- **FontAwesome:** Se utiliza en su versión web (v6) para proveer de iconografía (ubicaciones, carga, rutas empíricas, etc.).

## Estructura de Datos (`centros.json`)
La carga de datos se maneja dinámicamente desde el archivo base de configuración.
Los profesionales están organizados bajo un nodo raíz de localidades para agilizar búsquedas o futuras optimizaciones de bases de datos.

```json
{
    "especialidad": "Kinesiologia",
    "localidades": [
        {
            "nombre": "Quilmes",
            "profesionales": [
                {
                    "nombre": "DR. EJEMPLO",
                    "direccion": "Calle 123",
                    "telefono": "011-...",
                    "lat": -34.722,
                    "lng": -58.256
                }
            ]
        }
    ]
}
```

Cada vez que el DOM inicializa, el cliente efectúa un request para precargar esta base de profesionales antes de pedir la dirección al usuario.

## Instalación y Uso
1. Para modificar la lista de profesionales, basta con editar la estructura interna de `centros.json`.
2. Utilizar cualquier servidor web estático local (como Apache de XAMPP/LAMPP, o `python -m http.server`, o LiveServer) en el mismo nivel donde se ubica el archivo `index.html`.
3. Navegar en el navegador a través del localhost para utilizar el motor de búsqueda que inicializará por defecto en su referencia predefinida (Mendoza 563, Ezpeleta).

Este proyecto representa una prueba de concepto sólida y escalable para optimizar las asignaciones de turnos médicos presenciales.

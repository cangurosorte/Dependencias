# Detección y Visualización de Comunidades en Redes

Este proyecto utiliza un cuaderno de Google Colab para analizar archivos CSV que representan conexiones de red, con el objetivo de identificar y visualizar comunidades de máquinas virtuales.

## Objetivo

El objetivo principal de este cuaderno es proporcionar una herramienta para:

*   Cargar y pre-procesar datos de conexiones de red desde un archivo CSV.
*   Construir un modelo de grafo para representar las interconexiones.
*   Aplicar algoritmos de detección de comunidades (específicamente el algoritmo de Louvain) para identificar grupos de nodos densamente conectados.
*   Generar un reporte detallado de las comunidades encontradas y los nodos que actúan como puentes entre ellas.
*   Ofrecer una visualización interactiva del grafo para explorar las comunidades y conexiones.

## Parámetros de Configuración

Estos parámetros se encuentran en la sección "3. DEFINICIÓN DE PARÁMETROS" del cuaderno y permiten ajustar la carga de datos, el filtrado y la visualización:

*   `csv_file_path`: (string) La ruta al archivo CSV que contiene los datos de conexión de red. **Debe modificar esta variable** con el nombre de su archivo.
*   `output_file_path`: (string) El nombre del archivo de texto donde se guardará el reporte del análisis de comunidades.
*   `filter_unescanned`: (boolean) Si se establece en `True`, se excluirán del análisis todas las conexiones donde el nodo de origen o destino sea "Unscanned Device".
*   `apply_physics`: (boolean) Controla si se aplica el motor de física de `vis.js` en la visualización interactiva para la disposición de los nodos.
*   `show_arrows`: (boolean) Controla si se muestran las flechas en las aristas de la visualización interactiva para indicar la dirección de la conexión.

## Forma de Uso

1.  Sube tu archivo CSV con los datos de conexión de red al entorno de Google Colab.
2.  Actualiza la variable `csv_file_path` en la sección "3. DEFINICIÓN DE PARÁMETROS" con la ruta correcta a tu archivo CSV.
3.  Opcionalmente, ajusta los valores de `output_file_path`, `filter_unescanned`, `apply_physics`, y `show_arrows` según tus necesidades.
4.  Ejecuta todas las celdas del cuaderno en orden.
5.  El reporte del análisis se guardará en el archivo especificado por `output_file_path`.
6.  La visualización interactiva del grafo se mostrará en la salida de la última celda de código.

## Funcionalidades

*   **Carga de Datos:** Lee un archivo CSV con un formato específico (columnas esperadas: `Day`, `LocalVMName`, `LocalAssetID`, `LocalGroups`, `LocalIP`, `LocalPort`, `Protocol`, `LocalProcessName`, `RemoteVMName`, `RemoteAssetID`, `RemoteGroups`, `RemoteIP`, `RemotePort`, `ConnectionCount`). **Este formato corresponde a la salida del reporte de dependencias de red de Google Cloud Migration Center.**
*   **Filtrado Opcional:** Permite excluir nodos con el nombre "Unscanned Device" antes de construir el grafo.
*   **Construcción de Grafo:** Crea un grafo dirigido utilizando la librería `networkx`, donde los nodos representan máquinas virtuales y las aristas representan conexiones con un peso basado en `ConnectionCount`.
*   **Detección de Comunidades:** Implementa el algoritmo de Louvain (`python-louvain`) para encontrar la mejor partición del grafo en comunidades, considerando el peso de las conexiones.
*   **Generación de Reporte:** Exporta un archivo de texto (`reporte_comunidades.txt`) que resume el análisis, listando los nodos por comunidad y identificando los nodos que conectan diferentes comunidades.
*   **Visualización Interactivo:** Utiliza la librería `jaal` para generar una visualización interactiva del grafo, permitiendo explorar nodos, aristas y sus atributos, incluyendo la comunidad a la que pertenecen. También se incluye la opción de visualizar usando `pyvis` para generar un archivo HTML.

## Requisitos

*   Google Colab environment or a local Python environment with the required libraries.
*   A CSV file with network connection data in the specified format (output of Google Cloud Migration Center's network dependencies report).

## Instalación

If running in a local Python environment, you need to install the required libraries:

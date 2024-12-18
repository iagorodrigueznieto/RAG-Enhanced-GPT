
# rag_2024

## Descripción del proyecto
### ¿Qué es un RAG?
![Innovative AI: The Power of Retrieval Augmented Generation](https://ambersearch.de/wp-content/uploads/2023/10/Retrieval-Augmented-Generation_en_ohne-Uberschrift-1080x675.webp)

Un RAG es un modelo que mezcla dos procesos: buscar información y generar respuestas. Se usa para mejorar modelos como GPT, permitiéndoles acceder a bases de datos externas para obtener información útil antes de dar una respuesta.

### Primer Cuaderno
En esta cuaderno, se implementará un sistema RAG que crea una base de datos vectorial a partir de datos obtenidos de una página web, a través de web scraping. Este sistema podrá procesar la información recuperada y generar respuestas a preguntas basadas en esos datos.
### Segundo Cuaderno
Se desarrollará un RAG que toma archivos PDF como fuente de información. El sistema segmentará el texto de los documentos en partes, las guardará en una base de datos vectorial y generará respuestas en español basadas en esos fragmentos.
### Tercer Cuaderno
Se creará una interfaz gráfica (GUI) para interactuar con uno de los sistemas RAG desarrollados previamente. 

## Instrucciones para Docker

  

![alttext](https://cdn-icons-png.flaticon.com/256/919/919853.png)

  


Si no tienes docker, [descárgalo e instálalo.](https://www.docker.com/products/docker-desktop/)

Ya habiendo instalado docker primero crearemos una red propia para el propio proyecto.

    docker network create ollama_network

### *Ollama*
 Para ejecutar lanza el contenedor apropiado para tu equipo [Ollama](https://ollama.com/download) con el siguiente comando en la terminal. 
 
 **CPU ONLY**

     docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama --net=ollama_network ollama/ollama

**Nvidia GPU**
Esto es lo ideal para correr los modelos, el comando es el mismo pero con el parametro **--gpus=all**

    docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama --network=ollama_network ollama/ollama

Verificamos que Ollama está funcionando: 

    curl http://localhost:11434
Si recibes este mensaje es que todo va bien : 

    Ollama is running


### ***Open-WebUI***
En este caso vamos a ejecutar una interfaz web sólo para descargar nuestro modelo, pero podremos usarlo como interfaz para un chat bot. No es obligatorio pero si que conviene autenticarse. Como en Ollama, podremos ejecutar este contenedor con dos opciones: 

**CPU ONLY**

    docker run -d -p 3000:8080 -e OLLAMA_BASE_URL=http://ollama:11434 -v open-webui:/app/backend/data --name open-webui --net=ollama_network --restart always ghcr.io/open-webui/open-webui:main

**Nvidia GPU**
Necesitaríamos tener instalado Nvidia Container Toolkit:

    docker run -d -p 3000:8080 --gpus all -e OLLAMA_BASE_URL=http://ollama:11434 -v open-webui:/app/backend/data --name open-webui --net=ollama_network --restart always ghcr.io/open-webui/open-webui:main

- Accedemos a http://localhost:3000 para verificar que Open-WebUI está instalado.
 - Creamos una cuenta

## Configuración del entorno

Para la ejecución de los scripts es necesario tener instalado Python, y algún gestor de paquetes como por ejemplo conda.

  

Puedes descargar conda [aquí](https://docs.anaconda.com/miniconda/install/#quick-command-line-install).

  

  

Ya habiendo instalado conda, podremos crear un entorno a partir del exportado presente en el repositorio a través de este comando ejecutado en la terminal.

  

  

    conda env create -f requirements.yaml

  

  

Se creará un entorno ya con librerías necesarias para ejecutar los scripts del repositorio.





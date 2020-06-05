# Utilizando RASA con Docker

Descarga Docker [aquí](https://docs.docker.com/get-docker/)



## Actualiza tu modelo de NLU, y reentrena

Modifica nlu.md

`docker run -v $(pwd):/app rasa/rasa:1.8.1-full train nlu`

### Test NLU

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell nlu`

Échale un vistazo a los diferentes resultados que te puede dar un test del modelo NLU en [`test-nlu.md`](https://github.com/monoceros-tech/rasa-restaurant-docker/blob/nlu-test/test-nlu.md)


## Si empiezas con RASA init 

`docker run -v $(pwd):/app rasa/rasa:1.8.1-full init --no-prompt --name XXXX`

y luego testea la conversación "dummy"

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell` 


## Actualiza tu asistente DM con el dominio y stories, y reentrena

Modifica stories.md y domain.yml

`docker run -v $(pwd):/app rasa/rasa:1.8.1-full train --domain domain.yml --data data --out models`

## Testea la conversación con el asistente (DM+NLU)

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell`

Échale un vistazo a los diferentes resultados que te puede dar un test del asistente en [`test-dm.md`](https://github.com/monoceros-tech/rasa-restaurant-docker/blob/dm-test/test-dm.md)


## Añade custom actions, y reentrena

Crea la carpeta /actions y mueve el archivo actions.py ahí

`mkdir actions`
`mv actions.py actions/actions.py`

Rasa SDK espera un modulo de Python, asegúrate que tienes este fichero en el directorio.

`touch actions/__init__.py `

Actualiza `stories.md`y `domain.yml`.

Re-entrenamos con
`docker run -v $(pwd):/app rasa/rasa:1.8.1-full train`

Conecta tus actions, que están ejecutándose en un servidor separado del servidor de Rasa. Crea una red para conectar los dos contenedores de Docker.

`docker network create my-project`

Lanza las actions con el siguiente comando:

`docker run -d -v $(pwd)/actions:/app/actions --net my-project --name action-server rasa/rasa-sdk:1.10.0`

Para parar este último contenedor, ejecuta: `docker stop action-server`

Para decirle a RASA que utilice el servidor con las actions, tendrás que añadir esa localización en el fichero `endpoints.yml` referenciando el --name que le diste:

> action_endpoint:
>    url: "http://action-server:5055/webhook"

### Testea la conversación con las actions 

`docker run -it -v $(pwd):/app -p 5005:5005 --net my-project rasa/rasa:1.8.1-full shell`

## Más información en

[Building in Docker, RASA Blog](https://rasa.com/docs/rasa/user-guide/docker/building-in-docker/)

### Recomendaciones con Docker

Lista los contenedores de Docker con `docker ps`
Versión de Docker  `docker -v`

Si paras y reinicias el contenedor con nombre XXXX, puede que te salte un error así:

> docker: Error response from daemon: Conflict. The container name "/XXXX" is already in use by container "f7ffc625e81ad4ad54cf8704e6ad85123c71781ca0a8e4b862f41c5796c33530". You have to remove (or rename) that container to be able to reuse that name.

Esto significa que tienes un contenedor parado (stopped) con ese nombre. Puedes borrarlo con:

`docker rm XXXX`
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
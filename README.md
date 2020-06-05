# Utilizando RASA con Docker

Descarga Docker [aquí](https://docs.docker.com/get-docker/)



## Actualiza tu modelo de NLU, y reentrena

Modifica nlu.md

`docker run -v $(pwd):/app rasa/rasa:1.8.1-full train nlu`

### Test NLU

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell nlu`




## Si empiezas con RASA init 

`docker run -v $(pwd):/app rasa/rasa:1.8.1-full init --no-prompt --name XXXX`

y luego testea la conversación "dummy"

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell` 

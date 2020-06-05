
# Test Conversación (DM+NLU)

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell`

## Happy path: Comprende todo bien

Your input -> hello                                                                                                                        
Hey! What kind of restaurant are you looking for?
Your input ->  a spanish restaurant                                                                                                         
Great! Here is the list of restaurants...
Did that help you?
Your input ->  yes                                                                                                                          
Bye

## Desviación: entidad no reconocida

Your input ->  hello                                                                                                                        
Hey! What kind of restaurant are you looking for?
Your input ->  I want to go to a thailand restaurant                                                                                        
Oops!
Sorry! I don't know what it is. What type of restaurant?
Your input ->  thailand                                                                                                                     
Bye

## Desviación: no clasifica el intent bien

Your input ->  hello                                                                                                                        
Hey! What kind of restaurant are you looking for?
Your input ->  indian                                                                                                                       
Bye




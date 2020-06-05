## find_restaurants
* greet
  - utter_greet
* search_restaurant{"food_type":"korean"}
  - utter_list_restaurants
  - action_restaurant_search
  - utter_did_that_help
* affirm
  - utter_goodbye

## find_cheap_restaurants
* greet
  - utter_greet
* search_restaurant{"food_type":"spanish", "rest_characteristic":"cheap"}
  - utter_list_restaurants_cheap
  - action_restaurant_search
  - utter_did_that_help
* affirm
  - utter_goodbye

## error_not_received_foodtype + new search
* greet
  - utter_greet
* search_restaurant{"food_type":""}
  - utter_sorry
  - utter_sorry_not_understood
* search_restaurant{"food_type":"spanish"}
  - utter_list_restaurants
  - action_restaurant_search
  - utter_did_that_help
* affirm
  - utter_goodbye

## error_deny
* greet
  - utter_greet
* deny
  - utter_sorry
  - utter_did_that_help
* deny
  - utter_goodbye

## say goodbye
* goodbye
  - utter_goodbye


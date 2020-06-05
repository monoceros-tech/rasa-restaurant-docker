

# Test NLU

`docker run -it -v $(pwd):/app rasa/rasa:1.8.1-full shell nlu`


## Recognized intent + entity

i want a vegetarian

{
  "intent": {
    "name": "search_restaurant",
    "confidence": 0.9996820688247681
  },
  "entities": [
    {
      "entity": "food_type",
      "start": 9,
      "end": 19,
      "extractor": "DIETClassifier",
      "value": "vegetarian"
    }
  ],
  "intent_ranking": [
    {
      "name": "search_restaurant",
      "confidence": 0.9996820688247681
    },
    {
      "name": "affirm",
      "confidence": 0.00012818224786315113
    },
    {
      "name": "goodbye",
      "confidence": 0.00010138725338038057
    },
    {
      "name": "deny",
      "confidence": 7.190139149315655e-05
    },
    {
      "name": "greet",
      "confidence": 1.6501588106621057e-05
    }
  ],
  "response_selector": {
    "default": {
      "response": {
        "name": null,
        "confidence": 0.0
      },
      "ranking": []
    }
  },
  "text": "i want a vegetarian"
}


## Recognized intent + NOT entity

i want a fantastic restaurant

{
  "intent": {
    "name": "search_restaurant",
    "confidence": 0.9996992349624634
  },
  "entities": [],
  "intent_ranking": [
    {
      "name": "search_restaurant",
      "confidence": 0.9996992349624634
    },
    {
      "name": "affirm",
      "confidence": 0.0001699595304671675
    },
    {
      "name": "goodbye",
      "confidence": 8.32416262710467e-05
    },
    {
      "name": "deny",
      "confidence": 3.750960240722634e-05
    },
    {
      "name": "greet",
      "confidence": 1.0042891517514363e-05
    }
  ],
  "response_selector": {
    "default": {
      "response": {
        "name": null,
        "confidence": 0.0
      },
      "ranking": []
    }
  },
  "text": "i want a fantastic restaurant"
}

## Not recognized intent nor entities: error

indian

{
  "intent": {
    "name": "affirm",
    "confidence": 0.6268613934516907
  },
  "entities": [],
  "intent_ranking": [
    {
      "name": "affirm",
      "confidence": 0.6268613934516907
    },
    {
      "name": "search_restaurant",
      "confidence": 0.3155854344367981
    },
    {
      "name": "deny",
      "confidence": 0.03963344171643257
    },
    {
      "name": "goodbye",
      "confidence": 0.010602323338389397
    },
    {
      "name": "greet",
      "confidence": 0.007317427545785904
    }
  ],
  "response_selector": {
    "default": {
      "response": {
        "name": null,
        "confidence": 0.0
      },
      "ranking": []
    }
  },
  "text": "indian"
}

## Bad classified intent, recognized entity:

chinese

{
  "intent": {
    "name": "greet",
    "confidence": 0.41373059153556824
  },
  "entities": [
    {
      "entity": "food_type",
      "start": 0,
      "end": 7,
      "extractor": "DIETClassifier",
      "value": "chinese"
    }
  ],
  "intent_ranking": [
    {
      "name": "greet",
      "confidence": 0.41373059153556824
    },
    {
      "name": "affirm",
      "confidence": 0.3518904745578766
    },
    {
      "name": "search_restaurant",
      "confidence": 0.17603799700737
    },
    {
      "name": "deny",
      "confidence": 0.03687034174799919
    },
    {
      "name": "goodbye",
      "confidence": 0.021470529958605766
    }
  ],
  "response_selector": {
    "default": {
      "response": {
        "name": null,
        "confidence": 0.0
      },
      "ranking": []
    }
  },
  "text": "chinese"
}
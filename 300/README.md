# 300 - Building Our Application

Follow the instructions in the book.

TO DO: Write the instructions here, instead.

**NOTE**: To get your Chat ID of Telegram, open your Telegram application (desktop or web) and search for "Get My ID", This will be a [bot](https://web.telegram.org/k/#@getmyid_bot) which you can send a message to (```/start```) and it will return your Chat ID (a numeric value of 10 digits).

![Telegram_Random_Cocktail_Workflow](https://github.com/vanHeemstraSystems/n8n-telegram/assets/1499433/c6cbaa7d-83ff-4d77-9dd2-3af0bc7d66f7)

Telegram  - Random Cocktail workflow

In JSON, this workflow is defined as follows:

```
{
  "name": "Telegram - Random Cocktail",
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 18
            }
          ]
        }
      },
      "id": "8d84c0f1-b33b-485b-adff-ca16abddb3e1",
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.1,
      "position": [
        700,
        380
      ]
    },
    {
      "parameters": {
        "url": "https://www.thecocktaildb.com/api/json/v1/1/random.php",
        "options": {}
      },
      "id": "09e98ae2-9dd1-4ffa-ad47-c2c605200853",
      "name": "HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.1,
      "position": [
        920,
        380
      ]
    },
    {
      "parameters": {
        "chatId": "REPLACE_WITH_YOUR_CHAT_ID",
        "text": "={{ $json[\"drinks\"][0][\"strDrink\"] }}\n{{ $json[\"drinks\"][0][\"strInstructions\"] }}\n{{ $json[\"drinks\"][0][\"strDrinkThumb\"] }}",
        "additionalFields": {}
      },
      "id": "523f8541-d0e5-4ffb-bfb2-bf788610ea70",
      "name": "Telegram",
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.1,
      "position": [
        1140,
        380
      ],
      "credentials": {
        "telegramApi": {
          "id": "by72grh45mITwNPC",
          "name": "Telegram account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "19fb6faf-de22-4efa-8faf-3c0b9864d4e6",
  "id": "w0PCT1vei9dklSS2",
  "meta": {
    "instanceId": "71233aec82bf97d1f7455405991c6cb2a38b3444ef561233d0111cb97b5ca430"
  },
  "tags": []
}
```

**NOTE**: Replace ```REPLACE_WITH_YOUR_CHAT_ID``` with your Telegram Chat ID.

Once executed (either manually or as scheduled at 18:00 each day), you should see a message like below in your Telegram app (provided your are wvanheemstra@icloud.com):



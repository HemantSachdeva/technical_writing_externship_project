# Symbl API Documentation

Below is the documentation for sending a `GET` request to [Symbl Ai](https://symbl.ai/) that returns a conversation in JSON format as a response.

## Base URL

All of the APIs use the base URL as below for all the Symbl API services:

```
https://api.symbl.ai/v1
```

For conversations, the endpoint is:

```
/v1/conversations
```

It returns the conversation object that provides Conversation Intelligence like Topics, Action Items, Questions, etc.

Note: Before going deep into the conversation object, you first have to authenticate yourself using the `Authorization` header with the `Access Token` that you get from [here](https://docs.symbl.ai/docs/developer-tools/authentication/).

## GET Conversation Insights

This API returns the conversation meta-data like assignee and sender name and email, text message, eneities type and user ID.

### HTTP Request

```
GET https://api.symbl.ai/v1/conversations/{conversationId}/insights
```

### Example API Call

**cURL**

```
curl --location --request GET "https://api.symbl.ai/v1/conversations/$CONVERSATION_ID/insights" \
    --header "Authorization: Bearer $AUTH_TOKEN"
```

**Node.js**

```
const request = require('request');
const authToken = AUTH_TOKEN;
const conversationId = CONVERSATION_ID;

request.get({
    url: `https://api.symbl.ai/v1/conversations/${conversationId}/insights`,
    headers: { 'Authorization': `Bearer ${authToken}` },
    json: true
}, (err, response, body) => {
    console.log(body);
});
```

**Python**

```
import requests

conversation_id = "6627931611725824"
url = f"https://api.symbl.ai/v1/conversations/{conversation_id}/insights"

# set your access token here.
access_token = 'AccessToken'
headers = {
    'Authorization': 'Bearer ' + access_token,
    'Content-Type': 'application/json'
}

responses = {
    400: 'Bad Request! Please refer docs for correct input fields.',
    401: 'Unauthorized. Please generate a new access token.',
    404: 'The conversation and/or it\'s metadata you asked could not be found, please check the input provided',
    429: 'Maximum number of concurrent jobs reached. Please wait for some requests to complete.',
    500: 'Something went wrong! Please contact support@symbl.ai'
}
response = requests.request(
    "GET", url, headers=headers)
if response.status_code >= 200 and response.status_code < 400:
    # Successful API execution
    response_json = response.json()
    print(response_json)
elif response.status_code in responses.keys():
    print(responses[response.status_code])  # Expected error occurred
else:
    print("Unexpected error occurred. Please contact support@symbl.ai" +
          ", Debug Message => " + str(response.text))

```

**Response**

```
{
    "insights": [
        {
            "id": "5288719680536576",
            "text": "How was the difference there?",
            "type": "question",
            "score": 0.9827664988519251,
            "messageIds": [
                "5549178644070400"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
        {
            "id": "5660876935790592",
            "text": "Did you want navy blue or royal blue?",
            "type": "question",
            "score": 0.9921441245153866,
            "messageIds": [
                "5213026535866368"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
        {
            "id": "5810274487500800",
            "text": "What color did you want the New Yorker in?",
            "type": "question",
            "score": 0.9963072322074725,
            "messageIds": [
                "5861300292812800"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
        {
            "id": "6037045170405376",
            "text": "Sure what I need to do?",
            "type": "question",
            "score": 0.9081042802022934,
            "messageIds": [
                "5191824211705856"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
        {
            "id": "6098067562430464",
            "text": "Okay, what ZIP code are you located in 1940, 6?",
            "type": "question",
            "score": 0.9296213757388787,
            "messageIds": [
                "5582660145512448"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
        {
            "id": "6404582466912256",
            "text": "Yes, ma'am and Mr. Johnson, do you have the Parker scarf in light blue with you now?",
            "type": "question",
            "score": 0.9335907924659729,
            "messageIds": [
                "4936662100475904"
            ],
            "from": {
                'id': '1c9f5b5e-42b2-4f73-8a23-fb0de9523497',
                'name': 'Surbhi Rathore',
                'userId': 'surbhi@example.com'
            },
        },
    ]
}
```

More details about the services can be found in the [Conversation APIs](https://docs.symbl.ai/docs/conversation-api/introduction) section.

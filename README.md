# API Documentation



Symbl APIs are built around REST (Representational State Transfer) and has predictable resource-oriented URLs, accept form-encoded request bodies, return JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.
Terms to get acquainted with:
### 1.Base URL:
All Symbl APIs use the base URL 
```sh
https://api.symbl.ai/v1/ 
```

### 2.Endpoint:
 `/v1/conversations` - Returns the conversation object that provides Conversation Intelligence like Topics, Action Items, Questions, etc. - Supported API: [Conversation API](/docs/conversation-api/introduction)
### 3.Parameters:
 To get specific data from the server, Symbl has parameters depending on the API. 
### 4.Authentication: 
To identify a developer and keep track of the number of customers, we need authentication. 
Symbl uses OAuth2.0 Protocol for Authentication. Steps for API Authentication on the Symbl Platform
- Login to the Symbl Platform 
- From your homepage note down your App id and App Secret. It is advised to keep them confidential and handy
- To generate Access Token, make a POST to the Endpoint: ```
https://api.symbl.ai/oauth2/token:generate```


## CONVERSATION API 
The Conversation API provides a REST API interface for getting your processed Speech to Text data(also known as Transcripts) and Conversational Insights.

To view insights about a conversion, you must provide the API with a Conversation ID.

### API Reference 
If you have a Conversation ID the Conversation API can help you:
- _Conversation_ : Find the meeting name, member name and email, start and end time of the meeting, meeting type and meeting ID details.
- _Delete Conversation_ : Delete a conversation and all related entities.
- _Members_ : Find all members/participants from a conversation.
- _Update Members_: Update the unique speakers detected as members/participants.
- _Message_ : Provide you with Speech to Text, Sentiments and Action Items in conversation.
- _Topic_ : Provide you with important topics from a conversation.
- _Action Items_ : Provides you with important action items from a conversation.
- _Questions_: Provides you with questions present in a conversation.
- _Follow Ups_: Provides you with follow-up requests said in a conversation.
- _Analytics_: Find speaker ratio, talk time, silence, pace and overlap in a conversation.
- _Entities-: Provides you with entities like location, person, date, number, organization, datetime, daterange, etc.
- _Trackers_: Trackers allow you to track the occurrence of certain key words or phrases in a conversation so you can identify emerging trends and gauge the nature of interactions.
- _Summary_: This API allows you to get a Summary of important contextual messages in a conversation.
- _Comprehensive Action Items_: This API allows you to get a Summary of important contextual messages in a conversation.


### GET Insights 
Returns all the insights in a Conversation including Questions, Action Items, etc.

To Request GET Insight:
```sh
https://api.symbl.ai/v1/conversations/{conversationId}/insights 
```


| Field  | Description |
| ------ | ------ |
| id | To identify conversations uniquely |
| text | Conversation text |
| type | Type of insight. values could be [question, action_item] |
| score | Confidence score of the generated insight. value ranges from 0 to 1 |
| messagelds | Unique message identifiers of the respective messages |
| entities | List of entities found in the insight |

### cURL Request Syntax
```sh
curl "https://api.symbl.ai/v1/conversations/{conversationId}/insights" \
    -H "Authorization: Bearer $AUTH_TOKEN"
```
### Node.js Request Syntax
```sh
const request = require('request');
const authToken = '<your_auth_token>';


request.get({
   url: 'https://api.symbl.ai/v1/conversations/{conversationId}/insights',
   headers: { 'Authorization': `Bearer ${authToken}` },
   json: true
}, (err, response, body) => {
   console.log(body);
});
```
#### The above request will return a response structured as:

```sh
curl --location --request GET 'https://api.symbl.ai/v1/conversations/5526632414576640/insights' \
--header 'x-api-key: `
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
"from": {}
},
{
"id": "5660876935790592",
"text": "Did you want navy blue or royal blue?",
"type": "question",
"score": 0.9921441245153866,
"messageIds": [
"5213026535866368"
],
"from": {}
},
{
"id": "5810274487500800",
"text": "What color did you want the New Yorker in?",
"type": "question",
"score": 0.9963072322074725,
"messageIds": [
"5861300292812800"

],
"from": {}
},
{
"id": "6037045170405376",
"text": "Sure what I need to do?",
"type": "question",
"score": 0.9081042802022934,
"messageIds": [
"5191824211705856"
],
"from": {}
},
{
"id": "6098067562430464",

"text": "Okay, what ZIP code are you located in 1940, 6?",
"type": "question",
"score": 0.9296213757388787,
"messageIds": [
"5582660145512448"
],
"from": {}
},
{
"id": "6404582466912256",
"text": "Yes, mam and Mr. Johnson, do you have the Parker scarf in light blue with you now?",
"type": "question",

"score": 0.9915077116276262,
"messageIds": [
"4936662100475904"
],
"from": {}
},
]
}
``` 

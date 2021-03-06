# Webhooks (Coming Soon!)

Webhooks allow events to be sent to a specified url when an event matches the provided topic.

## Topic

A topic is composed of a subject, the subject's id, a verb, and an output type. For example the topic "player.examplePlayer.played.match" would receive events when a player with the id of examplePlayer played a match and the payload would be of type "match".

### Supported Topics

- player.playerId.played.match
- webhook.webhookId.verify.event

## Post a Webhook

```shell
curl -XPOST "https://api.dc01.gamelockerapp.com/shards/na/webhooks" \
  -H "Authorization: Bearer <api-key>" \
  -H "Accept: application/vnd.api+json"
```

This endpoint creates a webhook

Note: A verification event will be sent to the url (see supported events above). If the request does not succeed, the webhook will not be created.

### HTTP Request

`POST https://api.dc01.gamelockerapp.com/shards/shard_id/webhooks`

### Parameters

Parameter | Default | Description
--------- | ------- | -----------
url       |         | The callback url (must be accepting requests when the webhook is stored and will receive a verification event)
topic     |         | The subscription topic (i.e. player.ExamplePlayerID.playedMatch)

## Get Webhooks

```shell
curl "https://api.dc01.gamelockerapp.com/webhooks \
  -H "Authorization: Bearer <api-key>" \
  -H "Accept: application/vnd.api+json"
```

This endpoint returns all webhooks

### HTTP Request

`GET https://api.dc01.gamelockerapp.com/webhooks`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------

## Update Webhook

```shell
curl -XPUT "https://api.dc01.gamelockerapp.com/webhooks/{id} \
  -H "Authorization: Bearer <api-key>" \
  -H "Accept: application/vnd.api+json"
```

This endpoint updates a webhook

### HTTP Request

`PUT https://api.dc01.gamelockerapp.com/webhooks/{id}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id        |         | The id of the webhook as provided with the POST request to create it.

## Delete Webhook

```shell
curl -XDELETE "https://api.dc01.gamelockerapp.com/webhooks/{id} \
  -H "Authorization: Bearer <api-key>" \
  -H "Accept: application/vnd.api+json"
```

This endpoint removes a webhook

### HTTP Request

`DELETE https://api.dc01.gamelockerapp.com/webhooks/{id}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id        |         | The id of the webhook as provided with the POST request to create it.

## Limits

The number of webhooks that can be created is limited to 100 per app. All create requests after the limit has been exceeded will return a response code of 400.

## Webhook

```json
{
  "attributes": {
      "url": "http://test.callbackurl.com",
      "topic": "player.playerId.playedMatch"
  },
  "id": "fb374a7b-78be-4fcc-83ed-6a532a8a6f55",
  "type": "webhook"
}
```

## Event

### Authorization

For signing requests we use the HMAC authentication scheme (similar to AWS) with your JWT used as the secret.

The authorization header is in the following format:

```
Authorization: gamelocker APP:SIGNATURE
```

The signature includes the following:

- request method
- Content-MD5 header
- Content-Type header
- Date header
- request url path

Note: Content-MD5 is the md5 sum of the request body and can be used to verify that the body has not been modified.

### Payload

```json
{
  "attributes": {
      "topic": "player.playerId.played.match"
      "payload": "{"type":"match"}"
  },
  "id": "fb374a7b-78be-4fcc-83ed-6a532a8a6f55",
  "type": "event"
}
```

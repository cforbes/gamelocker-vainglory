# Webhooks (Coming Soon!)

Webhooks allow events to be sent to a specified url when an event matches the provided topic.

## Topic

A topic is composed of a subject, the subject's id, a verb, and an output type. For example the topic "player.examplePlayer.played.match" would receive events when a player with the id of examplePlayer played a match and the payload would be of type "match".

### Supported Topics

- player.playerId.played.match

## Post a Webhook

```shell
curl -XPOST "https://api.dc01.gamelockerapp.com/shards/na/webhooks" \
  -H "Authorization: Bearer <api-key>" \
  -H "Accept: application/vnd.api+json"
```

This endpoint creates a webhook

### HTTP Request

`POST https://api.dc01.gamelockerapp.com/shards/shard_id/webhooks`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
url       |         | The callback url (must be accepting requests when the webhook is stored and will receive a verification event)
----------|---------|------------
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
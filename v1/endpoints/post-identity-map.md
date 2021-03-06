[UID2 Documentation](../../README.md) > v1 > [Endpoints](./README.md) > POST /identity/map

# POST /identity/map

Retrieve advertising and bucket IDs for multiple email addresses or email hashes. Send a maximum of 10,000 combined `email` or `email_hash` per request.

## Request 

```POST '{environment}/{version}/identity/map'```

###  Request Properties

| Property | Data Type | Attributes | Description |
| --- | --- | --- | --- |
| `email` | List of `string` | Conditionally Required | A list of normalized email addresses for multiple users. Required when `email_hash` is not included in the request. |
| `email_hash` | List of `string` | Conditionally Required | A list of SHA256 hashes of normalized email addresses for multiple users. Required when `email` is not included in the request. |

#### Example Request Using an Email Address and an Email Hash

```curl
curl -L -X POST 'https://integ.uidapi.com/identity/map' -H 'Authorization: Bearer YourTokenBV3tua4BXNw+HVUFpxLlGy8nWN6mtgMlIk=' -H 'Content-Type: application/json' --data-raw '{
    "email":[
        "user@example.com"
    ],
    "email_hash":[
        "795BCB4BF560F9867AFB3DE2D0D3A94976324007C45EA099EC14E90231540547"
    ]    
}'
```

## Response

The response is a JSON object containing the user's UID2 identifier and bucket identifier.

```json
{
    "mapped": [
        {
            "identifier": "user@example.com",
            "advertising_id": "AdvtiSuYWAZSYe8t4n6sQx0gshoHYZdOzg9qUn/eKgE=",
            "bucket_id": "bucketId"
        },
        {
            "identifier": "795BCB4BF560F9867AFB3DE2D0D3A94976324007C45EA099EC14E90231540547",
            "advertising_id": "AdvIvSiaum0P5s3X/7X8h8sz+OhF2IG8DNbEnkWSbYM=",
            "bucket_id": "bucketId"
        }
    ]
}
```

## Body Response Properties

| Property | Data Type | Description |
| --- | --- | --- |
| `mapped.identifier` | `string` | The `email` or `email_hash` provided in the request. |
| `mapped.advertising_id` | `string` | The identity's advertising ID. |
| `mapped.bucket_id` | `string` | Bucket Id corresponding to that User identifier. |
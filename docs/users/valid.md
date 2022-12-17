# Is token valid

```https://extiri.com/api/1/users/valid/<token>```

Method: `GET`

This endpoint will return success HTTP response (200) if token is valid and unathorized HTTP response, if token is invalid (it doesn't exist or it expired).

## Parameters
- token (required) - token, for example: `C05D571B-E7F0-486D-98C9-7EF369F43CB7`

## Success response

Ok

## Example

Request:

```https://extiri.com/api/1/users/valid/0538C682-8D6D-4998-9990-7A7AD7BD5E13```

Response:

```json
Ok
```
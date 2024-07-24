# Get user

```https://extiri.com/api/1/users/get/<user's id>```

Method: `GET`

This endpoint will return user with specified id.

## Parameters
- user's id (required) - id of user, for example: `C05D571B-E7F0-486D-98C9-7EF369F43CB7`

## Success response

- id - id of user.
- name - string containing name of user.

## Example

Request:

```https://extiri.com/api/1/users/get/0538C682-8D6D-4998-9990-7A7AD7BD5E13```

Response:

```json
{
  "id": "0538C682-8D6D-4998-9990-7A7AD7BD5E13",
  "name": "Wiktor Wójcik" 
}
```
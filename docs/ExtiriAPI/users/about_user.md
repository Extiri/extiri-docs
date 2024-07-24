# Get user

```https://extiri.com/api/1/users/me```

Method: `GET`

This endpoint will return information about user with specified session token.

## Parameters
### Headers
- Authorization header (required) - bearer authorization using session token, for example: `Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47`

## Success response

- id - id of user.
- name - name of user.
- email - email of user.

## Example

Request:

```https://extiri.com/api/1/users/me```

### Header

```
Authorization: Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA4
```

Response:

```json
{
  "id": "AA2EE547-BBEB-45B6-89CA-4ABDF32E646E",
  "name": "Wiktor Wójcik",
  "email": "example@example.com"
}
```
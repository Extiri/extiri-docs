# Logout user

```https://extiri.com/api/1/users/logout```

Method: `GET`

This endpoint will log out specified user. Token will be invalidated.

## Parameters
### Headers
- Authorization header (required) - bearer authorization using session token, for example: `Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47`

## Success response

Ok

## Example

Request:

```https://extiri.com/api/1/users/logout```

### Header

```
Authorization: Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA4
```

Response:

```
OK
```
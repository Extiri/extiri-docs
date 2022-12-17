# Logout user

```https://extiri.com/api/1/users/logout```

Method: `GET`

This endpoint will delete specified user. The account will be deleted within 7 days. Account can be restored by logging in during this period.

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
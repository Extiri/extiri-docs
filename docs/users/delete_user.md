# Delete user

```https://extiri.com/api/1/users/delete```

Method: `DELETE`

This endpoint will delete specified user. The account will be deleted within 7 days. Account can be restored by logging in during this period.

## Parameters
### Headers
- Authorization header (required) - basic authorization using email and password concatenated using : and encoded using Base-64, for example: (not encoded) `example@example.com:S@meVeryP0werfu1Passw0rd` (encoded) `ZXhhbXBsZUBleGFtcGxlLmNvbTpleGFtcGxlUGFzc3dvcmQ=`

## Success response

Ok

## Example

Request:

```https://extiri.com/api/1/users/delete```

### Header

```
Authorization: Basic ZXhhbXBsZUBleGFtcGxlLmNvbTpleGFtcGxlUGFzc3dvcmQ=
```

Response:

```
Ok
```
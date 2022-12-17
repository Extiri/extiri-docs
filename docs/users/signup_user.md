# Signup user

```https://extiri.com/api/1/users/signup```

Method: `POST`

This endpoint will create account. The ser will receive email in which there is confirmation link. If the user doesn't confirm account within 24 hours, it will be deleted.

## Parameters
### Body
- name - name of user.
- email - email of user.
- password - password of user. It must be at least 8 characters long, contain at least 1 lowercase character, 1 uppercase character, 1 digit and must not be equal to either user's email or username.

## Success response

```
Account has been succesfully registered. You will need to confirm it using link in e-mail sent to you. If you don't see it, check Spam folder.
```

## Example

Request:

```https://extiri.com/api/1/users/signup```

### Body

```json
{
  "name": "Wiktor Wójcik",
  "email": "example@example.com",
  "password": "S@meVeryP0werfu1Passw0rd"
}
```

Response:

```
Account has been succesfully registered. You will need to confirm it using link in e-mail sent to you. If you don't see it, check Spam folder.
```
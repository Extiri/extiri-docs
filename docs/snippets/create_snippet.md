# Create snippet

```https://extiri.com/api/1/snippets/create```

Method: `POST`

This endpoint will create snippet with specified content. If server is set to hide new snippets, snippet's isHidden field will be set to `true` and will eventually checked and either approved or deleted, otherwise snippet is simply created.

## Parameters
### Headers
- Authorization header (required) - bearer authorization using session token, for example: `Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47`

### Body
- title - string containing title of snippet.
- description - string containing description of snippet.
- code - string containing code of snippet.
- category - string containing one of predefined categories for snippet.
- language - string containing language key for language of code.

## Success response

- id - id of snippet.
- title - string containing title of snippet.
- desc - string containing description of snippet.
- code - string containing code of snippet.
- category - string containing one of predefined categories for snippet.
- language - string containing language key for language of code.
- creationDate - string containing ISO-8601 encoded date of snippet creation.
- isHidden - bool informing whether snippet should be shown.

## Example

Request:

```https://extiri.com/api/1/snippets/create```

### Header

```
Authorization: Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47
```

### Body

```json
{
  "title": "Lorem ipsum",
  "language": "swift",
  "category": "UI",
  "description": "Dolor sit amet.",
  "code": "print(\"Hello, world!\")"
}
```

Response:

```json
{
  "id": "4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47",
  "title": "Lorem ipsum",
  "language": "swift",
  "category": "UI",
  "desc": "Dolor sit amet.",
  "code": "print(\"Hello, world!\")",
  "creator": "2AAA76CF-87D8-4446-83BF-C22B9AEF531F",
  "creationDate": "2022-03-20T16:29:46Z",
  "isHidden": false
}
```
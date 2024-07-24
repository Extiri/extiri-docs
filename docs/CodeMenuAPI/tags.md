# Get tags

```http://127.0.0.1:1300/v1/tags/?key=<key>```

Method: `GET`

This endpoint will return snippets stored in CodeMenu.

## Parameters
- key (optional, default: none) - user-specified protection key.
## Success response

- array of tags
  - id (string)
  - name (string)

## Example

Request: 
```http://localhost:1300/v1/tags```

Response:
```json
[
  {
    "id": "1E126396-D086-4B00-96B7-C2CFE346F90A",
    "name": "Favourite"
  },
  {
    "name": "Prompts",
    "id": "44DF78CD-091A-428F-8855-35DA66551C27"
  }
]
```
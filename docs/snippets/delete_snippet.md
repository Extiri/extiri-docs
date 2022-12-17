# Delete snippet

```https://extiri.com/api/1/snippets/delete/<snippets id>```

Method: `DELETE`

This endpoint will delete snippet with specified id.

## Parameters
- snippets id (required) - id of snippet, for example: `C05D571B-E7F0-486D-98C9-7EF369F43CB7`

### Headers
- Authorization header (required) - bearer authorization using session token, for example: `Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47`

## Success response

Ok

## Example

Request:

```https://extiri.com/api/1/snippets/delete/C05D571B-E7F0-486D-98C9-7EF369F43CB7```

### Header

```
Authorization: Bearer 4FB7B11C-C8E6-487C-92D8-EFB0CCBAEA47
```

Response:

```json
Ok
```
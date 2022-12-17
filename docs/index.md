# Home

This webstie contains documentation for Extiri API version 1.x.

!!! attention

    Extiri API is currently in beta. There may be breaking changes between versions.

## Contact

If you have any questions, contact Wiktor Wójcik at wiktor.wojcik@extiri.com or using other official channel.

## Access
### GraphQL
You can send GrapQL request to `https://extiri.com/graphql` endpoint. You need to send them with content type header set to `application/json`. There is also a editor at
`https://extiri.com/graphiql` which is also where documentation for GraphQL is.
### REST
All of REST endpoints start with `https://extiri.com/api/1/`. All endpoints requiring content support only JSON content type.

When request fails, it usually returns a response of following form:
``` json
{
  "error": true,
  "reason": "This string contains reason for failure."
}
```
It contains error field always set to true, a reason field, containing string describing reason of error.

## Server
Maximum request size is 100 MB. Server also supports gzip compression with maximum size of data 30 MB.

Server also limits number of requests per second per client to 16.
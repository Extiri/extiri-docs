## Extiri API
This section contains documentation of Extiri API.

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

## Open source and self-hosting

Extiri API is fully open source. It's written in Swift using Vapor framework. It uses Postgres as the database and SendGrid API as the e-mail provider. You can learn more [here](https://github.com/Extiri/ExtiriServer). There is also a web app for Snippets Store, which is also [open source](https://github.com/Extiri/extiri-web). It's written in Svelte and uses SvelteKit.

You can self-host both projects to have your own database of snippets. Personal or for a team. [CodeMenu](https://extiri.com/codemenu.html) (snippets manager by Extiri) supports changing server's address.
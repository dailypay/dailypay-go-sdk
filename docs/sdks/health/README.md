# Health
(*Health*)

## Overview

The _health_ endpoint provides a simple health check for the API. 

**Functionality:** Check the status of the API to ensure it is functioning
correctly.


### Available Operations

* [GetHealth](#gethealth) - Verify the status of the API

## GetHealth

Returns a 200 status code if the API is up and running.


### Example Usage

<!-- UsageSnippet language="go" operationID="getHealth" method="get" path="/rest/health" -->
```go
package main

import(
	"context"
	"undefined"
	"undefined/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := dailypay.New(
        dailypay.WithSecurity(components.Security{
            OauthUserToken: dailypay.String("<YOUR_OAUTH_USER_TOKEN_HERE>"),
        }),
    )

    res, err := s.Health.GetHealth(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.Health200 != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.GetHealthResponse](../../models/operations/gethealthresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |
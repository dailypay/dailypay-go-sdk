# People
(*People*)

## Overview

The _people_ endpoint allows you to see information related to who owns 
resources such as jobs and accounts.

**Functionality:** Retrieve limited details about a person, including
their name, global status, and state of residence.


### Available Operations

* [Read](#read) - Get a person object
* [Update](#update) - Update a person

## Read

Returns details about a person.

### Example Usage

<!-- UsageSnippet language="go" operationID="readPerson" method="get" path="/rest/people/{person_id}" -->
```go
package main

import(
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := dailypay.New(
        dailypay.WithVersion(3),
        dailypay.WithSecurity(components.Security{
            OauthUserToken: dailypay.String("<YOUR_OAUTH_USER_TOKEN_HERE>"),
        }),
    )

    res, err := s.People.Read(ctx, operations.ReadPersonRequest{
        PersonID: "aa860051-c411-4709-9685-c1b716df611b",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.PersonData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `ctx`                                                                        | [context.Context](https://pkg.go.dev/context#Context)                        | :heavy_check_mark:                                                           | The context to use for the request.                                          |
| `request`                                                                    | [operations.ReadPersonRequest](../../models/operations/readpersonrequest.md) | :heavy_check_mark:                                                           | The request object to use for the request.                                   |
| `opts`                                                                       | [][operations.Option](../../models/operations/option.md)                     | :heavy_minus_sign:                                                           | The options for this request.                                                |

### Response

**[*operations.ReadPersonResponse](../../models/operations/readpersonresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorNotFound     | 404                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |

## Update

Update a person object.

### Example Usage

<!-- UsageSnippet language="go" operationID="updatePerson" method="patch" path="/rest/people/{person_id}" -->
```go
package main

import(
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := dailypay.New(
        dailypay.WithVersion(3),
        dailypay.WithSecurity(components.Security{
            OauthUserToken: dailypay.String("<YOUR_OAUTH_USER_TOKEN_HERE>"),
        }),
    )

    res, err := s.People.Update(ctx, operations.UpdatePersonRequest{
        PersonID: "aa860051-c411-4709-9685-c1b716df611b",
        PersonData: components.PersonDataInput{
            Data: components.PersonResourceInput{
                ID: "aa860051-c411-4709-9685-c1b716df611b",
                Attributes: components.PersonAttributesInput{
                    StateOfResidence: dailypay.String("NY"),
                },
            },
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.PersonData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.UpdatePersonRequest](../../models/operations/updatepersonrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.UpdatePersonResponse](../../models/operations/updatepersonresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorNotFound     | 404                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |
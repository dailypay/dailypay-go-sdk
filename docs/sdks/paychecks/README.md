# Paychecks
(*Paychecks*)

## Overview

The _paychecks_ endpoint provides detailed information about paychecks. 
You can retrieve individual paycheck details, including the
person and job associated with the paycheck, its status, pay period,
expected deposit date, total debited amount, withholdings, earnings, and
currency.

**Functionality:** Retrieve specific paycheck details, including payee and
job information, and monitor the status and financial details of each
paycheck.


### Available Operations

* [Read](#read) - Get a Paycheck object
* [List](#list) - Get a list of paycheck objects

## Read

Returns details about a paycheck object.

### Example Usage

<!-- UsageSnippet language="go" operationID="readPaycheck" method="get" path="/rest/paychecks/{paycheck_id}" -->
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

    res, err := s.Paychecks.Read(ctx, operations.ReadPaycheckRequest{
        PaycheckID: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.PaycheckData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.ReadPaycheckRequest](../../models/operations/readpaycheckrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.ReadPaycheckResponse](../../models/operations/readpaycheckresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorNotFound     | 404                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |

## List

Returns a collection of paycheck objects. This object details a person's pay and pay period.
See [Filtering Paychecks](https://developer.dailypay.com/tag/Filtering#section/Supported-Endpoint-Filters) for a description of filterable fields.


### Example Usage

<!-- UsageSnippet language="go" operationID="listPaychecks" method="get" path="/rest/paychecks" -->
```go
package main

import(
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	"github.com/dailypay/dailypay-go-sdk/types"
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

    res, err := s.Paychecks.List(ctx, operations.ListPaychecksRequest{
        FilterDepositExpectedAtGte: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
        FilterDepositExpectedAtLt: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
        FilterPayPeriodEndsAtGte: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
        FilterPayPeriodEndsAtLt: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
        FilterPayPeriodStartsAtGte: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
        FilterPayPeriodStartsAtLt: types.MustNewTimeFromString("2023-03-15T04:00:00Z"),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.PaychecksData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                          | Type                                                                               | Required                                                                           | Description                                                                        |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `ctx`                                                                              | [context.Context](https://pkg.go.dev/context#Context)                              | :heavy_check_mark:                                                                 | The context to use for the request.                                                |
| `request`                                                                          | [operations.ListPaychecksRequest](../../models/operations/listpaychecksrequest.md) | :heavy_check_mark:                                                                 | The request object to use for the request.                                         |
| `opts`                                                                             | [][operations.Option](../../models/operations/option.md)                           | :heavy_minus_sign:                                                                 | The options for this request.                                                      |

### Response

**[*operations.ListPaychecksResponse](../../models/operations/listpaychecksresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |
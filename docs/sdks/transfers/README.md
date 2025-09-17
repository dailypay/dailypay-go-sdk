# Transfers
(*Transfers*)

## Overview

The _transfers_ endpoint allows you to initiate and track money movement.  You can access transfer details, including the transfer's unique ID, amount, currency, status, schedule, submission and resolution times, fees, and related links to the involved parties.

**Functionality** Retrieve transfer information, monitor transfer statuses, view transfer schedules, and access relevant links for the source, destination, and origin of the transfer.

**Important** - Account origin: a user initiated movement of money from one account to another - Paycheck origin: an automatic (system-generated) movement of money as part of payroll


### Available Operations

* [Read](#read) - Get a transfer object
* [List](#list) - Get a list of transfers
* [Create](#create) - Request a transfer

## Read

Returns details about a transfer of money from one account to another. 

Created when a person takes an advance against a future paycheck, or on a daily basis when available balance is updated based on current employment.


### Example Usage

<!-- UsageSnippet language="go" operationID="readTransfer" method="get" path="/rest/transfers/{transfer_id}" -->
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
            OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
                ClientID: "<YOUR_CLIENT_ID_HERE>",
                ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
                TokenURL: "<YOUR_TOKEN_URL_HERE>",
            },
        }),
    )

    res, err := s.Transfers.Read(ctx, operations.ReadTransferRequest{
        TransferID: "aba332a2-24a2-46de-8257-5040e71ab210",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.TransferData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.ReadTransferRequest](../../models/operations/readtransferrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.ReadTransferResponse](../../models/operations/readtransferresponse.md), error**

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

Returns a list of transfer objects.
See [Filtering Transfers](https://developer.dailypay.com/tag/Filtering#section/Supported-Endpoint-Filters) for a description of filterable fields.


### Example Usage

<!-- UsageSnippet language="go" operationID="listTransfers" method="get" path="/rest/transfers" -->
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
            OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
                ClientID: "<YOUR_CLIENT_ID_HERE>",
                ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
                TokenURL: "<YOUR_TOKEN_URL_HERE>",
            },
        }),
    )

    res, err := s.Transfers.List(ctx, operations.ListTransfersRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.TransfersData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                          | Type                                                                               | Required                                                                           | Description                                                                        |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `ctx`                                                                              | [context.Context](https://pkg.go.dev/context#Context)                              | :heavy_check_mark:                                                                 | The context to use for the request.                                                |
| `request`                                                                          | [operations.ListTransfersRequest](../../models/operations/listtransfersrequest.md) | :heavy_check_mark:                                                                 | The request object to use for the request.                                         |
| `opts`                                                                             | [][operations.Option](../../models/operations/option.md)                           | :heavy_minus_sign:                                                                 | The options for this request.                                                      |

### Response

**[*operations.ListTransfersResponse](../../models/operations/listtransfersresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |

## Create

Request transfer of funds from an `EARNINGS_BALANCE` account to a
personal `DEPOSITORY` or `CARD` account.


### Example Usage

<!-- UsageSnippet language="go" operationID="createTransfer" method="post" path="/rest/transfers" -->
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
            OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
                ClientID: "<YOUR_CLIENT_ID_HERE>",
                ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
                TokenURL: "<YOUR_TOKEN_URL_HERE>",
            },
        }),
    )

    res, err := s.Transfers.Create(ctx, operations.CreateTransferRequest{
        IdempotencyKey: "ea9f2225-403b-4e2c-93b0-0eda090ffa65",
        TransferCreateData: components.TransferCreateData{
            Data: components.TransferCreateResource{
                ID: dailypay.Pointer("aba332a2-24a2-46de-8257-5040e71ab210"),
                Attributes: components.TransferAttributesInput{
                    Preview: dailypay.Pointer(true),
                    Amount: 2500,
                    Currency: "USD",
                    Schedule: components.TransferAttributesScheduleWithinThirtyMinutes,
                },
                Relationships: components.TransferCreateRelationships{
                    Origin: components.AccountRelationship{
                        Data: components.AccountIdentifier{
                            ID: "2bc7d781-3247-46f6-b60f-4090d214936a",
                        },
                    },
                    Destination: components.AccountRelationship{
                        Data: components.AccountIdentifier{
                            ID: "2bc7d781-3247-46f6-b60f-4090d214936a",
                        },
                    },
                    Person: components.PersonRelationship{
                        Data: components.PersonIdentifier{
                            ID: "3fa8f641-5717-4562-b3fc-2c963f66afa6",
                        },
                    },
                },
            },
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.TransferData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                            | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `ctx`                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                | :heavy_check_mark:                                                                   | The context to use for the request.                                                  |
| `request`                                                                            | [operations.CreateTransferRequest](../../models/operations/createtransferrequest.md) | :heavy_check_mark:                                                                   | The request object to use for the request.                                           |
| `opts`                                                                               | [][operations.Option](../../models/operations/option.md)                             | :heavy_minus_sign:                                                                   | The options for this request.                                                        |

### Response

**[*operations.CreateTransferResponse](../../models/operations/createtransferresponse.md), error**

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| apierrors.TransferCreateError | 400                           | application/vnd.api+json      |
| apierrors.ErrorUnauthorized   | 401                           | application/vnd.api+json      |
| apierrors.ErrorForbidden      | 403                           | application/vnd.api+json      |
| apierrors.ErrorUnexpected     | 500                           | application/vnd.api+json      |
| apierrors.APIException        | 4XX, 5XX                      | \*/\*                         |
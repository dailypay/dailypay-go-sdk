# Accounts

## Overview

The _accounts_ endpoint provides comprehensive information about money
accounts. You can retrieve account details, including the
account's unique ID, a link to the account holder, type, subtype,
verification status, balance details, transfer capabilities, and
user-specific information such as names, routing numbers, and partial
account numbers.


**Functionality:** Access detailed user account information, verify
account balances, view transfer capabilities, and access user-specific
details associated with each account.


### Available Operations

* [Read](#read) - Get an Account object
* [List](#list) - Get a list of Account objects
* [Create](#create) - Create an Account object

## Read

Returns details about an account. This object represents a person's bank accounts, debit and pay cards, and earnings balance accounts.

### Example Usage

<!-- UsageSnippet language="go" operationID="readAccount" method="get" path="/rest/accounts/{account_id}" -->
```go
package main

import(
	"context"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	dailypay "github.com/dailypay/dailypay-go-sdk"
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

    res, err := s.Accounts.Read(ctx, operations.ReadAccountRequest{
        AccountID: "2bc7d781-3247-46f6-b60f-4090d214936a",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.AccountData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `ctx`                                                                          | [context.Context](https://pkg.go.dev/context#Context)                          | :heavy_check_mark:                                                             | The context to use for the request.                                            |
| `request`                                                                      | [operations.ReadAccountRequest](../../models/operations/readaccountrequest.md) | :heavy_check_mark:                                                             | The request object to use for the request.                                     |
| `opts`                                                                         | [][operations.Option](../../models/operations/option.md)                       | :heavy_minus_sign:                                                             | The options for this request.                                                  |

### Response

**[*operations.ReadAccountResponse](../../models/operations/readaccountresponse.md), error**

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

Returns a list of account objects. An account object represents a person's bank accounts, debit and pay cards, and earnings balance accounts.


### Example Usage

<!-- UsageSnippet language="go" operationID="listAccounts" method="get" path="/rest/accounts" -->
```go
package main

import(
	"context"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	dailypay "github.com/dailypay/dailypay-go-sdk"
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

    res, err := s.Accounts.List(ctx, operations.ListAccountsRequest{
        FilterPersonID: dailypay.Pointer("aa860051-c411-4709-9685-c1b716df611b"),
        FilterAccountType: components.FilterAccountTypeEarningsBalance.ToPointer(),
        FilterSubtype: dailypay.Pointer("ODP"),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.AccountsData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.ListAccountsRequest](../../models/operations/listaccountsrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.ListAccountsResponse](../../models/operations/listaccountsresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |

## Create

Create an account object to store a person's bank or card information as a destination for funds.

### Example Usage

<!-- UsageSnippet language="go" operationID="createAccount" method="post" path="/rest/accounts" -->
```go
package main

import(
	"context"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	dailypay "github.com/dailypay/dailypay-go-sdk"
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

    res, err := s.Accounts.Create(ctx, components.AccountDataInput{
        Data: components.AccountResourceInput{
            Attributes: components.CreateAccountAttributesInputDepositoryInput(
                components.DepositoryInput{
                    Name: "Acme Bank Checking Account",
                    Subtype: components.AccountAttributesDepositorySubtypeChecking,
                    DepositoryAccountDetails: components.DepositoryAccountDetails{
                        FirstName: "Edith",
                        LastName: "Clarke",
                        RoutingNumber: "XXXXX2021",
                        AccountNumber: "XXXXXX4321",
                    },
                },
            ),
            Relationships: components.AccountRelationships{
                Person: components.PersonRelationship{
                    Data: components.PersonIdentifier{
                        ID: "3fa8f641-5717-4562-b3fc-2c963f66afa6",
                    },
                },
            },
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.AccountData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |
| `request`                                                                  | [components.AccountDataInput](../../models/components/accountdatainput.md) | :heavy_check_mark:                                                         | The request object to use for the request.                                 |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |

### Response

**[*operations.CreateAccountResponse](../../models/operations/createaccountresponse.md), error**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| apierrors.AccountCreateError | 400                          | application/vnd.api+json     |
| apierrors.ErrorUnauthorized  | 401                          | application/vnd.api+json     |
| apierrors.ErrorForbidden     | 403                          | application/vnd.api+json     |
| apierrors.ErrorUnexpected    | 500                          | application/vnd.api+json     |
| apierrors.APIException       | 4XX, 5XX                     | \*/\*                        |
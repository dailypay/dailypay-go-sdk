# CardTokenization

## Overview

Securely tokenize personal cards for use in the accounts API.

### Available Operations

* [Create](#create) - Obtain a card token

## Create

Obtain a PCI DSS Compliant card token. This token must be used in order to add a card to a user’s DailyPay account.

### Example Usage

<!-- UsageSnippet language="go" operationID="createGenericCardToken" method="post" path="/cards/generic" -->
```go
package main

import(
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := dailypay.New()

    res, err := s.CardTokenization.Create(ctx, operations.CreateGenericCardTokenRequest{
        FirstName: "Edith",
        LastName: "Clarke",
        CardNumber: "4007589999999912",
        ExpirationYear: "2027",
        ExpirationMonth: "02",
        Cvv: dailypay.Pointer("123"),
        AddressLineOne: "123 Kebly Street",
        AddressLineTwo: dailypay.Pointer("Unit C"),
        AddressCity: "Fort Lee",
        AddressState: "NJ",
        AddressZipCode: "07237",
        AddressCountry: "US",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Object != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                | :heavy_check_mark:                                                                                   | The context to use for the request.                                                                  |
| `request`                                                                                            | [operations.CreateGenericCardTokenRequest](../../models/operations/creategenericcardtokenrequest.md) | :heavy_check_mark:                                                                                   | The request object to use for the request.                                                           |
| `opts`                                                                                               | [][operations.Option](../../models/operations/option.md)                                             | :heavy_minus_sign:                                                                                   | The options for this request.                                                                        |

### Response

**[*operations.CreateGenericCardTokenResponse](../../models/operations/creategenericcardtokenresponse.md), error**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| apierrors.APIException | 4XX, 5XX               | \*/\*                  |
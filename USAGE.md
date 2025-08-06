<!-- Start SDK Example Usage [usage] -->
### Look up accounts

Fetch a list of accounts, including earnings balance accounts.

```go
package main

import (
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

	res, err := s.Accounts.List(ctx, operations.ListAccountsRequest{
		FilterAccountType: components.FilterAccountTypeEarningsBalance.ToPointer(),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.AccountsData != nil {
		// handle response
	}
}

```

### Request a transfer

Initiate a transfer of funds from an earnings balance account to a personal depository or card account.

```go
package main

import (
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

	res, err := s.Transfers.Create(ctx, operations.CreateTransferRequest{
		IdempotencyKey: "ea9f2225-403b-4e2c-93b0-0eda090ffa65",
		TransferCreateData: components.TransferCreateData{
			Data: components.TransferCreateResource{
				ID: dailypay.String("aba332a2-24a2-46de-8257-5040e71ab210"),
				Attributes: components.TransferAttributesInput{
					Preview:  dailypay.Bool(true),
					Amount:   2500,
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
<!-- End SDK Example Usage [usage] -->
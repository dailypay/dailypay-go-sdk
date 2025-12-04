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
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Accounts.List(ctx, operations.ListAccountsRequest{
		FilterPersonID:    dailypay.Pointer("aa860051-c411-4709-9685-c1b716df611b"),
		FilterAccountType: components.FilterAccountTypeEarningsBalance.ToPointer(),
		FilterSubtype:     dailypay.Pointer("ODP"),
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
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Transfers.Create(ctx, operations.CreateTransferRequest{
		Include:        dailypay.Pointer("estimated_funding_sources,final_funding_sources"),
		IdempotencyKey: "e2736aa1-78c4-4cc6-b0a6-848e733f232a",
		TransferCreateData: components.TransferCreateData{
			Data: components.TransferCreateResource{
				Attributes: components.TransferAttributesInput{
					Preview:  dailypay.Pointer(true),
					Amount:   15000,
					Currency: "USD",
					Schedule: components.TransferAttributesScheduleWithinThirtyMinutes,
				},
				Relationships: components.TransferCreateRelationships{
					Origin: components.AccountRelationship{
						Data: components.AccountIdentifier{
							ID: "123e4567-e89b-12d3-a456-426614174000",
						},
					},
					Destination: components.AccountRelationship{
						Data: components.AccountIdentifier{
							ID: "223e4567-e89b-12d3-a456-426614174001",
						},
					},
					Person: components.PersonRelationship{
						Data: components.PersonIdentifier{
							ID: "aa860051-c411-4709-9685-c1b716df611b",
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
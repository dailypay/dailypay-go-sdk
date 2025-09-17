# dailypay

Developer-friendly & type-safe Go SDK specifically catered to leverage *dailypay* API.

<div align="left">
    <a href="https://www.speakeasy.com/?utm_source=dailypay&utm_campaign=go"><img src="https://custom-icon-badges.demolab.com/badge/-Built%20By%20Speakeasy-212015?style=for-the-badge&logoColor=FBE331&logo=speakeasy&labelColor=545454" /></a>
    <a href="https://opensource.org/licenses/MIT">
        <img src="https://img.shields.io/badge/License-MIT-blue.svg" style="width: 100px; height: 28px;" />
    </a>
</div>

<!-- No Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [dailypay](#dailypay)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add the SDK as a dependency to your project:
```bash
go get github.com/dailypay/dailypay-go-sdk
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

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
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Transfers.Create(ctx, operations.CreateTransferRequest{
		IdempotencyKey: "ea9f2225-403b-4e2c-93b0-0eda090ffa65",
		TransferCreateData: components.TransferCreateData{
			Data: components.TransferCreateResource{
				ID: dailypay.Pointer("aba332a2-24a2-46de-8257-5040e71ab210"),
				Attributes: components.TransferAttributesInput{
					Preview:  dailypay.Pointer(true),
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

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security schemes globally:

| Name                          | Type   | Scheme       |
| ----------------------------- | ------ | ------------ |
| `OauthClientCredentialsToken` | oauth2 | OAuth2 token |
| `OauthUserToken`              | oauth2 | OAuth2 token |

You can set the security parameters through the `WithSecurity` option when initializing the SDK client instance. The selected scheme will be used by default to authenticate with the API for all operations that support it. For example:
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
		dailypay.WithSecurity(components.Security{
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
		dailypay.WithVersion(3),
	)

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.JobData != nil {
		// handle response
	}
}

```
<!-- End Authentication [security] -->

<!-- Suggested: Use a Callback for Access Tokens -->
### Suggested: Use a Callback for Access Tokens

You can use a callback to automatically refresh and retrieve user access tokens from secure storage. Pass a callback as a security source when initializing the SDK:

```go
package main

import (
    "context"
    sdk "github.com/dailypay/dailypay-go-sdk"
    "github.com/dailypay/dailypay-go-sdk/models/components"
    "github.com/dailypay/dailypay-go-sdk/models/operations"
    "log"
)

// Example callback function to retrieve the latest access token
func securityCallback(ctx context.Context) (components.Security, error) {
    // Retrieve token from secure storage or refresh logic
    token := "<YOUR_OAUTH_USER_TOKEN_HERE>"
    return components.Security{
        OauthUserToken: sdk.String(token),
    }, nil
}

func main() {
    ctx := context.Background()

    s := sdk.New(
        sdk.WithSecuritySource(securityCallback),
        sdk.WithVersion(3),
    )

    req := operations.ReadJobRequest{
        JobID: "aa860051-c411-4709-9685-c1b716df611b",
    }

    res, err := s.Jobs.Read(ctx, req)
    if err != nil {
        log.Fatal(err)
    }
    // handle response
}
```

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Accounts](docs/sdks/accounts/README.md)

* [Read](docs/sdks/accounts/README.md#read) - Get an Account object
* [List](docs/sdks/accounts/README.md#list) - Get a list of Account objects
* [Create](docs/sdks/accounts/README.md#create) - Create an Account object

### [Cards](docs/sdks/cards/README.md)

* [Create](docs/sdks/cards/README.md#create) - Obtain a card token

### [Health](docs/sdks/health/README.md)

* [GetHealth](docs/sdks/health/README.md#gethealth) - Verify the status of the API

### [Jobs](docs/sdks/jobs/README.md)

* [Read](docs/sdks/jobs/README.md#read) - Get a job object
* [Update](docs/sdks/jobs/README.md#update) - Update paycheck settings or deactivate a job
* [List](docs/sdks/jobs/README.md#list) - Get a list of job objects

### [Organizations](docs/sdks/organizations/README.md)

* [Read](docs/sdks/organizations/README.md#read) - Get an organization
* [List](docs/sdks/organizations/README.md#list) - List organizations

### [Paychecks](docs/sdks/paychecks/README.md)

* [Read](docs/sdks/paychecks/README.md#read) - Get a Paycheck object
* [List](docs/sdks/paychecks/README.md#list) - Get a list of paycheck objects

### [People](docs/sdks/people/README.md)

* [Read](docs/sdks/people/README.md#read) - Get a person object
* [Update](docs/sdks/people/README.md#update) - Update a person


### [Transfers](docs/sdks/transfers/README.md)

* [Read](docs/sdks/transfers/README.md#read) - Get a transfer object
* [List](docs/sdks/transfers/README.md#list) - Get a list of transfers
* [Create](docs/sdks/transfers/README.md#create) - Request a transfer

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `retry.Config` object to the call by using the `WithRetries` option:
```go
package main

import (
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"github.com/dailypay/dailypay-go-sdk/retry"
	"log"
	"models/operations"
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

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	}, operations.WithRetries(
		retry.Config{
			Strategy: "backoff",
			Backoff: &retry.BackoffStrategy{
				InitialInterval: 1,
				MaxInterval:     50,
				Exponent:        1.1,
				MaxElapsedTime:  100,
			},
			RetryConnectionErrors: false,
		}))
	if err != nil {
		log.Fatal(err)
	}
	if res.JobData != nil {
		// handle response
	}
}

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `WithRetryConfig` option at SDK initialization:
```go
package main

import (
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/components"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"github.com/dailypay/dailypay-go-sdk/retry"
	"log"
)

func main() {
	ctx := context.Background()

	s := dailypay.New(
		dailypay.WithRetryConfig(
			retry.Config{
				Strategy: "backoff",
				Backoff: &retry.BackoffStrategy{
					InitialInterval: 1,
					MaxInterval:     50,
					Exponent:        1.1,
					MaxElapsedTime:  100,
				},
				RetryConnectionErrors: false,
			}),
		dailypay.WithVersion(3),
		dailypay.WithSecurity(components.Security{
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.JobData != nil {
		// handle response
	}
}

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or an error, they will never return both.

By Default, an API error will return `apierrors.APIException`. When custom error responses are specified for an operation, the SDK may also return their associated error. You can refer to respective *Errors* tables in SDK docs for more details on possible error types for each operation.

For example, the `Read` function may return the following errors:

| Error Type                  | Status Code | Content Type             |
| --------------------------- | ----------- | ------------------------ |
| apierrors.ErrorBadRequest   | 400         | application/vnd.api+json |
| apierrors.ErrorUnauthorized | 401         | application/vnd.api+json |
| apierrors.ErrorForbidden    | 403         | application/vnd.api+json |
| apierrors.ErrorNotFound     | 404         | application/vnd.api+json |
| apierrors.ErrorUnexpected   | 500         | application/vnd.api+json |
| apierrors.APIException      | 4XX, 5XX    | \*/\*                    |

### Example

```go
package main

import (
	"context"
	"errors"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/apierrors"
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

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	})
	if err != nil {

		var e *apierrors.ErrorBadRequest
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.ErrorUnauthorized
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.ErrorForbidden
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.ErrorNotFound
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.ErrorUnexpected
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.APIException
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}
	}
}

```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Server Variables

The default server `https://api.{environment}.com` contains variables and is set to `https://api.dailypay.com` by default. To override default values, the following options are available when initializing the SDK client instance:

| Variable      | Option                                           | Supported Values                     | Default      | Description |
| ------------- | ------------------------------------------------ | ------------------------------------ | ------------ | ----------- |
| `environment` | `WithEnvironment(environment ServerEnvironment)` | - `"dailypay"`<br/>- `"dailypayuat"` | `"dailypay"` |             |

#### Example

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
		dailypay.WithEnvironment("dailypayuat"),
		dailypay.WithVersion(3),
		dailypay.WithSecurity(components.Security{
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.JobData != nil {
		// handle response
	}
}

```

### Override Server URL Per-Client

The default server can be overridden globally using the `WithServerURL(serverURL string)` option when initializing the SDK client instance. For example:
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
		dailypay.WithServerURL("https://api.dailypay.com"),
		dailypay.WithVersion(3),
		dailypay.WithSecurity(components.Security{
			OauthClientCredentialsToken: &components.SchemeOauthClientCredentialsToken{
				ClientID:     "<YOUR_CLIENT_ID_HERE>",
				ClientSecret: "<YOUR_CLIENT_SECRET_HERE>",
				TokenURL:     "<YOUR_TOKEN_URL_HERE>",
			},
		}),
	)

	res, err := s.Jobs.Read(ctx, operations.ReadJobRequest{
		JobID: "aa860051-c411-4709-9685-c1b716df611b",
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.JobData != nil {
		// handle response
	}
}

```

### Override Server URL Per-Operation

The server URL can also be overridden on a per-operation basis, provided a server list was specified for the operation. For example:
```go
package main

import (
	"context"
	dailypay "github.com/dailypay/dailypay-go-sdk"
	"github.com/dailypay/dailypay-go-sdk/models/operations"
	"log"
)

func main() {
	ctx := context.Background()

	s := dailypay.New()

	res, err := s.Cards.Create(ctx, operations.CreateGenericCardTokenRequest{
		FirstName:       "Edith",
		LastName:        "Clarke",
		CardNumber:      "4007589999999912",
		ExpirationYear:  "2027",
		ExpirationMonth: "02",
		Cvv:             dailypay.Pointer("123"),
		AddressLineOne:  "123 Kebly Street",
		AddressLineTwo:  dailypay.Pointer("Unit C"),
		AddressCity:     "Fort Lee",
		AddressState:    "NJ",
		AddressZipCode:  "07237",
		AddressCountry:  "US",
	}, operations.WithServerURL("https://payments.dailypay.com/v2"))
	if err != nil {
		log.Fatal(err)
	}
	if res.Object != nil {
		// handle response
	}
}

```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Go SDK makes API calls that wrap an internal HTTP client. The requirements for the HTTP client are very simple. It must match this interface:

```go
type HTTPClient interface {
	Do(req *http.Request) (*http.Response, error)
}
```

The built-in `net/http` client satisfies this interface and a default client based on the built-in is provided by default. To replace this default with a client of your own, you can implement this interface yourself or provide your own client configured as desired. Here's a simple example, which adds a client with a 30 second timeout.

```go
import (
	"net/http"
	"time"

	"github.com/dailypay/dailypay-go-sdk"
)

var (
	httpClient = &http.Client{Timeout: 30 * time.Second}
	sdkClient  = dailypay.New(dailypay.WithClient(httpClient))
)
```

This can be a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration.
<!-- End Custom HTTP Client [http-client] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=dailypay&utm_campaign=go)

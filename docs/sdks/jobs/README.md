# Jobs
(*Jobs*)

## Overview

The _jobs_ endpoint provides access to comprehensive information 
about a person's employment. It enables you to retrieve details about
individual jobs, including information about the organization
they work for, status, wage rate, job title, location,
paycheck settings, and related links to associated accounts.


### Available Operations

* [Read](#read) - Get a job object
* [Update](#update) - Update paycheck settings or deactivate a job
* [List](#list) - Get a list of job objects

## Read

Returns details about a person's employment.

### Example Usage

<!-- UsageSnippet language="go" operationID="readJob" method="get" path="/rest/jobs/{job_id}" -->
```go
package main

import(
	"context"
	"undefined"
	"undefined/models/components"
	"undefined/models/operations"
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

### Parameters

| Parameter                                                              | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `ctx`                                                                  | [context.Context](https://pkg.go.dev/context#Context)                  | :heavy_check_mark:                                                     | The context to use for the request.                                    |
| `request`                                                              | [operations.ReadJobRequest](../../models/operations/readjobrequest.md) | :heavy_check_mark:                                                     | The request object to use for the request.                             |
| `opts`                                                                 | [][operations.Option](../../models/operations/option.md)               | :heavy_minus_sign:                                                     | The options for this request.                                          |

### Response

**[*operations.ReadJobResponse](../../models/operations/readjobresponse.md), error**

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

Update this job to set where pay should be deposited for paychecks related to this job,  or deactivate on-demand pay for this job. 
Returns the job object if the update succeeded. Returns an error if update parameters are invalid.


### Example Usage

<!-- UsageSnippet language="go" operationID="updateJob" method="patch" path="/rest/jobs/{job_id}" -->
```go
package main

import(
	"context"
	"undefined"
	"undefined/models/components"
	"undefined/models/operations"
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

    res, err := s.Jobs.Update(ctx, operations.UpdateJobRequest{
        JobID: "e9d84b0d-92ba-43c9-93bf-7c993313fa6f",
        JobUpdateData: components.JobUpdateData{
            Data: components.Data{
                ID: "e9d84b0d-92ba-43c9-93bf-7c993313fa6f",
                Attributes: &components.JobAttributesInput{
                    ActivationStatus: components.ActivationStatusDeactivated.ToPointer(),
                },
                Relationships: &components.JobRelationshipsInput{
                    DirectDepositDefaultDepository: &components.AccountRelationship{
                        Data: components.AccountIdentifier{
                            ID: "2bc7d781-3247-46f6-b60f-4090d214936a",
                        },
                    },
                    DirectDepositDefaultCard: &components.AccountRelationship{
                        Data: components.AccountIdentifier{
                            ID: "2bc7d781-3247-46f6-b60f-4090d214936a",
                        },
                    },
                },
            },
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.JobData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |
| `request`                                                                  | [operations.UpdateJobRequest](../../models/operations/updatejobrequest.md) | :heavy_check_mark:                                                         | The request object to use for the request.                                 |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |

### Response

**[*operations.UpdateJobResponse](../../models/operations/updatejobresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.JobUpdateError    | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorNotFound     | 404                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |

## List

Returns a collection of job objects. This object represents a person's employment details.
See [Filtering Jobs](https://developer.dailypay.com/tag/Filtering#section/Supported-Endpoint-Filters) for a description of filterable fields.


### Example Usage

<!-- UsageSnippet language="go" operationID="listJobs" method="get" path="/rest/jobs" -->
```go
package main

import(
	"context"
	"undefined"
	"undefined/models/components"
	"undefined/models/operations"
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

    res, err := s.Jobs.List(ctx, operations.ListJobsRequest{})
    if err != nil {
        log.Fatal(err)
    }
    if res.JobsData != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ctx`                                                                    | [context.Context](https://pkg.go.dev/context#Context)                    | :heavy_check_mark:                                                       | The context to use for the request.                                      |
| `request`                                                                | [operations.ListJobsRequest](../../models/operations/listjobsrequest.md) | :heavy_check_mark:                                                       | The request object to use for the request.                               |
| `opts`                                                                   | [][operations.Option](../../models/operations/option.md)                 | :heavy_minus_sign:                                                       | The options for this request.                                            |

### Response

**[*operations.ListJobsResponse](../../models/operations/listjobsresponse.md), error**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| apierrors.ErrorBadRequest   | 400                         | application/vnd.api+json    |
| apierrors.ErrorUnauthorized | 401                         | application/vnd.api+json    |
| apierrors.ErrorForbidden    | 403                         | application/vnd.api+json    |
| apierrors.ErrorUnexpected   | 500                         | application/vnd.api+json    |
| apierrors.APIException      | 4XX, 5XX                    | \*/\*                       |
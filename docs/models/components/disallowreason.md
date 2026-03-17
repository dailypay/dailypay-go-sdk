# DisallowReason

The statuses and required actions are:
- `null` The person has not been disallowed, and is free to use DailyPay.
- `INACTIVE` The person has not completed registration or account verification.
- `DELINQUENT` The person has an outstanding, unrecoverable balance with DailyPay, and should contact support.
- `BANNED` Access has been revoked.


## Example Usage

```go
import (
	"github.com/dailypay/dailypay-go-sdk/models/components"
)

value := components.DisallowReasonInactive
```


## Values

| Name                       | Value                      |
| -------------------------- | -------------------------- |
| `DisallowReasonInactive`   | INACTIVE                   |
| `DisallowReasonDelinquent` | DELINQUENT                 |
| `DisallowReasonBanned`     | BANNED                     |
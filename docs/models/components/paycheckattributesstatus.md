# PaycheckAttributesStatus

A paycheck expected for an open pay period will have the status ESTIMATED. At the end of the pay period, the paycheck will begin PROCESSING. When it is sent, it will become IN_TRANSIT. Finally, once deposited in an account it will have the status DEPOSITED.

## Example Usage

```go
import (
	"github.com/dailypay/dailypay-go-sdk/models/components"
)

value := components.PaycheckAttributesStatusEstimated
```


## Values

| Name                                 | Value                                |
| ------------------------------------ | ------------------------------------ |
| `PaycheckAttributesStatusEstimated`  | ESTIMATED                            |
| `PaycheckAttributesStatusProcessing` | PROCESSING                           |
| `PaycheckAttributesStatusInTransit`  | IN_TRANSIT                           |
| `PaycheckAttributesStatusDeposited`  | DEPOSITED                            |
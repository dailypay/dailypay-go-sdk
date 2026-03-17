# TransferCreateAttributesSchedule

Set the schedule for the transfer. If not set, the transfer will be processed immediately. 
A preview transfer will never send.


## Example Usage

```go
import (
	"github.com/dailypay/dailypay-go-sdk/models/components"
)

value := components.TransferCreateAttributesScheduleWithinThirtyMinutes
```


## Values

| Name                                                  | Value                                                 |
| ----------------------------------------------------- | ----------------------------------------------------- |
| `TransferCreateAttributesScheduleWithinThirtyMinutes` | WITHIN_THIRTY_MINUTES                                 |
| `TransferCreateAttributesScheduleNextBusinessDay`     | NEXT_BUSINESS_DAY                                     |
# JobUpdateDataActivationStatus

Activation is the process of verifying that data is available for a Job,  and that a person has verified their identity as the Person associated with the Job. Only paychecks from Jobs with `activated` status will contribute to an earnings balance account.

To deactivate a job, update activation_status to `DEACTIVATED`.



## Values

| Name                                                 | Value                                                |
| ---------------------------------------------------- | ---------------------------------------------------- |
| `JobUpdateDataActivationStatusDeactivated`           | DEACTIVATED                                          |
| `JobUpdateDataActivationStatusDeactivationPending`   | DEACTIVATION_PENDING                                 |
| `JobUpdateDataActivationStatusActivationRequired`    | ACTIVATION_REQUIRED                                  |
| `JobUpdateDataActivationStatusActivationUnderReview` | ACTIVATION_UNDER_REVIEW                              |
| `JobUpdateDataActivationStatusActivated`             | ACTIVATED                                            |
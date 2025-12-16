# JobAttributesActivationStatus

Activation is the process of verifying that data is available for a Job,  and that a person has verified their identity as the Person associated with the Job. Only paychecks from Jobs with `activated` status will contribute to an earnings balance account.

To deactivate a job, update activation_status to `DEACTIVATED`.



## Values

| Name                                                 | Value                                                |
| ---------------------------------------------------- | ---------------------------------------------------- |
| `JobAttributesActivationStatusDeactivated`           | DEACTIVATED                                          |
| `JobAttributesActivationStatusDeactivationPending`   | DEACTIVATION_PENDING                                 |
| `JobAttributesActivationStatusActivationRequired`    | ACTIVATION_REQUIRED                                  |
| `JobAttributesActivationStatusActivationUnderReview` | ACTIVATION_UNDER_REVIEW                              |
| `JobAttributesActivationStatusActivated`             | ACTIVATED                                            |
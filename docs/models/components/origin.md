# Origin

Origin may be a reference to either a Paycheck or an Account.

User-created transfers always originate from an Account with `account_type` `EARNINGS_BALANCE`.

A transfer that originates from a Paycheck is a  
system-created record that describes a credit of earnings to an account with `account_type` `EARNINGS_BALANCE`.



## Supported Types

### AccountRelationship

```go
origin := components.CreateOriginAccountRelationship(components.AccountRelationship{/* values here */})
```

### PaycheckRelationship

```go
origin := components.CreateOriginPaycheckRelationship(components.PaycheckRelationship{/* values here */})
```


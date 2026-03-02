# AccountAttributes

The details of the account.


## Supported Types

### Card

```go
accountAttributes := components.CreateAccountAttributesCard(components.Card{/* values here */})
```

### EarningsBalanceReadOnly

```go
accountAttributes := components.CreateAccountAttributesEarningsBalanceReadOnly(components.EarningsBalanceReadOnly{/* values here */})
```

### Depository

```go
accountAttributes := components.CreateAccountAttributesDepository(components.Depository{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch accountAttributes.Type {
	case components.AccountAttributesTypeCard:
		// accountAttributes.Card is populated
	case components.AccountAttributesTypeEarningsBalanceReadOnly:
		// accountAttributes.EarningsBalanceReadOnly is populated
	case components.AccountAttributesTypeDepository:
		// accountAttributes.Depository is populated
}
```

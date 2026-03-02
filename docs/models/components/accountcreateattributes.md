# AccountCreateAttributes

The details of the account.


## Supported Types

### AccountCreateAttributesCard

```go
accountCreateAttributes := components.CreateAccountCreateAttributesAccountCreateAttributesCard(components.AccountCreateAttributesCard{/* values here */})
```

### AccountCreateAttributesDepository

```go
accountCreateAttributes := components.CreateAccountCreateAttributesAccountCreateAttributesDepository(components.AccountCreateAttributesDepository{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch accountCreateAttributes.Type {
	case components.AccountCreateAttributesTypeAccountCreateAttributesCard:
		// accountCreateAttributes.AccountCreateAttributesCard is populated
	case components.AccountCreateAttributesTypeAccountCreateAttributesDepository:
		// accountCreateAttributes.AccountCreateAttributesDepository is populated
}
```

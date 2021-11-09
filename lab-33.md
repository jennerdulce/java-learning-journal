# New title

- `amplify update api`
- Graphql
- Disable datastore for entire API

## Handling Date

```java
.timeAdded(new Temporal.DateTime(new Date(), 0));
```

- Parse AWS date using AWS formatter boiler plate
- 


## Connections

- Connect models by using `@connection`

```java
@key(name: "byOurItem", fields: ["businessUnitId"])
type ShoppingItem @model {
  id: ID!
  businessUnitId: ID!
  businessUnit: BusinessUnit @connection(fields: ["businessUnitId"])
}

type BusinessUnit @model{
  id: ID!
  businessName: String
  shoppingItems: [ShoppingItem] @connection(keyName: "byOurItem", fields:["id"])
}
```

## Completeable Futures to fetch Data

- Set completeable future
- Complete
- Get
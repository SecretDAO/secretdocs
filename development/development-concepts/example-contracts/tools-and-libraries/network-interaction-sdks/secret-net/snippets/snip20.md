# SNIP20

[**SecretNET.Token**](https://github.com/0xxCodemonkey/SecretNET.Token) is a layer on top of the Secret.NET which supports all methods of the [reference implementation](https://github.com/scrtlabs/snip20-reference-impl) of the [**SNIP20 contract**](https://docs.scrt.network/secret-network-documentation/development/snips/snip-20-spec-private-fungible-tokens).

`nuget install SecretNET.Token`

### Transfer SNIP-20 tokens

```csharp
var snip20Client = new SecretNET.Token.Snip20Client(secretClient);

var txExec = await snip20Client.Tx.Transfer(
                       contractAddress,
                       recipient,
                       amount, // int as string
                       codeHash,
                       txOptions: new TxOptions() { GasLimit = 5_000_000 }
                    );
```

### Send SNIP-20 Tokens

```csharp
var txExec = await snip20Client.Tx.Send(
                       contractAddress,
                       recipient,
                       amount, // int as string
                       codeHash,
                       txOptions: new TxOptions() { GasLimit = 5_000_000 }
                    );
```

### Set Viewing Key and Query Balance

```csharp
var txExec = await snip20Client.Tx.SetViewingKey(
                    contractAddress,
                    "hello",
                    txOptions: new TxOptions() { GasLimit = 100_000 });

var txQuery = await snip20Client.Query.GetBalance(
                    contractAddress, 
                    viewingKey: "hello", 
                    codeHash: codeHash
                    );
```

## Query Token Parameters

```csharp
var txQuery = await await snip20Client.Query.GetTokenInfo(
                    contractAddress, 
                    codeHash: codeHash
                    );
```

### Get Transaction History

```csharp
var txQuery = await snip20Client.Query.GetTransactionHistory(
                    contractAddress, 
                    pageSize: 10,
                    viewingKey: "hello",                     
                    codeHash: codeHash
                    );
```

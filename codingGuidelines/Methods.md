## Métodos
> As regras abaixo são validas para todos os níveis de acesso (`private`, `protected`, `internal` e `public`). 

- Pascal Case: **DoItNow**

- Nomes devem representar a ação que está sendo executada.

- Tente quebrar o comportamento do método de maneira que o fluxo do algoritmo não fique grande e possa ser lido de forma fluída e contínua, sem a necessidade de realizar saltos no arquivo de código fonte. Evite separar o comportamento de um método em blocos separados por linhas em branco. Tente extrair o comportamento destes blocos para outros métodos privados e dê nomes significativos para estes.

- Ao utilizar coleções em retornos ou parâmetros defina-os como **IEnumerable** sempre que possível. 

**Ruim:**
```csharp
var transactions = this.GetTransactions();

public IList<Transaction> GetTransactions()
{
    //do anything that returns IList<Transaction> at the end...
}

var clients = this.GetClients();
public List<Client> GetClients()
{
    //do anything that returns List<Client> at the end...
}
```

**Bom:**
```csharp
var transactions = this.GetTransactions();

public IEnumerable<Transaction> GetTransactions()
{
    //do anything that returns IEnumerable<Transaction> at the end...
}

var clients = this.GetClients();
public IEnumerable<Client> GetClients()
{
    //do anything that returns IEnumerable<Client> at the end...
}

var clientsList = clients.ToList();
```

- Sempre valide seus parâmetros de métodos públicos para evitar _side effects_ em lugares indesejados.

	**Ruim**
	```csharp
	public void Foo(object someParameter)
	{
		this.Bar(someParameter.SomeField);
	}
	```

	**Bom**
	```csharp
	public void Foo(object someParameter)
	{
		if(someParameter == null)
		{
			throw new ArgumentNullException(nameof(someParameter));
		}
		
		this.Bar(someParameter.SomeField);
	}
	```
- Para verificações de parâmetros em construtores, utilize o [operador _null coalescing_](https://docs.microsoft.com/pt-br/dotnet/csharp/language-reference/operators/null-coalescing-operator)

	```csharp
	public class Foo
	{
		private object someField;

		public Foo(object someParameter)
		{
			this.someField = someParameter ?? throw new ArgumentNullException(nameof(someParameter));
		}
	}
	```
	
	
[Home](https://github.com/Cappta/best-practices)

[Próximo](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Variables.md)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Classes.md)

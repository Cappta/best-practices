## Métodos
> As regras abaixo são validas para todos os níveis de acesso (private, protected, internal e public). 

- Pascal Case: **DoItNow**

- Nomes devem representar a ação que está sendo executada.

- Tente quebrar o comportamento do método de maneira que o fluxo do algoritmo não fique grande e possa ser lido de forma fluída e contínua, sem a necessidade de realizar saltos no arquivo de código fonte. Evite separar o comportamento de um método em blocos separados por linhas em branco. Tente extrair o comportamento destes blocos para outros métodos privados e dê nomes significativos para estes.

- Ao utilizar coleções em retornos ou parâmetros sempre defina-os como **IEnumerable**

**Ruim:**
```c#
var transactions = default(ICollection<Transaction>);
tasks = this.GetTransactions();

public IList<Transaction> GetTransactions()
{
    //do anything that returns IList<Transaction> at the end...
}

var clients = default(List<Clients>);
clients = this.GetClients();

public List<Client> GetClients()
{
    //do anything that returns List<Client> at the end...
}
```

**Bom:**
```c#
var transactions = default(IEnumerable<Transaction>);
tasks = this.GetTransactions();

public IEnumerable<Transaction> GetTransactions()
{
    //do anything that returns IEnumerable<Transaction> at the end...
}

var clients = default(IEnumerable<Clients>);
clients = this.GetClients();

public IEnumerable<Client> GetClients()
{
    //do anything that returns IEnumerable<Client> at the end...
}

var clientsList = clients.ToList();
```

- Sempre valide seus parâmetros de métodos publicos para evitar side effects em lugares indesejados.

	**Ruim**
	```c#
	public void Foo(object someParameter)
	{
		this.Bar(someParameter.SomeField);
	}
	```

	**Bom**
	```c#
	public void Foo(object someParameter)
	{
		if(someParameter == null)
		{
			throw new ArgumentNullException(nameof(someParameter));
		}
		
		this.Bar(someParameter.SomeField);
	}
	```
- Para verificações de parametros em construtores utilize o [operador null coalescing] (https://docs.microsoft.com/pt-br/dotnet/csharp/language-reference/operators/null-coalescing-operator)

	```c#
	public class Foo
	{
		private object someField;

		public Foo(object someParameter)
		{
			this.someField = someParameter ?? throw new ArgumentNullException(nameof(someParameter));
		}
	}
	```
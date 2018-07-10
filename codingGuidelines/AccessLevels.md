## Níveis de acesso

- Sempre diminuir o máximo possível o acesso

- Variaveis em contexto de classe sempre serão `private`;

- Não exponha variáveis de uma classe deixando-as públicas. Se precisar compartilhar o dado com outras classes, transforme a variável numa propriedade com `get` público
	
	**Ruim**
	```csharp
	public class Foo
	{
		public object someField;
	}
	```

	**Bom**
	```csharp
	public class Foo
	{
		public object SomeField { get; set; }
	}
	```
	
- Sempre que criar propriedades reduza ao máximo o acesso de seu _setter_ caso ela seja vital para o funcionamento da classe

	**Ruim**
	```csharp
	public class BankAccount
	{
		//setter da propriedade Balance público permite que outro trecho de código altere o saldo da conta livremente
		public decimal Balance { get; set; }
	}
	```

	**Bom**
	```csharp
	public class BankAccount
	{
		public decimal Balance { get; private set; }

		public void Deposit(decimal amount)
		{
			this.Balance += amount;
		}

		public decimal Withdraw(decimal amount)
		{
			this.Balance -= amount;
			
			return this.Balance;
		}
	}
	```

- Mantenha o _setter_ de uma _Property_ público somente caso ele seja algum tipo de configuração ou opcional;

- Assim como variáveis, sempre que criar métodos ou classes, mantenha o nível de acesso o mínimo possível.


[Home](https://github.com/Cappta/best-practices)

[Próximo](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/GIT.md)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Variables.md)
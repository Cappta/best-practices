## Níveis de acesso

- Sempre diminuir o máximo possível o acesso

- Variaveis em contexto de classe sempre serão private

- Não exponha variáveis de uma classe deixando-as públicas. Se precisar compartilhar o dado com outras classes, transforme a variável numa propriedade com get público
	
	**Ruim**
	```c#
	public class Foo
	{
		public object someField;
	}
	```

	**Bom**
	```c#
	public class Foo
	{
		public object SomeField {get;set;}
	}
	```
	
- Sempre que criar propriedades reduza ao máximo o acesso de seu setter caso ela seja vital para o funcionamento da classe

	**Ruim**
	```c#
	public class BankAccount
	{
		//setter da propriedade Balance público permite que outro trecho de código altere o saldo da conta livremente
		public decimal Balance {get;set;}
	}
	```

	**Bom**
	```c#
	public class BankAccount
	{
		public decimal Balance {get;private set;}

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

- Mantenha o setter de Properties publico somente caso ele seja algum tipo de configuração ou opcional

- Assim como variáveis, sempre que criar métodos ou classes, mantenha o nível de acesso o mínimo possível.


[Home](https://github.com/Cappta/best-practices)

[Próximo](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/GIT.md)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Variables.md)
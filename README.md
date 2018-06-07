## Geral

- Ao implementar uma nova classe ou método, pense em SOLID quando aplicável! 
- Chamadas a métodos e variáveis não estáticos em contexto de classe devem sempre utilizar o **this**. Em caso de herança utilize **base**

## Formatação

- O código sempre deve ser escrito em inglês a não ser que seja um acrônimo que impossibilite a tradução e complique o entendimento da regra de negócio

- Sempre formatar abertura de chaves na linha seguinte a menos que o trecho de código dentro das chaves seja relativamente simples, neste caso mantenha toda a sentença na mesma linha (incluindo as chaves)

**Ruim:**
```c#
if (Condition){
	// ...Stuff
   	// ...More than one stuff
}
```

**Bom:**
```c#
if (Condition)
{
	// ...Stuff
   	// ...More than one stuff
}
   
   or
   
if (Condition){ // ...Stuff }
```

- Máximo de colunas 120, porém, este limite pode ser extrapolado caso a quebra de linha prejudique o entendimento do trecho de código.

- Sempre utilizar **{}** nos ifs mesmo que tenha somente uma linha, isso serve para evitar que por engano alguém inclua código sem reparar que as chaves não existam.
 
**Ruim:**
```c#
if(word.IsNullOrEmpty() == true ) DoNothing();
```
**Bom:**
```c#
if(word.IsNullOrEmpty() == true ) { DoNothing(); }
```

- Nunca utilizar **!** e sim **== false**, pois é muito mais fácil um caractere magro no início da sentença passar batido do que a segunda opção.

#### Inverter a condição
  Sempre que possível tentar inverter a condição para reduzir ao máximo a quantidade de tabulações e facilitar a leitura.

**Ruim:**
```c#
if (string.IsNullOrWhiteSpace(someTextInput) == false)
{
  this.someService.Execute(someTextInput)
  this.fallbackSomeService.Execute(someTextInput);
  //...
}

throw new ArgumentNullException("Input is empty");
```

**Bom:**
```c#
if (string.IsNullOrWhiteSpace(someTextInput)) { throw new ArgumentNullException("Input is empty"); }

this.someService.Execute(someTextInput)
this.fallbackSomeService.Execute(someTextInput);
//...
``` 

- Ordene os métodos na ordem em que eles são lidos verticalmente

- Ordene suas classes da seguinte maneira:

```c#
class Example
{
	private const int CONST_VARIABLE_EXAMPLE = 0;   // 1° - Variáveis const

	private static readonly string STATIC_READONLY_VARIABLE_EXAMPLE = "Example";	// 2° - Variaveis static readonly

	private static int staticVariableExample = 0; // 3° - Variaveis static

	private string commomVariableExample = "Example";	// 4° Variaveis comuns

	public Example()	// 5° - Construtores
	{
				
	}

	public string PropertieExample { get; set; }	// 6° - Propriedades

	public void EventExemple(object sender, Args e)	// 7° - Eventos
	{

	}

	public void MethodExample()	// 8° Métodos
	{
			//Stuff...
	}
}
```

## Solution

**Definição de nomes de projetos:**
> Nome da empresa, nome do produto e por último o nome do módulo

- Para solution `<Empresa>.<Produto>` - Exemplo Cappta.Gp

- Para projetos `<Empresa>.<Produto>.<Módulo>` - Exemplo Cappta.Gp.TefEngine

- Class libraries, se possível, devem ser criadas como .NET Standard Class Libraries, pois assim garantimos a compatibilidade com ambos .NET Framework e .NET Core, o que aumenta a sua portabilidade entre sistemas operacionais.

## Classes

- Pascal Case: **CustomerRepository**

- Nomes devem representar a Entidade em questão

- Mantenha tudo o menos acessível possível somente aumente o acesso a classe quando necessário.
	https://www.codingblocks.net/podcast/episode-23-back-to-basics-encapsulation-for-object-oriented-programming/


- 

- Prefira utilizar o construtor para realizar a inicialização de propriedades obrigatórias.

- Utilize object initializer para configurar propriedades opcionais ou de configuração.

**Ruim:**
```c#
var transaction = new Transaction();
transaction.Amount = 1000;
transaction.Type = "Credit";
```

**Bom:**
```c#
var transaction = new Transaction
{
    Amount = 1000,
    Type = "Credit"
};
```

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

## Variáveis

- Camel Case (paymentTransaction)

- Variáveis `private` em contexto de classe não devem ser escritas com _ (underscore).

- Variáveis `private` em contexto de classe devem sempre que possível ser definidas como readonly.

##### Utilize as keywords
  Para tipos primitivos sempre utilize as keywords e nunca utilize suas classes.

**Ruim:**
```c#
using System;
//...
public AddBook(String title, Decimal price, Int32 releaseYear);
```

**Bom:**
```c#
public AddBook(string title, decimal price, int releaseYear);
```

- Utilize a keyword **var** para definir a declaração de variaveis locais

**Ruim:**

```c#
Object listObjects = new List<Object>();
```

**Bom:**

```c#
var listObjects = new List<Object>();
```

- Encontre nomes que contextualizem suas variaveis e métodos/classes

**Ruim:**
```c#
public class Utils
{
    public string PaymChanName { get; set; }
    public Client People { get; set; }
    
    public void DoOperation(Client Merchant, string PaymentChannel, double ProductValue)
    {
        this.People = Merchant;
        this.PaymChanName = PaymentChannel;
        
        SalesRepository.Make(this.People, this.PaymChanName, ProductValue);
    }
}
```

**Bom:**
```c#
public class SalesController
{
    public string PaymentChannel { get; set; }
    public Client Merchant { get; set; }
    
    public void MakeASale(Client Merchant, string PaymentChannel, double ProductValue)
    {
        this.Merchant = Merchant;
        this.PaymentChannel = PaymentChannel;
        
        SalesRepository.Make(this.Merchant, this.PaymentChannel, ProductValue);
    }
}
```

- Magic numbers ou Strings utilizadas em algoritmos devem ser sempre definidos como constantes dentro da classe para facilitar o entendimento.

- Strings quando de mensagens para o usuário (seja final ou programador) devem ser utilizadas a partir um arquivo de *.resx dentro do projeto que a contém, além do fato disso garantir o reaproveitamento facilita no entendimento do código e desacopla detalhes de implementação de UI.

- Sempre utiliza-las em conjunto com **this** caso estejam em contexto de classe, em caso de herança utilize **base**

- **Constantes** e variáveis **static readonly** devem ser definidas em uppercase separando as palavras com **_** (underscore).

## Níveis de acesso

- Sempre diminuir o máximo possível o acesso

- Variaveis em contexto de classe sempre serão private

- Caso tenha necessidade de abrir o escopo de uma variável a contexto de classe converte-la em uma Property
	
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

<<<<<<< HEAD
- Sempre que criar Properties, reduza ao máximo o acesso de seu setter caso ele seja importante para o funcionamento da classe. Mantenha o setter de Properties publico somente caso ele seja algum tipo de configuração ou seja opcional.
=======
- Sempre que criar Properties reduza ao máximo o acesso de seu setter caso ela seja vital para o funcionamento da classe

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
>>>>>>> Add code examples and references from tasks cj2~cj5

- Assim como variáveis, sempre que criar métodos ou classes, mantenha o nível de acesso o mínimo possível.

## GIT

- Caso esteja implementando uma feature crie uma branch isolada para ela a partir da branch de desenvolvimento

- Branches para tickets de features devem sempre ser criados abaixo da feature correspondente

- Branches de bug devem sempre ser criados abaixo da branch de desenvolvimento

- Utilize a seguinte notação para criar branches de ticket `pivotal_<id>_<owner>` 

- Ao realizar um commit relacionado a um ticket inicie seu comentário com `[#<id_ticket>]`

- Treine o habito de criar commits regulares para evitar conflitos monstruosos no git

## Comentários

- Caso seu código necessite de muitos comentários para ser compreendido, precisa ser refatorado

- Somente utilize comentários quando houver a necessidade de definir o motivo de algo fora de contexto, antes tente refatorar o código ou conversas com alguém para simplificar a solução

- Caso encontre algo esquisito no código que necessite de refatoração ou algo temporário, crie um ticket na plataforma de gerenciamento de projetos e inclua um comentário no código especificando o motivo e destacando o ID para facilitar a referência.

- Nunca utilizar comentários obvios como "Caterpie Pokemon do tipo inseto"

## Testes

- Sempre execute seus testes

- Um Assert por método

- Framework atual MsTest

- Frameworks atuais de Mock Nsubstitute e AutoFixture para gerar valores aleatórios

- Evitar detalhes de implementação nos testes

- Criar o hábito de sempre executar os testes

- Em caso de TDD, utilize o conceito RGR (Red Green Refactor)

- Sempre rodar testes unitários

- Montar os testes no padrão AAA (Arrange Act Assert)

- Priorize os testes importantes para a regra de negócio

- Utilize a nomeclatura `When_<cenario>_given_that_<contexto>_should_<validacao>`

- Já te falei para executar os testes?


## Exceptions

#### Evite rethrow
Evitar ao máximo o uso de _rethrow_ de uma _Exception_, pois isto faz com que esta perca seu antigo _callstack_, ocultando o problema que originou a exceção.

**Ruim:**
```c#
try 
{
  // Do stuff that might throw an exception
}
catch (Exception e) {
  throw e; // This destroys the strack trace information!
}
```

**Bom:**
```c#
try 
{
  // code that may throw exceptions    
}
catch(Exception ex) 
{
  // add error logging here
  throw; // This preserves the stack trace
}
```

[Referência](https://stackoverflow.com/questions/881473/why-catch-and-rethrow-an-exception-in-c)

Sempre que possível realizar o tratamento de Exceptions especificas. Evitando algo como: 

```c#
try 
{
  // Do stuff that might throw an exception
} catch(Exception) {}
```

#### Exceptions customizadas
- Sempre crie _exceptions_ customizadas para contextualizar os erros de seu sistema;
- Utilize uma _exception_ base para seu sistema, assim você pode separar as _exceptions_ de seu sistema e _exceptions_ inesperadas;
- Utilize um código de erro para identificar cada uma de suas _exceptions_. Isso faz com que a identificação de cada erro seja muito mais simples para o usuário de seu código.

Abaixo você pode encontrar alguns exemplos de boas _exceptions_ e algumas não tão boas assim.

**Ruim**
```csharp
public class InvalidUserException : Exception
{
	public InvalidUserException(string message) : base(message)
	{
	}
}
```

**Boa**
```csharp
public enum ErrorCode
{
	UserNotFound = 1,
	InvalidCnpj = 2
}

public abstract class BaseException : Exception
{
	public BaseException(ErrorCode errorCode) : base(GetMessage(errorCode))
	{
		this.ErrorCode = errorCode;
	}

	public ErrorCode ErrorCode { get; }

	private static string GetMessage(ErrorCode errorCode)
	{
		// Return message for the exception based on the error code
		// Gets the message from a resource file
		return ErrorMessages.ResourceManager.GetString(errorCode.ToString());
	}
}

public class InvalidCnpjException : BaseException
{
	public InvalidCnpjException() : base(ErrorCode.InvalidCnpj)
	{
	}
}
```

#### Tratamento de exceções
É muito importante que seu software seja capaz de apresentar _feedbacks_ para os erros causados pelas ações de seu usuário. Uma forma de fazer isto é utilizando exceções para informá-lo de erros de entrada ou fluxo da aplicação. Porém, sua aplicação também deve ser capaz de se recuperar de erros não mapeados. Por este motivo, é muito importante que seu tratamento de exceções seja:

1. Centralizado;
2. Enxuto;
3. Capaz de separar erros mapeados pela sua aplicação de erros não mapeados;
4. Capaz de armazenar detalhes sobre erros não mapeados que ocorrerem na execução da aplicação;

Abaixo pode-se ver um exemplo de um bom tratamento de exceções e de um tratamento não tão bom:

**Ruim**
```csharp
try
{
	// Do some action
}
catch (Exception ex)
{
	ShowDialog(ex.Message);
}
```

**Aceitável, porém com muita repetição**
```csharp
try
{
	// Do some action
}
catch (InvalidUserException ex)
{
	ShowDialog(101, ex.Message);
}
catch (InvalidActionException ex)
{
	ShowDialog(102, ex.Message);
}
catch (UserNotFoundException ex)
{
	ShowDialog(299, ex.Message);
}
catch (Exception ex)
{
	// Log exception
	this.logger.Log(ex);
	ShowDialog(500, "Unexpected error happened");
}
```

**Bom**
```csharp
try
{
	// Do some action
}
catch (BaseException ex)
{
	ShowDialog(ex.ErrorCode, ex.Message);
}
catch (Exception ex)
{
	this.logger.Log(ex);
	ShowDialog(ErrorCode.UnknownError, "Unexpected error happened");
}
```

## Geral

- Ao implementar uma nova classe ou método, pense em SOLID quando aplicavel! 
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

- Máximo de colunas **120** a menos que a quebra de linha prejudique o entendimento do trecho de código.

- Sempre utilizar **{}** nos ifs mesmo que tenha somente uma linha, isso serve para evitar que por engano alguém inclua código sem reparar que as chaves não existam.

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

	private static int STATIC_VARIABLE_EXAMPLE = 0; // 3° - Variaveis static

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

- Class libraries devem sempre ser criadas como .NET Standard Class Libraries, pois assim garantimos a compatibilidade entre SO. A menos que seja uma implementação específica.​

## Classes

- Pascal Case: **CustomerRepository**

- Nomes devem representar a Entidade em questão

- Mantenha tudo o menos acessível possível somente aumente o acesso a classe quando necessário.

- 

- Prefira utilizar o construtor para realizar a inicialização de propriedades obrigatórias.

- Utilize object initializer para configurar propriedades opcionais ou de configuração.

## Métodos
> As regras abaixo são validas para todos os níveis de acesso (private, protected, internal e public). 

- Pascal Case: **DoItNow**

- Nomes devem representar a ação que está sendo executada.

- Tente quebrar o comportamento do método de maneira que o fluxo do algoritmo não fique muito grande e seja lido simplesmente pelo fluxo de seus métodos. Ao separar o comportamento de um método em blocos para facilitar a leitura considere refatorar o comportamento para outro método private que seja responsável pela ação e dê a ele um nome significativo.

- Ao utilizar coleções em retornos ou parâmetros sempre defina-os como **IEnumerable**

- Sempre valide seus parâmetros de métodos publicos para evitar side effects em lugares indesejados

## Variáveis

- Camel Case (paymentTransaction)

- Variáveis private em contexto de classe não devem ser escritas com _ (underscore).

- Variáveis private em contexto de classe devem sempre que possível ser definidas como readonly.

##### Utilize as keywords
  Para tipos primitivos sempre utilize as keywords e nunca utilize suas classes

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

- Encontre nomes que contextualizem suas variaveis

- Magic numbers ou Strings utilizadas em algoritmos devem ser sempre definidos como constantes dentro da classe para facilitar o entendimento.

- Strings quando de mensagens para o usuário (seja final ou programador) devem ser utilizadas a partir um arquivo de *.resx dentro do projeto que a contém, além do fato disso garantir o reaproveitamento facilita no entendimento do código e desacopla detalhes de implementação de UI.

- Sempre utiliza-las em conjunto com **this** caso estejam em contexto de classe, em caso de herança utilize **base**

- **Constantes** e variáveis **static readonly** devem ser definidas em uppercase separando as palavras com **_** (underscore).

## Níveis de acesso

- Sempre diminuir o máximo possível o acesso

- Variaveis em contexto de classe sempre serão private

- Caso tenha necessidade de abrir o escopo de uma variável a contexto de classe converte-la em uma Property

- Sempre que criar Properties reduza ao máximo o acesso de seu setter caso ela seja vital para o funcionamento da class. Mantenha o setter de Properties publico somente caso ele seja algum tipo de configuração ou opcional

- Assim como variáveis sempre que criar métodos ou classes, reduza seu nível de acesso ao máximo possível e de acordo com a necessidade libere o acesso aos poucos.

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
  Evitar ao máximo o uso de rethrow em Exceptions

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

- Sempre crie exceptions customizadas para contextualizar os erros 

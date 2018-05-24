## Formatação

- O código sempre deve ser escrito em inglês a não ser que seja um acrônimo que impossibilite a tradução e complique o entendimento da regra de negócio

- Sempre formatar abertura de chaves na linha seguinte a menos que o trecho de código dentro das chaves seja relativamente simples, neste caso mantenha toda a sentença na mesma linha (incluindo as chaves)

Wrong:
```
if (Condition){
	// ...Stuff
   	// ...More than one stuff
}
```

Right:
```
if (Condition)
{
	// ...Stuff
   	// ...More than one stuff
}
   
   or
   
if (Condition){ // ...Stuff }
```

- Máximo de colunas **120**

- Sempre utilizar **{}** nos ifs mesmo que tenha somente uma linha, isso serve para evitar que por engano alguém inclua código sem reparar que as chaves não existam.

- Nunca utilizar **!** e sim **== false**, pois é muito mais fácil um caractere magro no início da sentença passar batido do que a segunda opção.

- Sempre que possível tentar inverter a condição para reduzir ao máximo a quantidade de tabulações e facilitar a leitura.

- Ordene os métodos na ordem em que eles são lidos verticalmente

- Ordene suas classes da seguinte maneira:

```
class Example
{
	private const int CONST_VARIABLE_EXAMPLE = 0;   // 1° - Variáveis const

	private static readonly string STATIC_READONLY_VARIABLE_EXAMPLE = "Example";	// 2° - Variaveis static readonly

	private static int STATIC_VARIABLE_EXAMPLE = 0; // 3° - Variaveis static

	private string COMMON_VARIABLE_EXAMPLE = "Example";	// 4° Variaveis comuns

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

- Definição de nomes de projetos:
 - Nome da empresa
 - Nome do produto
 - Nome do módulo

- Para solution `<Empresa>.<Produto>` - Exemplo Cappta.Gp

- Para projetos `<Empresa>.<Produto>.<Módulo>` - Exemplo Cappta.Gp.TefEngine
 - Class libraries devem sempre ser criadas como Portable Class Libraries, pois assim garantimos a compatibilidade entre SO. A menos que seja uma implementação específica.​

## Classes

- Pascal Case: **CustomerRepository**

- Nomes devem representar a Entidade em questão

- Mantenha tudo o menos acessível possível somente aumente o acesso a classe quando necessário.

- Ao implementar uma nova classe pense em SOLID quando aplicavel 

- Prefira utilizar o construtor para realizar a inicialização de propriedades obrigatórias.

- Utilize object initializer para configurar propriedades opcionais ou de configuração.

## Métodos

- As regras abaixo são validas para todos os níveis de acesso (private, protected, internal e public).

- Pascal Case: **DoItNow**

- Nomes devem representar a ação que está sendo executada.

- Tente quebrar o comportamento do método de maneira que o fluxo do algoritmo não fique muito grande e seja lido simplesmente pelo fluxo de seus métodos.

- Ao separar o comportamento de um método em blocos para facilitar a leitura considere refatorar o comportamento para outro método private que seja responsável pela ação e dê a ele um nome significativo (após a alteração analise se a leitura não ficou melhor).

- Chamadas a métodos não estáticos em contexto de classe devem sempre utilizar o **this**, em caso de herança utilize **base**

- Ao utilizar coleções em retornos ou parâmetros sempre defina-os como **IEnumerable**

- Sempre valide seus parâmetros de métodos publicos para evitar side effects em lugares indesejados

## Variáveis

- Camel Case (paymentTransaction)

- Variáveis private em contexto de classe não devem ser escritas com _ (underscore)

- Variáveis private em contexto de classe devem sempre que possível ser definidas como readonly.

- Para tipos primitivos sempre utilize as keywords e nunca utilize suas classes

- Utilize a keyword **var** para definir a declaração de variaveis locais

Wrong:

```
Object listObjects = new List<Object>();
```

Right:

```
var listObjects = new List<Object>();
```

- Encontre nomes que contextualizem suas variaveis

- Magic numbers ou Strings utilizadas em algoritmos devem ser sempre definidos como constantes dentro da classe para facilitar o entendimento.

- Strings quando de mensagens para o usuário (seja final ou programador) devem ser utilizadas a partir um arquivo de *.resx dentro do projeto que a contém, além do fato disso garantir o reaproveitamento facilita no entendimento do código e desacopla detalhes de implementação de UI.

- Sempre utiliza-las em conjunto com **this** caso estejam em contexto de classe, em caso de herança utilize **base**

- Constantes devem ser definidas em uppercase separando as palavras com **_**

- Variaveis **static readonly** devem utilizar a mesma regra de constantes para serem nomeadas

## Níveis de acesso

- Sempre diminuir o máximo possível o acesso

- Variaveis em contexto de classe sempre serão private

- Caso tenha necessidade de abrir o escopo de uma variável a contexto de classe converte-la em uma Property

- Sempre que criar Properties reduza ao máximo o acesso de seu setter caso ela seja vital para o funcionamento da classe

- Mantenha o setter de Properties publico somente caso ele seja algum tipo de configuração ou opcional

- Assim como variáveis sempre que criar métodos reduza seu nível de acesso ao máximo possível e de acordo com a necessidade libere o acesso aos poucos.

- O mesmo vale para as classes

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

- Sempre crie testes para evitar o efeito Bug Jason

- Foque somente nos testes importantes para a regra de negócio

- Utilize a nomeclatura `When_<cenario>_given_that_<contexto>_should_<validacao>`

- Já te falei para executar os testes?


## Exceptions

- Evitar ao máximo o uso de rethrow em Exceptions

- A não ser que tenha um bom motivo sempre que possível realizar o tratamento de Exceptions especificas evitando algo como try {} catch(Exception) {}

- Sempre crie exceptions customizadas para contextualizar os erros 

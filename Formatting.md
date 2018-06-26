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

- Linhas de código devem seguir, preferencialmente, o limite de 120 colunas. Contudo, este limite pode ser extendido para 160 caso o entendimento do código fique prejudicado com a quebra da linha.

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
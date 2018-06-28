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


[Home](https://github.com/Cappta/best-practices)

[Próximo](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/AccessLevels.md)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Methods.md)
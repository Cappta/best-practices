## Classes

- Pascal Case: **CustomerRepository**

- Nomes devem representar a Entidade em questão

- Mantenha tudo o menos acessível possível somente aumente o acesso a classe quando necessário.
	https://www.codingblocks.net/podcast/episode-23-back-to-basics-encapsulation-for-object-oriented-programming/

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
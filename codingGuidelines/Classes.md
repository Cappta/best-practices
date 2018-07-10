## Classes

- Pascal Case: **CustomerRepository**

- Nomes devem representar a Entidade em questão

- Mantenha tudo o menos acessível possível somente aumente o acesso a classe quando necessário.
	https://www.codingblocks.net/podcast/episode-23-back-to-basics-encapsulation-for-object-oriented-programming/

- Prefira utilizar o construtor para realizar a inicialização de propriedades obrigatórias.

- Utilize _object initializer_ para configurar propriedades opcionais ou de configuração quando possível.
    - Quando utilizamos o _object initializer_, se uma exceção é lançada em alguma linha de inicialização, esta exceção será indicada na primeira linha da declaração do _object initializer_, não na linha que realmente lançou a exceção. Portanto, para objetos complexos e que podem lançar exceções, é preferível que você não faça o uso deste recurso.

**Ruim:**
```csharp
var transaction = new Transaction();
transaction.Amount = 1000;
transaction.Type = "Credit";
```

**Bom:**
```csharp
var transaction = new Transaction
{
    Amount = 1000,
    Type = "Credit"
};
```

[Home](https://github.com/Cappta/best-practices)

[Próximo](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Methods.md)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Solution.md)
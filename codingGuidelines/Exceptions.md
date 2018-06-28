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


[Home](https://github.com/Cappta/best-practices)

[Anterior](https://github.com/Cappta/best-practices/blob/master/codingGuidelines/Tests.md)
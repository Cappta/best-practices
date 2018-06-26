## Solution

**Definição de nomes de projetos:**
> Nome da empresa, nome do produto e por último o nome do módulo

- Para solution `<Empresa>.<Produto>` - Exemplo Cappta.Gp

- Para projetos `<Empresa>.<Produto>.<Módulo>` - Exemplo Cappta.Gp.TefEngine

- Para produtos _whitelabel_ o nome da empresa deve ser ocultado - `<Produto>.<Módulo>` - Exemplo: Scrooge | Scrooge.Core

- Class libraries, se possível, devem ser criadas como .NET Standard Class Libraries, pois assim garantimos a compatibilidade com ambos .NET Framework e .NET Core, o que aumenta a sua portabilidade entre sistemas operacionais.
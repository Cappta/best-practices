# Guia de Arquitetura

Desenvolvedores são responsáveis por criar as ferramentas que compõem negócios e transformam o mundo. Na Cappta não é diferente: trabalhamos duro para criar soluções que facilitem a vida do empreendedor no varejo brasileiro, e essa missão não é nada fácil! 

Você já ouviu algo parecido: especificações e necessidades mudam a todo momento e os sistemas que desenvolvemos precisam ser capazes de acompanhar essas transformações nos negócios, mas como fazer isso? Como "desenhar" um sistema para que ele seja saúdavel, extensível e que não seja um pesadelo para a galera que vai fazer a sustentação dele?

Arquitetura e design de software são um temas controversos na comunidade, onde especialistas debatem constantemente sobre qual o melhor modelo. Mas será que existe um padrão de arquitetura melhor que os demais? A resposta para essa pergunta é a mesma para outras diversas perguntas em tecnologia: DEPENDE do que você quer construir. Dessa forma, a proposta deste texto não é te dizer "a melhor arquitetura", mas trazer conceitos e princípios que auxiliem a criação de bons softwares. :)

## SOLID

Se você está escrevendo software na Cappta, a chance é que você está usando alguma linguagem de programação orientada a objetos. Provavelmente você está usando .NET, ou escrevendo algum módulo em JavaScript para uma API em Node ou uma pagína em Angular, talvez seu time esteja pensando em usar Python, ou Java (bleh()). Não importa, SOLID se ajusta a todas elas.

SOLID não são padrões de projetos ou modelos de arquitetura mais sim princípios de *design* que guiam o desenvolvedor\arquiteto de software a escrever e pensar em módulos de alta coesão e baixo acoplamento, diminuindo o custo de manunteção e extensão.

(A também quem diga que SOLID vale para [paradigma funcional](http://blog.ploeh.dk/2014/03/10/solid-the-next-step-is-functional/))

### O que é SOLID ?

**O termo SOLID é um acrônimo para 5 princípios de design e programação orientada a objetos** identificados por Robert C. Martin (Uncle Bob) por volta dos anos 2000. É importante destacar a palavra **princípios** para não confundirmos SOLID com *design patterns*, que são soluções reutilizáveis para problemas de programação recorrentes que podem e são utilizados para atingir os principios de SOLID.

### Os princípios
Os princípios do SOLID são:

**S**ingle Responsability Principle
    - entidades de software devem ter apenas uma responsabilidade (deve fazer apenas uma coisa) ou uma classe deve ter um, e somente um, motivo para mudar;

**O**pen/Closed Principle
    - uma classe deve ser aberta para extensão mas fechada para modificação, ou seja, introdução de novos comportamentos\funcionalidades não deve quebrar código existente;

**L**iskov Substituiton Principle
    - entidades de software (classes) devem ser substítuiveis por instâncias derivadas (sub-classes) sem afetar a exatidão do programa;

**I**nterface Segregation Princicple
    - segregar comportamentos em diversas interfaces é melhor do que ter uma interface de proposito geral;

**D**ependency Inversion Principle
    - módulos de alto nível não devem depender de módulos de baixo nível, ou seja, abstrações não devem depender de detalhes, detalhes devem depender de abstrações.

Links para aprender sobre o assunto:

- curso da Alura de [SOLID com C#](https://cursos.alura.com.br/course/orientacao-a-objetos-avancada-e-principios-solid-csharp);
- [palestra do Uncle Bob](https://www.youtube.com/watch?v=t86v3N4OshQ) sobre o tema;

## Database Centric Architecture

### O que é?
Neste modelo de arquitetura, **todas as dependências do software apontam para o banco de dados**. Este padrão faz uso em larga escala de stored-procedures, triggers e views (SQL) para processamento de regras de negócio que rodam no servidor de banco de dados ao invés de lógica em aplicações construídas com linguagem de alto-nível (C#, Java, etc.). O sistema tem alto grau de acoplamento com a modelagem do banco de dados, geralmente feita antes e representando o núcleo do projeto.

Para o padrão *database centric* os dados e os objetos de BD são os componentes mais valiosos do sistema, e o banco de dados é geralmente utilizado por diversas aplicações - é dessa forma atingem reusabilidade de código (stored procedures e funções SQL no banco de dados).

Este modelo de arquitetura juntamente com a metodologia de desenvolvimento em cascata, são os padrões mais difundido nos cursos de computação pelo mundo afora e, apesar de serem independentes, esse "pacote" é apresentado através do conhecido padrão de **arquitetura em 3 camadas**, onde temos uma camada de Apresentação (camada de UI), uma camada de aplicação (camada contendo as regras de negócio) e uma camada de acesso a dados (lógica de acesso a dados e conexão com banco de dados).

### Conclusão

O modelo *database centric* é um modelo simples de arquitetura, que juntamente com o padrão de 3 camadas pode ser utilizado na construção de aplicações simples (CRUD - tela\banco) ou na prototipagem de sistemas mais complexos (construção de POCs).

## Domain-Centric Architecture

Neste padrão de arquitetura, todas as dependências do sistema apontam para a camada de **domínio** (*DomainModel*, *Domain*, etc.), residente em softrware midleware geralmente escrito em linguagem de programação de alto nível (Java, C#, Python, etc). 

Nesta camada as entidades e casos de uso do projeto (regras de negócio) residem isoladas do restante,permitindo extensa cobertura de teste do domínio livre de dependências das demais camadas do projeto, de outros sistemas e de infraestrutura (APIs, BDs, etc.).

Neste padrão de arquitetura, o domínio é o ativo mais valioso de todo o sistema, e constitue o núcleo da aplicação. O restante como camadas de apresentação e persistência são considerados detalhes de implementação e ficam entorno do domínio. Este conceito pode ser expresso através da máxima de Uncle Bob : "A primeira preocupação da arquitetura é ter certeza que a casa é utilizável, não é para garantir que a casa é feita de tijolos".

A implementação deste tipo de arquitetura é mais custosa que outros pois demanda o aprendizado de diversas técnicas e padrões (DDD, BDD, design patterns, frameworks de teste, etc.) tornando a curva de aprendizado de sua implementação mais acentuada que em outros modelos, portanto este tipo de arquitetura é utilizado para modelar e resolver problemas de domínios complexos.

Existem muitas implementações de arquiteturas *Domain Centric*, entre elas a _Hexagonal_, a _Onion_ e a _Clean Architecture_, _Microservices_. Procure a que melhor atenda a necessidade de seu negócio.

### Conclusão

A arquitetura orientada a domínio, é melhor utilizada em projetos com domínios complexos, aonde existam a representação de fluxos e processos que envolvem diversos setores, atores e sistemas. O mau uso desta arquitetura pode tornar um projeto simples, em algo desnecessariamente complexo.

Para aprender mais: 

[Clean Arquitecture - Patterns, Practices and Principles](https://www.pluralsight.com/courses/clean-architecture-patterns-practices-principles)

[SOLID](https://en.wikipedia.org/wiki/SOLID)

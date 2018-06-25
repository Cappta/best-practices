# Guia de Arquitetura

Desenvolvedores são responsáveis por criar as ferramentas que compõem negócios e transformam o mundo. Na Cappta não é diferente: trabalhamos duro para criar soluções que facilitem a vida do empreendedor no varejo brasileiro, e essa missão não é nada fácil! 

Você já ouviu algo parecido: especificações e necessidades mudam a todo momento e os sitemas que desenvolvemos precisam ser capazes de acompanhar essas transformações nos negócios. Mas, como fazer isso? Como "desenhar" um sistema para que ele seja saúdavel, extensível e que não seja um pesadelo para a galera que vai fazer a sustentação dele?

Arquitetura e design de software é um tema controverso na comunidade, onde especialistas debatem sobre qual o melhor modelo. Mas será que existe um padrão de arquitetura melhor que os demais? A resposta para essa pergunta é a mesma para outras diversas perguntas em tecnologia: DEPENDE do que você está querendo construir. Dessa forma, a proposta deste texto não é te dizer "a melhor" arquitetura, mas sim trazer conceitos e principios de design que te auxiliem no processo de desenvolvimento para atingir esse objetivo.

## SOLID

Se você está escrevendo software na Cappta, chance é que você está usando alguma linguagem de programação orientada a objetos. Provavelemente, você está usando .NET, ou escrevendo algum módulo em JavaScript para uma API em Node ou uma pagína em Angular, talvez seu time esteja pensando em usar Python, ou Java (bleh()). Não importa, SOLID se ajusta a todas elas.

SOLID não são padrões de projetos ou modelos de arquitetura mais sim princípios de *design* que guiam o desenvolvedor\arquiteto de software a escrever e pensar em módulos de alta coesãos e baixo acoplamento, diminuir o custo e de manunteção e extensão.

(A também quem diga que SOLID vale para [paradigma funcional](http://blog.ploeh.dk/2014/03/10/solid-the-next-step-is-functional/))

### O que é SOLID ?

**O termo SOLID é um acrônimo para 5 princípios de design e programação orientada a objetos** identificados por Robert C. Martin (Uncle Bob) por volta dos anos 2000. É importante destacar a palavra **princípios** para não confundirmos SOLID com *design patterns* que são soluções reutilizáveis para problemas de programação recorrentes que podem e são utilizados para atingir os principios de SOLID.

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

Para o padrão *database centric* os dados e os objetos de BD são os componentes mais valiosos do sistema, e o banco de dados é geralmente utilizado por diversas aplicações - é dessa forma atingem que atigem reusabilidade de código (stored procedures e funções SQL no banco de dados).

Este modelo de arquitetura juntamente com a metodologia de desenvolvimento em cascata, são os padrões mais difundido nos cursos de computação pelo mundo afora e, apesar de serem independentes, esse "pacote" é apresentado através do conhecido padrão de **arquitetura em 3 camadas**, onde temos uma camada de Apresentação (camada de UI), uma camada de aplicação (camada contendo as regras de negócio) e uma camada de acesso a dados (lógica de acesso a dados e conexão com banco de dados).
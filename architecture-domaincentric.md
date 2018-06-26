Este guia foi baseado no curso [Clean Arquitecture - Patterns, Practices and Principles](https://www.pluralsight.com/courses/clean-architecture-patterns-practices-principles) e com a contribuição de outros desenvolvedores da companhia.

### Domain-Centric Architecture


Neste padrão de arquitetura, todas as dependências do sistema apontam para a camada de **domínio** (*DomainModel*, *Domain*, etc.), residente em softrware midleware geralmente escrito em linguagem de programação de alto nível (Java, C#, Python, etc). 

Nesta camada as entidades e casos de uso do projeto (regras de negócio) residem isoladas do restante,permitindo extensa cobertura de teste do domínio livre de dependencias das demais camadas do projeto, outros sistemas e de infraestrutura (APIs, BDs, etc.)

Neste padrão de arquitetura, o domínio é o ativo mais valioso de todo o sistema, e constitue o núcleo da aplicação. O restante como camadas de apresentação e persistência são considerados detalhes de implementação e ficam entorno do domínio. Este conceito pode ser expresso através da máxima de Uncle Bob : "A primeira preocupação da arquitetura é ter certeza que a casa é utilizável, não é para garantir que a casa é feita de tijolos".

A implementação deste tipo de arquitetura é mais custosa que outros pois demanda o aprendizado de diversas técnicas e padrões (DDD, BDD, design patterns, frameworks de teste, etc.) tornando a curva de aprendizado de sua implementação mais acentuada que em outros modelos, portanto este tipo de arquitetura é utilizado para modelar e resolver problemas de domínios complexos.



### Conclusão

A arquitetura orientada a domínio, é melhor utilizada em projetos com domínios complexos, aonde existam a representação de fluxos e processos que envolvem diversos setores, atores e sistemas, e o mau uso desta arquitetura pode tornar um projeto simples, em algo desnecessariamente complexo.

Existem muitas implementações de arquiteturas *Domain Centric*, entre elas a _Hexagonal_, a _Onion_ e a _Clean Architecture_, _Microservices_. Procure a que melhor atenda a necessidade de seu negócio.

Para aprender mais: 
[Clean Arquitecture - Patterns, Practices and Principles](https://www.pluralsight.com/courses/clean-architecture-patterns-practices-principles)
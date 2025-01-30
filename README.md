# DSLista - Intensivo Java Spring

Este projeto foi desenvolvido durante o **Intensivão Java Spring**, apresentado pelo professor Nélio Alves, um curso focado em ensinar o desenvolvimento de aplicações web utilizando o framework Spring Boot.
O DSLista é uma aplicação que gerencia listas de jogos, permitindo a consulta de jogos, listas e a movimentação de jogos entre listas. A DSLista foi desenvolvida utilizando a linguagem Java, o framework Spring Boost
e seguindo o padrão em camadas que abrange entidades/ORM, DTOs e API REST.

## Funcionalidades

- **Listagem de Jogos**: Exibe todos os jogos cadastrados no sistema.
- **Detalhes do Jogo**: Mostra informações detalhadas sobre um jogo específico.
- **Listas de Jogos**: Exibe listas de jogos e permite a movimentação de jogos entre listas.
- **CORS Configurado**: A aplicação permite requisições de origens específicas, configuradas via propriedades.

## Tecnologias Utilizadas

- **Spring Boot**: Framework principal para desenvolvimento da aplicação.
- **Spring Data JPA**: Para persistência de dados e acesso ao banco de dados.
- **PostgreSQL**: Banco de dados principal para ambiente de produção.
- **H2 Database**: Banco de dados em memória para testes.
- **Maven**: Gerenciador de dependências e build do projeto.
- **Java 17**: Versão do Java utilizada no projeto.

## Configuração do Ambiente

### Pré-requisitos

- **Java 17**: Certifique-se de ter o JDK 17 instalado.
- **Maven**: Instale o Maven para gerenciar as dependências e build do projeto.
- **PostgreSQL**: Para ambiente de produção, é necessário ter o PostgreSQL instalado e configurado.

### Configuração do Banco de Dados

1. **Ambiente de Teste**:
   - O banco de dados H2 é utilizado por padrão. Para acessar o console do H2, acesse `http://localhost:8080/h2-console`.
   - As credenciais padrão são:
     - URL: `jdbc:h2:mem:testdb`
     - Usuário: `sa`
     - Senha: (vazio)

2. **Ambiente de Desenvolvimento**
  - Para este ambiente precisaremos do PostgreSQL e o pgAdmin instalados e configurados.
  - Tire os comentários do trecho presente no `application-dev.properties` para criação das tabelas em SQL (lembre-se de comentar novamente após a criação delas):
    ```properties
    #spring.jpa.properties.jakarta.persistence.schema-generation.create-source=metadata
    #spring.jpa.properties.jakarta.persistence.schema-generation.scripts.action=create
    #spring.jpa.properties.jakarta.persistence.schema-generation.scripts.create-target=create.sql
    #spring.jpa.properties.hibernate.hbm2ddl.delimiter=;
    ```
  - No arquivo `application.properties` mude o trecho abaixo:
    ```properties
    spring.profiles.active=${APP_PROFILE:test}
    ```
    Para:
    ```properties
    spring.profiles.active=${APP_PROFILE:dev}
    ```
    Assim a aplicação rodará no ambiente de desenvolvimento.
   
2. **Ambiente de Produção**:
   - Configure o arquivo `application-prod.properties` com as credenciais do seu banco PostgreSQL.
   - Exemplo:
     ```properties
     spring.datasource.url=jdbc:postgresql://localhost:5433/dslist
     spring.datasource.username=postgres
     spring.datasource.password=1234567
     ```
   - No arquivo `application.properties` mude o trecho abaixo:
      ```properties
      spring.profiles.active=${APP_PROFILE:test}
      ```
      Para:
      ```properties
      spring.profiles.active=${APP_PROFILE:prod}
      ```
      Assim a aplicação rodará no ambiente de produção.

### Configuração do CORS

- O CORS está configurado para permitir requisições de origens específicas. As origens permitidas podem ser configuradas no arquivo `application.properties`:
  ```properties
  cors.origins=http://localhost:5173,http://localhost:3000

### Executando o Projeto

1. **Clone o repositório**
```bash
git clone https://github.com/seu-usuario/dslista.git
cd dslista
```

2. **Compile o projeto**
```bash
./mvnw clean install
```
3. **Execute a aplicação**
```bash
./mvnw spring-boot:run
```
4. **Acesse a aplicação**
A aplicação estará disponível em `http://localhost:8080`.

### Endpoints da API

- **GET /games**: Retorna a lista de todos os jogos.
- **GET /games/{id}**: Retorna os detalhes de um jogo específico.
- **GET /lists**: Retorna todas as listas de jogos.
- **GET /lists/{listId}/games**: Retorna os jogos de uma lista específica.
- **POST /lists/{listId}/replacement**: Move um jogo de uma posição para outra dentro de uma lista.


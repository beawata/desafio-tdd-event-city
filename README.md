# Desafio TDD: Event-City 🏙️📅

Este repositório contém a resolução de um desafio focado em desenvolvimento guiado por testes (**TDD - Test-Driven Development**). No cenário proposto, a estrutura inicial contava apenas com os testes automatizados integrados e de unidade. O objetivo principal foi implementar e estruturar todas as regras de negócio e endpoints necessários para fazer com que 100% dos testes fossem aprovados.

## 🎯 Competências Avaliadas e Demonstradas

O desenvolvimento deste desafio exigiu o domínio de práticas recomendadas no ecossistema **Java** e **Spring Boot**, com ênfase em:

* **Test-Driven Development (TDD):** Capacidade de ler, interpretar e implementar o código de produção guiado estritamente por testes pré-existentes.
* **Construção de APIs RESTful:** Criação de endpoints robustos seguindo as convenções e as melhores práticas do protocolo HTTP.
* **Arquitetura em Camadas:** Divisão clara e isolada de responsabilidades entre Controladores (`Web/Controller`), Serviços (`Service`) e Acesso a Dados (`Repository`), utilizando **DTOs (Data Transfer Objects)** para o tráfego de dados.
* **Tratamento de Exceções Personalizado:** Captura e tratamento centralizado de erros da aplicação, como recursos não encontrados ou violações de integridade, garantindo respostas limpas e padronizadas.
* **Persistência de Dados e ORM:** Utilização do Spring Data JPA para comunicação com banco de dados relacional e manipulação adequada de entidades e relacionamentos.

---

## 💻 Tecnologias Utilizadas

* **Linguagem:** Java
* **Framework Principal:** Spring Boot (Spring Web, Spring Data JPA)
* **Banco de Dados:** H2 Database (Banco em memória para ambiente de testes/desenvolvimento)
* **Ferramentas de Testes:** JUnit 5, Mockito e MockMvc (para testes de controladores)
* **Gerenciador de Dependências:** Maven

---

## 🛠️ Resolução do Desafio

O domínio da aplicação consiste em um sistema de gerenciamento de **Cidades (`City`)** e **Eventos (`Event`)**, onde um evento obrigatoriamente pertence a uma cidade.

### Regras de Negócio Implementadas

1.  **Cidades (`City`):**
    * `GET /cities`: Retorna todas as cidades cadastradas organizadas em ordem alfabética por nome.
    * `POST /cities`: Realiza a inserção de uma nova cidade no banco de dados.
    * `DELETE /cities/{id}`: Exclui uma cidade existente baseado no ID fornecido. Esta funcionalidade cobre **3 cenários testados**:
        * **Sucesso:** A exclusão é realizada com sucesso caso o ID exista e a cidade não tenha vínculos.
        * **Recurso Não Encontrado:** Lança uma exceção customizada (`ResourceNotFoundException`) caso o ID informado não exista.
        * **Integridade Referencial:** Lança uma exceção de integridade de dados (`DatabaseException`) caso se tente deletar uma cidade que possui eventos vinculados a ela (impedindo a quebra de restrição de chave estrangeira).

2.  **Eventos (`Event`):**
    * `PUT /events/{id}`: Atualiza os dados de um evento existente baseado no ID fornecido. Caso o ID não exista, a aplicação lança de forma segura uma exceção do tipo `ResourceNotFoundException`.

### Estrutura do Projeto

A solução foi estruturada seguindo o padrão de camadas do Spring:

```text
src/main/java/com/devsuperior/bds02
├── controllers
│   ├── CityController.java
│   └── EventController.java
├── services
│   ├── CityService.java
│   └── EventService.java
├── repositories
│   ├── CityRepository.java
│   └── EventRepository.java
├── dto
│   ├── CityDTO.java
│   └── EventDTO.java
└── entities
    ├── City.java
    └── Event.java
```




🚀 Como Executar o Projeto e os Testes
Para clonar e testar a resolução localmente, siga os passos abaixo:

**Pré-requisitos**
*  Java JDK instalado (versão compatível configurada no projeto)
*  Maven

* **Passo a Passo**
  
#### 1. Clonar o repositório:
```
git clone [https://github.com/beawata/desafio-tdd-event-city.git](https://github.com/beawata/desafio-tdd-event-city.git)
```

#### 2. Entrar na pasta do projeto:
```
cd desafio-tdd-event-city
```

#### 3. Executar a suíte de testes automatizados:
```
mvn test
```


* Se preferir rodar a aplicação para interagir com os endpoints (usando ferramentas como Postman ou Insomnia), execute o comando:
```
mvn spring-boot:run
```

Para encerrar a aplicação no terminal, basta utilizar o atalho **Ctrl + C**.

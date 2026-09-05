# Notificações API
API RESTful desenvolvida com Spring Boot para consumir dados de uma fila do RabbitMQ, enviar um e-mail de boas-vindas ao usuário e demonstrar o funcionamento de mensageria entre APIs.

> Projeto de portfólio / estudo pessoal. Credenciais de banco, mensageria e e-mail ficam direto no `application.properties` — isso não é o padrão indicado para produção (o ideal ali é usar variáveis de ambiente).

⚠️ Esta API consome mensagens da fila `pessoas`, que antes era alimentada pelo repositório `apiPessoas` — removido do portfólio. Sem um produtor publicando na fila, ela fica vazia; para testar, publique uma mensagem manualmente pelo painel do RabbitMQ (formato esperado abaixo).

## Tecnologias utilizadas:
 * Java 21
 * Spring Boot
 * Spring Mail
 * Maven
 * JPA / Hibernate
 * Swagger
 * H2 (banco em memória — os logs são perdidos a cada reinício)
 * RabbitMQ

## Funcionalidade:
A API consome da fila `pessoas`, processa o payload recebido (nome e e-mail), envia um e-mail de boas-vindas usando o Spring Mail e registra um log da mensagem processada no banco.

Formato esperado da mensagem na fila:
```json
{
  "nome": "Maria Silva",
  "email": "maria@email.com"
}
```

## Endpoints
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/logs/mensagem` | Consulta os logs das mensagens processadas |

## Como executar o projeto:

### Requisitos
* Java 21+
* Spring Boot 3.4.0+
* Um servidor de mensageria (RabbitMQ local ou CloudAMQP)

#### 1. Clone o repositório
```bash
   git clone https://github.com/samuelmsilva2v/notificacoes-api.git
   cd notificacoes-api
```
#### 2. Instale as dependências e compile o projeto com Maven:
```bash
./mvnw clean install
```
#### 3. Execute a aplicação:
```bash
./mvnw spring-boot:run
```

A aplicação vai rodar em http://localhost:8081/swagger-ui/index.html#

Configure `application.properties` com os dados da sua fila e do seu servidor de e-mail:
```properties
spring.rabbitmq.host=
spring.rabbitmq.port=
spring.rabbitmq.username=
spring.rabbitmq.password=

spring.mail.host=smtp-mail.outlook.com
spring.mail.port=587
spring.mail.username=
spring.mail.password=
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

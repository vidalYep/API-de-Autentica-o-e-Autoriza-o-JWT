# API de Autenticação e Autorização JWT com Spring Boot

## 🚀 Visão Geral

Esta API foi construída com **Spring Boot 3.x** para fornecer autenticação e autorização baseada em **JWT (JSON Web Tokens)**, gerando e validando tokens internamente. É ideal para arquiteturas que demandam segurança robusta, stateless e escalável, protegendo recursos e endpoints de forma eficiente.

A aplicação implementa as melhores práticas de:

- Segurança
- Testabilidade
- Documentação automática (Swagger / OpenAPI)

---

## 📦 Tecnologias e Dependências

- Spring Boot Starter Web (REST API)  
- Spring Boot Starter Security (Autenticação e autorização)  
- Spring Boot Starter OAuth2 Resource Server (Validação JWT)  
- Spring Boot Starter Data JPA (Persistência)  
- Banco de dados H2 em memória (desenvolvimento e testes)  
- Lombok (redução de boilerplate)  
- Springdoc OpenAPI (documentação Swagger)  
- Spring Boot DevTools (hot reload)  
- JUnit 5 e Mockito (testes automatizados)  
- Auth0 Java JWT (geração e validação de tokens)  

---

## ⚙️ Configuração

O arquivo `src/main/resources/application.yml` configura o servidor, banco de dados, JWT e Swagger:

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
    driver-class-name: org.h2.Driver
    username: sa
    password:
  h2:
    console:
      enabled: true
      path: /h2-console
  jpa:
    database-platform: org.hibernate.dialect.H2Dialect
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
  devtools:
    restart:
      enabled: true
    livereload:
      enabled: true

jwt:
  secret: umaChaveSecretaMuitoLongaEComplexaParaAssinarTokensJWT
  expiration: 3600000 # 1 hora em ms

springdoc:
  swagger-ui:
    path: /swagger-ui.html
    disable-swagger-default-url: true
  api-docs:
    path: /v3/api-docs
```

## 🔑 Funcionalidades Principais

### Autenticação

- Login via endpoint `/auth/login`  
- Recebe username e password  
- Retorna token JWT assinado se credenciais estiverem corretas  

### Validação de Token

- Endpoint `/auth/validate` para validar tokens JWT existentes  
- Retorna sucesso ou erro conforme validade e expiração  

### Proteção de Endpoints

- Configuração Spring Security para proteger endpoints  
- Stateless: sem sessões, apenas validação via JWT  
- Suporte a roles para autorização (ex: ADMIN, USER)  

---

## Estrutura do Projeto

- **Model**: Entidade `User` com username, password codificada e role  
- **Repository**: `UserRepository` para acesso a dados  
- **Service**: `JwtService` (geração/validação do token), `AuthService` (lógica de autenticação)  
- **Controller**: `AuthController` para login e validação, `TestProtectedController` para testes de endpoints protegidos  
- **Config**: `SecurityConfig` para regras do Spring Security, configuração JWT e criação inicial de usuários  

## 📚 Documentação da API

A documentação interativa está disponível em:
http://localhost:8080/swagger-ui/index.html

Lá você pode testar os endpoints e ver descrições detalhadas de cada um.

---

## 🧪 Testes Automatizados

Testes integrados foram implementados com JUnit 5 e MockMvc para garantir:

- Autenticação bem-sucedida e falha  
- Validação correta de tokens  
- Proteção de endpoints sem token ou com token inválido  
- Restrição de acesso baseado em roles  

---

## 📈 Testes de Carga (JMeter)

Inclui roteiro básico para simular múltiplos usuários realizando login para avaliar performance.

---

## 🔧 Como Rodar

1. Clone o repositório  
2. Configure a variável de ambiente para `jwt.secret` (em produção)  
3. Execute via Maven ou IDE:  

```bash
./mvnw spring-boot:run
```

## Acesse

- API em: [http://localhost:8080](http://localhost:8080)  
- H2 Console em: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)  
- Swagger UI em: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)  

---

## Usuários padrões criados no startup

- **admin** / senha: `123456` (role ADMIN)  
- **user** / senha: `password` (role USER)  

---

## Contato

Desenvolvido por Samuel Vidal


---

## Licença

Este projeto está licenciado sob a licença Apache 2.0 - veja o arquivo [LICENSE](LICENSE) para detalhes.

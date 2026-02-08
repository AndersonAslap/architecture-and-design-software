# Clean Architecture — Estrutura, intenções e exemplos

Este documento descreve a intenção da pasta `clean-arch`, explicando a **estrutura de pastas**, o **papel de cada camada** e **exemplos práticos** baseados na Clean Architecture de Robert C. Martin (*Uncle Bob*).

O objetivo é servir como **referência didática** e **modelo base** para projetos que buscam:

* independência de frameworks
* alta testabilidade
* separação clara de responsabilidades
* evolução do sistema sem acoplamento excessivo

---

## Visão geral

A Clean Architecture organiza o código em **camadas concêntricas**, onde:

* **camadas externas dependem das internas**
* **camadas internas nunca dependem das externas**

Isso garante que regras de negócio não sejam impactadas por detalhes técnicos como banco de dados, frameworks web ou bibliotecas externas.

### Benefícios principais

* Independência de frameworks
* Facilidade de testes unitários
* Troca de banco, UI ou framework sem refatorar regras de negócio
* Código mais legível e sustentável a longo prazo

---

## Terminologia essencial

* **Entities**
  Objetos de negócio centrais que contêm regras críticas e invariantes do domínio.

* **Use Cases / Interactors**
  Regras da aplicação que coordenam entidades para executar um fluxo específico.

* **Interface Adapters**
  Adaptadores que convertem dados entre formatos externos (HTTP, DB, UI) e os formatos usados internamente.

* **Frameworks & Drivers**
  Detalhes externos como banco de dados, frameworks web, bibliotecas, mensageria, etc.

---

## Estrutura geral de pastas

```txt
clean-arch/
 ├── readme.md
 ├── src/
 │    ├── domain/
 │    ├── application/
 │    ├── infrastructure/
 │    └── adapters/
```

Cada pasta representa **uma camada arquitetural**, não um tipo de tecnologia.

---

## Estrutura de pastas e responsabilidades

### 1️⃣ `domain/` — Domínio (núcleo do sistema)

📌 **Camada mais interna e mais importante**

**Intenção**
Conter as regras de negócio puras e os conceitos centrais do problema.

**O que deve existir aqui**

* Entities
* Value Objects
* Interfaces (ports) de repositórios e serviços
* Exceções de domínio
* Eventos de domínio

**O que NÃO deve existir**

* Frameworks
* ORM
* HTTP
* Banco de dados
* Bibliotecas externas

```txt
src/domain/
 ├── entities/
 │    └── User.ts
 ├── value-objects/
 │    └── EmailAddress.ts
 ├── ports/
 │    └── IUserRepository.ts
 ├── events/
 │    └── UserCreated.ts
 └── errors/
      └── DomainError.ts
```

**Exemplo (pseudocódigo)**

```ts
class User {
  constructor(id, email, name) { }
  changeEmail(newEmail) {
    // valida regras de negócio
  }
}
```

---

### 2️⃣ `application/` — Casos de uso

📌 **Orquestra o domínio, mas não contém regras profundas**

**Intenção**
Implementar os **casos de uso da aplicação**, coordenando entidades e portas.

**O que deve existir aqui**

* Use Cases (Interactors)
* DTOs de entrada e saída
* Interfaces de serviços de aplicação
* Regras de fluxo (não regras de negócio)

**Dependências**

* Pode depender de `domain`
* Nunca depende de `infrastructure`

```txt
src/application/
 ├── usecases/
 │    └── CreateUserUseCase.ts
 ├── dto/
 │    └── CreateUserInput.ts
 └── ports/
      └── EmailSender.ts
```

**Exemplo**

```ts
class CreateUserUseCase {
  constructor(userRepository) {}
  async execute(inputDTO) {
    // cria entidade
    // aplica regras
    // persiste
  }
}
```

---

### 3️⃣ `adapters/` — Interface Adapters

📌 **Tradução entre o mundo externo e o mundo interno**

**Intenção**
Adaptar formatos externos para os formatos internos usados pelos casos de uso.

**O que deve existir aqui**

* Controllers (HTTP, CLI, Webhook)
* Presenters / Serializers
* Mappers (DTO ↔ Entity)

```txt
adapters/
 ├── http/
 │    └── UserController.ts
 ├── presenters/
 │    └── UserPresenter.ts
 └── mappers/
      └── UserMapper.ts
```

**Responsabilidade-chave**

> Converter dados, nunca decidir regras de negócio.

---

### 4️⃣ `infrastructure/` — Frameworks & Drivers

📌 **Detalhes técnicos e implementações concretas**

**Intenção**
Conter tudo que é **volátil** ou **substituível**.

**O que deve existir aqui**

* Implementações de repositórios
* ORM
* Banco de dados
* Mensageria
* Integrações externas
* Serviços técnicos (email, cache, auth)

```txt
src/infrastructure/
 ├── repositories/
 │    └── SqlUserRepository.ts
 ├── database/
 │    └── connection.ts
 ├── email/
 │    └── SmtpEmailSender.ts
 └── config/
      └── env.ts
```

Essas classes **implementam interfaces** definidas nas camadas internas.

---

## Regras de dependência (Dependency Rule)

* Código sempre depende **para dentro**
* Nada em `domain` conhece `application`, `adapters` ou `infrastructure`
* Nada em `application` conhece `infrastructure`

### Dependency Inversion Principle (DIP)

* Camadas de alto nível dependem de **abstrações**
* Implementações concretas ficam nas camadas externas
* Interfaces vivem no domínio ou na aplicação

---

## Fluxo típico de uma requisição HTTP

```txt
HTTP Request
 ↓
Controller (adapter)
 ↓
Use Case (application)
 ↓
Entity (domain)
 ↓
Repository Interface (domain/application)
 ↓
Repository Implementation (infrastructure)
```

---

## Testabilidade

* **Domain**: testes unitários puros
* **Application**: testes de casos de uso com mocks
* **Adapters + Infra**: testes de integração

Nada impede testar camadas isoladamente.

---

## Boas práticas

* Regras de negócio nunca em controllers
* Use Cases devem ser finos
* Entidades devem proteger invariantes
* Interfaces pequenas e intencionais
* Evite DTOs vazando detalhes de infraestrutura
* Nomeie pastas por **responsabilidade**, não por tecnologia

---

## Erros comuns

* Lógica de negócio na infra
* Controllers “inteligentes”
* Repositórios genéricos demais
* Entidades anêmicas
* DTOs misturados com entidades

---

## Referências

* **Clean Architecture** — Robert C. Martin
* Arquitetura Hexagonal (Ports and Adapters)
* Onion Architecture

Perfeito — vou **acrescentar duas sessões bem didáticas, diretas e sem romantizar a arquitetura**, deixando claro **tradeoffs, quando usar, quando não usar e o nível real de complexidade ao longo do tempo**.
O texto abaixo já está no **mesmo tom do documento**, pronto para entrar no `readme.md`.

---

## Tradeoffs da Clean Architecture

A Clean Architecture **não é “de graça”**. Ela troca simplicidade imediata por flexibilidade e robustez futura. Entender os tradeoffs evita frustração e overengineering.

### Benefícios (o que você ganha)

* **Isolamento de regras de negócio**

  * O domínio não depende de banco, framework, HTTP ou mensageria.
  * Facilita mudanças estruturais sem quebrar regras críticas.

* **Alta testabilidade**

  * Entities e Use Cases são testados sem mockar framework.
  * Testes são rápidos, determinísticos e baratos.

* **Evolução segura**

  * Trocar REST por GraphQL, PostgreSQL por Mongo, ou Web por Mobile não afeta o core.
  * Menos “efeito dominó” em mudanças.

* **Escalabilidade organizacional**

  * Times grandes conseguem trabalhar em paralelo com menos conflito.
  * Contratos claros (ports) reduzem acoplamento entre squads.

---

### Custos (o que você paga)

* **Mais código e mais arquivos**

  * Interfaces, DTOs, mappers e camadas adicionais aumentam o volume inicial.

* **Curva de aprendizado**

  * Para quem vem de MVC ou CRUD puro, o modelo mental é mais complexo.
  * Exige disciplina arquitetural do time.

* **Overhead cognitivo**

  * Nem toda regra simples precisa de um Use Case formal.
  * Se mal aplicada, vira “arquitetura cerimonial”.

* **Produtividade inicial menor**

  * O “time to first feature” é mais lento comparado a abordagens diretas.

---

### Tradeoffs

> **Clean Architecture troca velocidade inicial por sustentabilidade a médio e longo prazo.**

---

## Quando utilizar (e quando NÃO utilizar) Clean Architecture

Essa seção é **intencionalmente objetiva**. Use como checklist.

---

### Projetos ideais para Clean Architecture

Use **Clean Architecture** quando o projeto tem **pelo menos um** dos cenários abaixo:

* **Domínio com regras não triviais**

  * Ex.: financeiro, pagamentos, identidade, autorização, contratos, workflows, omnichannel, automações.
* **Produto com expectativa de vida longa**

  * Sistemas que vão evoluir por anos.
* **Múltiplas interfaces**

  * API + Web + Mobile + Integrações externas.
* **Alta probabilidade de mudança tecnológica**

  * Banco, mensageria, framework ou provider podem mudar.
* **Time médio ou grande**

  * Mais de 3–4 pessoas trabalhando simultaneamente.
* **Necessidade forte de testes**

  * Regras críticas que não podem quebrar silenciosamente.

**Exemplos reais:**

* Sistemas SaaS
* Plataformas de atendimento (como omnichannel, bots, CRM)
* Sistemas financeiros
* Backends de produto principal (core business)

---

### Projetos onde NÃO vale a pena

Evite Clean Architecture quando:

* **Projeto muito simples**

  * CRUD básico sem regras reais.
* **Prova de conceito (POC)**

  * Código descartável.
* **Scripts, automações pequenas, integrações pontuais**
* **Projetos com prazo extremamente curto**

  * MVP de validação rápida sem expectativa de evolução.

Nesses casos, o custo **não se paga**.

---

## Nível de complexidade ao longo do ciclo do projeto

Aqui está a parte que quase ninguém explica direito 👇

---

### Início do projeto

**Complexidade percebida: ALTA**

* Muitas abstrações “sem uso aparente”
* Sensação de:

  > “Tem muita coisa pra pouco código”
* Time ainda não sente os benefícios
* Requer liderança técnica firme para não desistir

👉 **É a fase mais dolorosa**

---

### Meio do projeto

**Complexidade percebida: MÉDIA (equilibrada)**

* Casos de uso começam a se repetir
* Mudanças passam a ser locais (menos efeito colateral)
* Testes dão segurança para refatorações
* Novas features seguem padrões claros

👉 **Aqui a arquitetura começa a se pagar**

---

### Fim do projeto / longo prazo

**Complexidade percebida: BAIXA (comparada ao tamanho do sistema)**

* Sistema grande, mas organizado
* Regras de negócio continuam legíveis
* Trocas de tecnologia são viáveis
* Onboarding de novos devs é mais previsível

👉 **Sem essa arquitetura, o projeto estaria “travado”**

---

## Sessão-chave: quando DEVE ser utilizada essa abordagem

Use **Clean Architecture obrigatoriamente** quando:

* O **negócio é mais importante que a tecnologia**
* O sistema **vai mudar mais do que você imagina**
* Você quer:

  * reduzir risco
  * ganhar previsibilidade
  * proteger regras críticas
* O projeto **não é descartável**

**Regra prática:**

> Se perder o sistema causa prejuízo real → use Clean Architecture.

---

## Benefícios estratégicos ao longo do tempo

| Momento do projeto | Benefício principal             |
| ------------------ | ------------------------------- |
| Início             | Clareza de intenção e contratos |
| Crescimento        | Isolamento de mudanças          |
| Escala             | Sustentabilidade técnica        |
| Longo prazo        | Redução de dívida técnica       |

---

## Conclusão honesta

Clean Architecture **não é para todo projeto**,
mas **é para projetos que importam**.

Ela exige maturidade técnica, mas:

* protege o domínio,
* desacopla decisões,
* e evita que o sistema vire refém de frameworks.
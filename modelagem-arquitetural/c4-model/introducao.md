# 📚 C4 Model — Modelo de Arquitetura de Software em Quatro Níveis

## 🧠 Introdução

A comunicação da **arquitetura de software** sempre foi um desafio dentro da engenharia de software. Diferente de áreas como engenharia civil, onde existem padrões claros para representar projetos arquitetônicos (plantas, cortes, elevações), na engenharia de software muitas vezes encontramos diagramas confusos, inconsistentes e difíceis de interpretar.

Foi para resolver esse problema que o **C4 Model** foi proposto por Simon Brown.

O **C4 Model** define uma abordagem estruturada para **visualizar e documentar a arquitetura de sistemas de software**, utilizando **quatro níveis de abstração** que ajudam a comunicar diferentes aspectos de um sistema para diferentes públicos.

Esses níveis funcionam como um **zoom progressivo**, semelhante ao funcionamento de um mapa digital como o Google Maps, permitindo começar com uma visão geral do sistema e avançar gradualmente para níveis mais detalhados.

Ao longo deste material, você aprenderá:

* O que é o **C4 Model**
* Quais são seus **quatro níveis de abstração**
* Como utilizar cada nível na documentação de software
* Para quais públicos cada diagrama é mais adequado
* Boas práticas para aplicar o modelo na prática

---

## 📖 Conceitos Fundamentais

### O problema da documentação arquitetural

Na prática, quando pedimos a um desenvolvedor para representar a arquitetura de um sistema, frequentemente recebemos:

* Diagramas com **caixas e linhas sem padrão**
* **Nomenclatura inconsistente**
* Relações não explicadas
* Falta de indicação de tecnologias
* Mistura de níveis de abstração

Esse cenário torna a documentação:

* Difícil de entender
* Difícil de manter
* Pouco útil para comunicação entre equipes

O **C4 Model** foi criado exatamente para resolver esse problema.

---

### O que é o C4 Model?

O **C4 Model** é um modelo de documentação arquitetural baseado em **quatro níveis de abstração**:

1. **Context (Contexto)**
2. **Container**
3. **Component**
4. **Code**

Cada nível responde a perguntas diferentes sobre o sistema e se destina a públicos distintos.

A principal ideia é **começar com uma visão macro e ir aproximando o zoom até chegar ao nível mais detalhado**.

---

### Analogia com mapas (Google Maps)

O funcionamento do C4 Model pode ser comparado a um sistema de mapas:

| Nível      | Analogia                |
| ---------- | ----------------------- |
| Contexto   | Continente ou país      |
| Container  | Região ou cidade        |
| Componente | Bairro ou rua           |
| Código     | Detalhes de um edifício |

Assim, cada nível adiciona **mais detalhes ao sistema**.

---

## 🔎 Explicação Detalhada

## 1️⃣ Nível de Contexto (System Context)

O **nível de contexto** é o nível mais alto do C4 Model.

Seu objetivo é mostrar **como o sistema se relaciona com o mundo ao redor**.

### O que esse nível mostra

* Usuários do sistema
* Sistemas externos
* Integrações
* Responsabilidade geral do sistema

### Pergunta que esse nível responde

> Como o sistema se encaixa no ambiente ao seu redor?

### Público-alvo

Esse nível é ideal para:

* Stakeholders
* Product Managers
* Executivos
* Equipes de negócio

### Exemplo

Imagine um sistema de e-commerce.

O diagrama de contexto poderia mostrar:

* Cliente
* Sistema de pagamento
* Sistema de logística
* Plataforma de e-commerce

Fluxo simplificado:

```
Cliente → Sistema de E-commerce → Gateway de Pagamento
                               → Sistema de Entrega
```

Esse diagrama **não mostra detalhes técnicos**, apenas as relações externas.

---

## 2️⃣ Nível de Containers

O segundo nível mostra **o que existe dentro do sistema**.

⚠️ Importante:
No C4 Model, **container não tem relação com Docker**.

Container significa simplesmente **uma unidade executável ou de armazenamento dentro do sistema**.

### Exemplos de containers

* Aplicação Web
* API Backend
* Banco de Dados
* Aplicação Mobile
* Sistema de arquivos
* Microserviços

### Pergunta que esse nível responde

> Quais são os blocos principais que compõem o sistema?

### Exemplo de containers em um sistema

```
Sistema de E-commerce

Frontend Web (React)
Backend API (Node.js)
Banco de Dados (PostgreSQL)
Aplicativo Mobile
Sistema de Cache (Redis)
```

### Importância desse nível

Esse nível ajuda a:

* Compreender a **estrutura tecnológica**
* Identificar **responsabilidades**
* Planejar **infraestrutura**
* Estimar **custos e recursos humanos**

Por isso, esse nível é muito útil em:

* Planejamento de projetos
* Apresentação para stakeholders
* Estimativa de esforço técnico

---

## 3️⃣ Nível de Componentes

O terceiro nível aprofunda o detalhamento **dentro de um container específico**.

Aqui o objetivo é identificar **quais componentes internos existem dentro daquele container**.

### Pergunta que esse nível responde

> Como um container específico é estruturado internamente?

### Exemplo

Dentro de uma API backend podemos ter:

```
API Backend

Controller
Service
Repository
Auth Module
Payment Module
Notification Module
```

Cada componente possui responsabilidades claras.

Esse nível permite discutir:

* Arquitetura interna
* Padrões de projeto
* Organização de código
* Regras de negócio

### Público-alvo

Esse nível é ideal para:

* Arquitetos de software
* Desenvolvedores
* Equipes técnicas

### Complexidade

Esse é frequentemente o **nível mais difícil de desenhar**, porque ele envolve:

* Modelagem do domínio
* Estrutura de negócio
* Requisitos funcionais e não funcionais

---

## 4️⃣ Nível de Código

O quarto nível representa **o detalhamento da implementação**.

Aqui podem ser utilizados diagramas como:

* Diagramas de classe
* Diagramas de entidade-relacionamento
* Diagramas UML

Esses diagramas mostram:

* Classes
* Métodos
* Relações entre objetos

Exemplo simplificado:

```java
class User {
   id
   name
   email
}

class Order {
   id
   total
   userId
}
```

---

### Por que esse nível raramente é usado?

Existem duas razões principais.

#### 1️⃣ Alto custo de manutenção

O código muda constantemente:

* Novas funcionalidades
* Correções
* Refatorações

Manter a documentação sincronizada com o código pode ser **muito trabalhoso**.

---

#### 2️⃣ Metodologias ágeis

Metodologias modernas priorizam:

* documentação leve
* código como fonte da verdade

Por isso, muitas equipes preferem gerar diagramas automaticamente.

Ferramentas de **análise estática de código** podem gerar diagramas atualizados automaticamente.

---

## 💡 Exemplos práticos

### Exemplo de aplicação do C4 Model

Imagine um sistema de streaming.

#### Contexto

```
Usuário
   ↓
Sistema de Streaming
   ↓
Gateway de Pagamento
   ↓
CDN
```

---

#### Containers

```
Web App
Mobile App
API Backend
Banco de Dados
Sistema de Recomendação
```

---

#### Componentes da API

```
Auth Controller
User Service
Recommendation Service
Video Service
Payment Service
```

---

#### Código

```
class VideoService {
   playVideo()
   recommendVideos()
}
```

---

## ⚠️ Pontos importantes

* O **C4 Model não define iconografia obrigatória**
* O foco principal está nos **níveis de abstração**
* Cada nível se comunica com **um público diferente**
* A documentação deve ser **progressiva**
* O nível de **código geralmente não é necessário**
* Ferramentas podem gerar diagramas automaticamente

---

## 📝 Resumo do conteúdo

O **C4 Model** é um modelo de documentação arquitetural que organiza a representação de sistemas em **quatro níveis de abstração**.

Esses níveis são:

1. **Contexto** — visão do sistema dentro do ambiente
2. **Containers** — principais blocos tecnológicos do sistema
3. **Componentes** — estrutura interna de um container
4. **Código** — detalhamento da implementação

A grande vantagem do C4 Model é permitir **comunicação clara entre diferentes públicos**, indo de uma visão macro até um nível mais técnico.

---

## 🎯 Perguntas para revisão

1. Qual é o principal objetivo do **C4 Model** na arquitetura de software?

2. Quais são os **quatro níveis de abstração** do modelo?

3. Por que o termo **container no C4 Model não tem relação com Docker**?

4. Qual é o nível mais indicado para discutir **arquitetura interna e padrões de projeto**?

5. Por que o **nível de código geralmente não é recomendado na documentação manual**?

---

## 📌 Conclusão

O **C4 Model** é uma abordagem poderosa para representar arquiteturas de software de forma **simples, progressiva e compreensível**.

Ao dividir a documentação em **quatro níveis de abstração**, ele permite:

* Melhor comunicação entre equipes
* Clareza arquitetural
* Documentação mais organizada
* Maior alinhamento entre negócio e tecnologia

Na prática, a maioria das equipes utiliza principalmente os **três primeiros níveis**:

* Contexto
* Containers
* Componentes

Esses níveis já fornecem uma visão suficiente para entender e evoluir sistemas complexos, mantendo a documentação útil e sustentável ao longo do tempo.

## 🎯 Público-alvo de cada nível do C4 Model

Cada nível do **C4 Model**, proposto por Simon Brown, foi pensado para **comunicar a arquitetura para públicos diferentes**.
À medida que o nível aprofunda o detalhe técnico, o público também se torna **mais especializado**.

A tabela abaixo resume isso:

| Nível do C4 Model      | O que mostra                                                           | Público-alvo principal                                                     | Objetivo da comunicação                                                    |
| ---------------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Context (Contexto)** | O sistema e sua relação com usuários e sistemas externos               | Stakeholders, Product Managers, Executivos, Equipe de Negócio              | Explicar **para que serve o sistema** e como ele se encaixa no ecossistema |
| **Container**          | Principais blocos técnicos do sistema (APIs, aplicações, bancos, etc.) | Arquitetos de software, Tech Leads, Desenvolvedores, Stakeholders técnicos | Mostrar **como o sistema é estruturado tecnologicamente**                  |
| **Component**          | Componentes internos de um container específico                        | Desenvolvedores, Arquitetos de software, Tech Leads                        | Explicar **como as partes internas do sistema funcionam**                  |
| **Code**               | Estrutura detalhada de classes, entidades e código                     | Desenvolvedores                                                            | Mostrar **como implementar o sistema no nível de código**                  |

---

### 📌 Regra prática para lembrar

Quanto mais você **aproxima o zoom**, mais **técnico** é o público.

| Nível     | Zoom                    | Público         |
| --------- | ----------------------- | --------------- |
| Context   | 🌍 Visão macro          | Negócio         |
| Container | 🏙 Estrutura do sistema | Arquitetura     |
| Component | 🏠 Estrutura interna    | Engenharia      |
| Code      | 🔬 Implementação        | Desenvolvedores |

---

💡 **Dica importante usada em empresas grandes**

Na prática, muitas equipes usam principalmente **apenas três níveis**:

* Context
* Container
* Component

O nível **Code** raramente é mantido manualmente porque **o código muda constantemente**.

---

Criar **diagramas do C4 Model automaticamente a partir do código** é uma prática cada vez mais comum para evitar um dos maiores problemas da documentação arquitetural: **ficar desatualizada**.

A ideia é simples:

> O **código é a fonte da verdade**, e os diagramas são **gerados automaticamente** a partir dele.

Isso pode ser feito com ferramentas que **analisam o código ou usam uma DSL (Domain Specific Language)** para gerar os diagramas.

---

# 🧠 Estratégias para gerar C4 automaticamente

Existem **3 abordagens principais** usadas na indústria.

| Abordagem     | Como funciona                                      | Ferramentas comuns  |
| ------------- | -------------------------------------------------- | ------------------- |
| Model-based   | Você descreve o sistema em código e gera diagramas | Structurizr         |
| Code analysis | Ferramenta analisa o código e gera diagramas       | ArchUnit, CodeScene |
| Annotations   | Você adiciona anotações no código e gera diagramas | C4-PlantUML         |

A abordagem **mais usada atualmente** é com **Structurizr**.

---

# 🚀 1️⃣ Structurizr (a solução mais usada)

O **Structurizr** foi criado pelo próprio autor do C4 Model.

Ele permite:

* Modelar arquitetura **como código**
* Gerar **diagramas C4 automaticamente**
* Exportar para:

  * PlantUML
  * Mermaid
  * imagens
  * documentação

Ferramenta:

Structurizr

---

## Exemplo simples de arquitetura como código

```java
Workspace workspace = new Workspace("Sistema E-commerce", "Exemplo C4");

Model model = workspace.getModel();

Person customer = model.addPerson("Cliente", "Usuário do sistema");

SoftwareSystem ecommerce = model.addSoftwareSystem("Sistema de E-commerce");

Container webApp = ecommerce.addContainer(
    "Web Application",
    "Aplicação web para clientes",
    "React"
);

Container api = ecommerce.addContainer(
    "API",
    "Backend do sistema",
    "Java Spring Boot"
);

Container database = ecommerce.addContainer(
    "Database",
    "Banco de dados",
    "PostgreSQL"
);

customer.uses(webApp, "Acessa");
webApp.uses(api, "Chama API");
api.uses(database, "Lê e escreve dados");
```

Isso gera automaticamente:

* **Context Diagram**
* **Container Diagram**

---

# 🧩 2️⃣ C4 + PlantUML (muito usado em times Dev)

Outra forma muito comum é usar:

* PlantUML

Com a biblioteca:

* **C4-PlantUML**

Isso permite gerar diagramas diretamente a partir de **arquivos de texto versionados no Git**.

---

## Exemplo

```plantuml
@startuml
!include C4_Context.puml

Person(user, "Usuário")

System(system, "Sistema de Pedidos")

System_Ext(payment, "Gateway de Pagamento")

Rel(user, system, "Faz pedidos")
Rel(system, payment, "Processa pagamento")

@enduml
```

Isso gera automaticamente o **diagrama de contexto**.

---

# ⚙️ 3️⃣ Gerar diagramas a partir da estrutura do código

Algumas ferramentas analisam o código diretamente.

Exemplo:

* ArchUnit
* CodeScene

Elas podem detectar:

* módulos
* dependências
* arquitetura

Exemplo com **Java packages**:

```id="ex1"
com.app.controller
com.app.service
com.app.repository
com.app.domain
```

Ferramentas conseguem montar diagramas mostrando as dependências.

---

# 🏗️ Exemplo prático (pipeline automatizado)

Um fluxo moderno de documentação pode ser:

```text
Código fonte
     ↓
Structurizr DSL
     ↓
Gerador de diagramas
     ↓
PlantUML / Mermaid
     ↓
Documentação (Markdown / Confluence)
```

Assim:

* toda alteração no código
* atualiza os diagramas automaticamente

---

# 📦 Exemplo de projeto com documentação automática

Estrutura típica:

```id="ex2"
project
 ├─ src
 │   ├─ controller
 │   ├─ service
 │   ├─ repository
 │
 ├─ architecture
 │   ├─ workspace.dsl
 │
 ├─ diagrams
 │   ├─ context.puml
 │   ├─ container.puml
```

---

# ⚠️ Boas práticas

### 1️⃣ Documentação como código

Mantenha diagramas no **repositório Git**.

---

### 2️⃣ Automatize no CI/CD

Exemplo:

```id="ex3"
Git push
   ↓
CI Pipeline
   ↓
Generate diagrams
   ↓
Publish documentation
```

---

### 3️⃣ Não documente demais

No C4 Model geralmente basta:

* Context
* Container
* Component

O nível **Code** raramente compensa manter manualmente.

---

# 🏆 Stack moderna para C4 automatizado

Uma stack muito usada hoje:

| Ferramenta  | Função        |
| ----------- | ------------- |
| Structurizr | Modelagem C4  |
| PlantUML    | Renderização  |
| Git         | Versionamento |
| CI/CD       | Automação     |
| Markdown    | Documentação  |

---

# 💡 Exemplo de fluxo usado em empresas grandes

```text
Developer escreve código
        ↓
Arquitetura definida em Structurizr DSL
        ↓
Pipeline gera diagramas C4
        ↓
Diagramas publicados na documentação
```

Resultado:

✔ documentação sempre atualizada
✔ diagramas padronizados
✔ fácil manutenção

---

✅ **Regra usada por arquitetos experientes**

> "Arquitetura deve ser **versionada como código**."
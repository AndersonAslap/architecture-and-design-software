Perfeito — agora você entrou na parte que separa um sistema “que funciona” de um sistema **que escala, não quebra e dá lucro**.

Se requisitos funcionais dizem **o que o sistema faz**, os não funcionais dizem:

> **como bem o sistema faz isso**

---

# 🧠 O que são Requisitos Não Funcionais (RNF)

São **restrições e qualidades do sistema**.

Eles respondem perguntas como:

* O sistema é rápido?
* Aguenta quantos usuários?
* É seguro?
* Pode cair?
* Funciona no celular?
* Dá pra manter?

---

# 🧱 Tipos de Requisitos Não Funcionais

Aqui estão os principais (isso cai MUITO na prática):

---

## ⚡ 1. Performance

Velocidade e tempo de resposta

Ex:

* Tempo de resposta < 2 segundos
* Processamento de mensagens em tempo real

---

## 📈 2. Escalabilidade

Capacidade de crescer

Ex:

* Suportar 10.000 conexões simultâneas
* Escalar horizontalmente

---

## 🔒 3. Segurança

Proteção de dados

Ex:

* Autenticação JWT
* Criptografia HTTPS
* Proteção contra XSS/SQL Injection

---

## 🟢 4. Disponibilidade

Tempo no ar

Ex:

* 99.9% de uptime
* Failover automático

---

## 🧪 5. Confiabilidade

Sistema não falha ou se recupera

Ex:

* Retry automático
* Logs de erro
* Circuit breaker

---

## 🧩 6. Manutenibilidade

Facilidade de evolução

Ex:

* Código modular
* Arquitetura desacoplada
* Testes automatizados

---

## 🌐 7. Usabilidade

Experiência do usuário

Ex:

* Interface responsiva
* Tempo de aprendizado baixo

---

## 🔗 8. Integração

Comunicação com outros sistemas

Ex:

* APIs REST
* Webhooks
* Suporte a múltiplos canais

---

## 📊 9. Observabilidade (MUITO importante hoje)

Você sabe o que está acontecendo no sistema?

Ex:

* Logs estruturados
* Métricas (CPU, memória, latência)
* Tracing distribuído

---

# 📌 Como escrever um RNF de forma profissional

Um RNF bom precisa ser:

✔ Mensurável
✔ Testável
✔ Claro
✔ Objetivo

---

### ❌ Exemplo ruim:

> “O sistema deve ser rápido”

---

### ✅ Exemplo bom:

> “O sistema deve responder requisições em até 2 segundos para 95% dos casos”

---

# 🧱 Estrutura de um documento de RNF

---

## 1. Introdução

Contexto do sistema

---

## 2. Escopo

Define o que os RNFs cobrem

---

## 3. Classificação dos RNFs

Separar por categorias (performance, segurança, etc.)

---

## 4. Lista de Requisitos Não Funcionais

Cada requisito com:

* ID
* Nome
* Descrição
* Métrica
* Critério de aceitação

---

## 5. Métricas e SLAs

Define limites claros:

* Latência
* Uptime
* Throughput

---

## 6. Restrições técnicas (opcional)

Ex:

* Deve rodar em cloud
* Deve usar containers

---

## 7. Monitoramento e validação

Como você garante que os RNFs estão sendo cumpridos

---

# 🧩 TEMPLATE PROFISSIONAL (PRONTO PRA USAR)

---

# 📄 Documento de Requisitos Não Funcionais

## 1. Introdução

Este documento descreve os requisitos não funcionais do sistema **[Nome do Sistema]**, definindo padrões de qualidade, desempenho, segurança e escalabilidade.

---

## 2. Escopo

Este documento cobre todos os aspectos não funcionais do sistema, incluindo performance, segurança, disponibilidade e manutenção.

---

## 3. Classificação dos Requisitos

* Performance
* Escalabilidade
* Segurança
* Disponibilidade
* Confiabilidade
* Usabilidade
* Observabilidade
* Integração

---

## 4. Requisitos Não Funcionais

---

### RNF01 — Tempo de Resposta

O sistema deve responder requisições em até **2 segundos** para 95% dos usuários.

**Métrica:**

* Latência média e p95

**Critério de Aceitação:**

* Testes de carga devem comprovar tempo inferior a 2s

---

### RNF02 — Escalabilidade

O sistema deve suportar até **10.000 usuários simultâneos** sem degradação significativa.

**Métrica:**

* Número de conexões simultâneas

**Critério de Aceitação:**

* Testes de stress devem manter estabilidade

---

### RNF03 — Segurança

O sistema deve garantir comunicação segura via **HTTPS** e autenticação baseada em token.

**Métrica:**

* 100% das requisições protegidas

**Critério de Aceitação:**

* Nenhuma requisição deve trafegar sem criptografia

---

### RNF04 — Disponibilidade

O sistema deve ter disponibilidade mínima de **99.9%**.

**Métrica:**

* Uptime mensal

**Critério de Aceitação:**

* Monitoramento deve comprovar disponibilidade mínima

---

### RNF05 — Observabilidade

O sistema deve possuir logs estruturados e monitoramento em tempo real.

**Métrica:**

* Cobertura de logs e métricas

**Critério de Aceitação:**

* Todos os eventos críticos devem ser rastreáveis

---

### RNF06 — Manutenibilidade

O sistema deve possuir arquitetura modular e cobertura de testes automatizados.

**Métrica:**

* Cobertura de testes (>80%)

**Critério de Aceitação:**

* Código deve permitir alterações sem impacto sistêmico

---

## 5. SLAs e Métricas

| Métrica              | Valor    |
| -------------------- | -------- |
| Tempo de resposta    | ≤ 2s     |
| Uptime               | ≥ 99.9%  |
| Usuários simultâneos | ≥ 10.000 |

---

## 6. Restrições Técnicas

* O sistema deve ser executado em ambiente cloud
* Deve suportar containers (Docker)
* Deve utilizar arquitetura baseada em APIs

---

## 7. Monitoramento e Validação

* Uso de ferramentas de monitoramento (ex: logs, métricas, tracing)
* Testes de carga periódicos
* Alertas automáticos para falhas

---

---

# 🚀 Dica de especialista (nível avançado)

Se você quer construir um SaaS sério (tipo o seu omnichannel):

👉 Conecte RNFs com arquitetura

Exemplo:

* RNF de escala → usar filas (RabbitMQ, Kafka)
* RNF de disponibilidade → usar load balancer
* RNF de performance → usar cache (Redis)

---

# 🔥 O que pouca gente faz (mas deveria)

* Versionar RNFs junto com código
* Validar RNFs em CI/CD (teste de carga automático)
* Criar **SLOs e SLIs** (nível Google/AWS)
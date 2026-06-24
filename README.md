# 🧭 Charter de Teste Exploratório SBTM

Skill para geração automatizada de Charters de Teste Exploratório no formato **Session-Based Test Management (SBTM)**, com exploração guiada por **Heurísticas de Teste**.

---

## 🎯 Propósito

Apoiar analistas de testes na execução de **testes exploratórios** estruturados, combinando:

- **SBTM** (Session-Based Test Management) — metodologia de Jonathan Bach para organizar sessões de teste exploratório em blocos ininterruptos com charter, timebox e relatório
- **Heurísticas de Teste** — atalhos mentais e guias para direcionar a investigação (ALTR FACE, Fronteira, CRUD, Estado, Abordagem Contrária, Interrupção, etc.)

---

## 📋 Como usar

### Entrada

A skill aceita como entrada:

- Uma **User Story** completa (com critérios de aceitação)
- Um **Documento de Requisitos**
- Uma **descrição livre** da funcionalidade a ser testada

### Saída

A skill gera um Charter SBTM completo contendo:

| Seção | Descrição |
|---|---|
| **Introdução** | Explicação didática sobre testes exploratórios e heurísticas (para novos analistas) |
| **Identificação** | Título da missão com heurística explícita, funcionalidade alvo, duração sugerida |
| **Missão** | Objetivo central da sessão |
| **Heurísticas Recomendadas** | Heurística principal + heurísticas de apoio selecionadas conforme o contexto |
| **Áreas de Investigação** | O que explorar, mapeado a partir dos critérios de aceitação |
| **Recursos e Dados** | Dados de teste, ambientes e ferramentas necessários |
| **Fora do Escopo** | O que não será testado nesta sessão |
| **TBS (Task Breakdown)** | Métricas pós-sessão: Test Design & Execution, Bug Investigation, Session Setup, Charter vs Opportunity |
| **Notas da Sessão** | Descobertas marcadas como (I)nformação ou (R)isco |
| **Defeitos** | Bugs encontrados durante a exploração |
| **Issues** | Dúvidas sobre o comportamento esperado |
| **Debriefing PROOF** | Roteiro pós-sessão: Past, Results, Obstacles, Outlook, Feelings |

---

## 🧠 Seleção de Heurísticas

A skill seleciona automaticamente as heurísticas com base no **tipo de funcionalidade** identificado na User Story ou requisito:

| Tipo de Funcionalidade | Heurísticas Priorizadas |
|---|---|
| **Web com componentes dinâmicos** (modais, tooltips, menus, carousels, validações em tempo real) | **ALTR FACE** — Activation, Layers, Timing, Removable, Float, Achievable, Collision, Expansion |
| **Formulários e campos de entrada** (cadastros, filtros, buscas) | **Fronteira, Dados, Strings** — limites, caracteres especiais, injeção |
| **Fluxos de negócio** (pedidos, aprovações, transferências, agendamentos) | **CRUD, Siga os Dados, Interrupção** |
| **Segurança e permissões** (autenticação, roles, acesso, recuperação de senha) | **Abordagem Contrária, Estado** |
| **Qualquer funcionalidade** | Mínimo de **2 heurísticas gerais** |

### Exemplo prático de seleção

| User Story | Heurística principal | Heurísticas de apoio |
|---|---|---|
| Redefinição de senha (validações de campo + link expirado) | **Fronteira** | Estado, Abordagem Contrária, Interrupção |
| Cadastro de produto (formulário + upload de imagens) | **Fronteira** | CRUD, ALTR FACE, Abordagem Contrária |

---

## 📄 Estrutura do Charter Gerado
```markdown
🧭 CHARTER DE TESTE EXPLORATÓRIO — SBTM

### 📋 IDENTIFICAÇÃO
- **Título da Missão:** [heurística explícita no título]
- **Funcionalidade Alvo:**
- **Data / Versão:**
- **Duração sugerida:** [30-90 min]

### 🎯 MISSÃO
[Objetivo central da sessão]

### 🔍 HEURÍSTICAS RECOMENDADAS PARA ESTA SESSÃO
- **Heurística principal:** [nome e descrição]
- **Heurísticas de apoio:** [lista]

### 🔎 ÁREAS DE INVESTIGAÇÃO
- [Área 1 — com heurística aplicada]
- [Área 2 — com heurística aplicada]

### 🧩 RECURSOS E DADOS
- Dados de teste necessários
- Configurações / ambientes
- Ferramentas de apoio

### 🚫 FORA DO ESCOPO

### ⏱️ TIMEBOX

---
### 📊 TASK BREAKDOWN (TBS) — Preencher após a sessão
### 📝 NOTAS DA SESSÃO — (I) e (R)
### 🐞 DEFEITOS ENCONTRADOS
### ❓ ISSUES / PERGUNTAS
### 🔄 DEBRIEFING PROOF
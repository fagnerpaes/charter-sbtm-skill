# Charter de Teste Exploratório SBTM

Skill para geração automatizada de Charters de Teste Exploratório no formato **Session-Based Test Management (SBTM)**, com exploração guiada por **Heurísticas de Teste**.

---

## Propósito

Apoiar analistas de testes na execução de **testes exploratórios** estruturados, combinando:


## Introdução: Testes Exploratórios com Heurísticas

- **Teste Exploratório** 

É uma abordagem onde o analista aprende, projeta e executa testes ao mesmo tempo, usando conhecimento, criatividade e experiência para explorar o software em busca de comportamentos inesperados. Diferente do teste com script pré-definido, no teste exploratório cada sessão é única e guiada por uma missão (o Charter).

- **O que são Heurísticas de Teste?**

Heurísticas são **atalhos mentais, regras práticas ou guias** que ajudam o analista a decidir o que testar, como testar e onde procurar bugs. Elas funcionam como lentes que você aplica sobre a funcionalidade para enxergar riscos que o "caminho feliz" não mostra.

- **Session-Based Test Management (SBTM)**

Metodologia de Jonathan Bach para organizar o teste exploratório em sessões de teste exploratório em blocos ininterruptos de teste com um Charter (missão), timebox definido e um relatório ao final (Session Sheet). Cada sessão gera: descobertas, bugs, issues e métricas TBS (Task Breakdown).


## Referências

### Materiais de base

| # | Material | Autor | Ano | Tipo | Foco principal |
|---|---|---|---|---|---|
| 1 | **ALTR FACE — Uma Heurística de Testes para Aplicações Web Modernas** | Júlio de Lima | — | Heurística específica | Activation, Layers, Timing, Removable, Float, Achievable, Collision, Expansion — 8 heurísticas para testar componentes Web artesanais (modais, tooltips, menus, balões, carousels) |
| 2 | **Heurísticas de Teste** (Ataques de Tipos de Dados, Testes de Strings, Testes de UI, Sabedoria em Testes, Heurísticas Gerais) | Júlio de Lima (baseado em Test Obsessed, Elisabeth Hendrickson, James Lyndsay, Dale Emery) | — | Catálogo de heurísticas | Ataques de dados (nomes longos, caracteres especiais, datas inválidas, timeouts), strings (acentos, injeção SQL, espaços), UI (botão voltar, manipular URL, desativar JS), heurísticas gerais (CRUD, Siga os Dados, Interrupção) |
| 3 | **Heuristic Test Strategy Model v6.0** | James Bach (Satisfice, Inc.) | 2024 | Modelo estratégico | 9 técnicas gerais de teste (Function, Domain, Stress, Flow, Scenario, Claims, User, Risk, Tool-Supported), Product Elements (Structure, Function, Data, Interfaces, Platform, Operations, Time), Quality Criteria Categories (Capability, Reliability, Usability, Charisma, Security, Scalability, Compatibility, Performance, Installability, Development), Project Environment |
| 4 | **Session-Based Test Management** (STQE Magazine) | Jonathan Bach | Nov/Dez 2000 | Metodologia | Definição de sessões de teste como unidade básica de trabalho, charter, TBS (Task Breakdown: Test Design & Execution, Bug Investigation, Session Setup), métrica Charter vs Opportunity, debriefing PROOF (Past, Results, Obstacles, Outlook, Feelings), ToDo/Hopper, métricas de produtividade |
| 5 | **Relatório de Sessão — Exemplo Prático** | Júlio de Lima | 2025 | Exemplo aplicado | Session sheet real preenchida: charter com heurística explícita ("Explore a Funcionalidade de Transferência de Valores com a Heurística de Sabedoria em Testes com foco em Adotar a Abordagem Contrária"), notação (I) para Informações e (R) para Riscos, defeitos documentados, perguntas/issues|

---

## Como usar

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

## Seleção de Heurísticas

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

## Estrutura do Charter Gerado
```markdown
  CHARTER DE TESTE EXPLORATÓRIO — SBTM

### IDENTIFICAÇÃO
- **Título da Missão:** [heurística explícita no título]
- **Funcionalidade Alvo:**
- **Data / Versão:**
- **Duração sugerida:** [30-90 min]

### MISSÃO
[Objetivo central da sessão]

### HEURÍSTICAS RECOMENDADAS PARA ESTA SESSÃO
- **Heurística principal:** [nome e descrição]
- **Heurísticas de apoio:** [lista]

### ÁREAS DE INVESTIGAÇÃO
- [Área 1 — com heurística aplicada]
- [Área 2 — com heurística aplicada]

### RECURSOS E DADOS
- Dados de teste necessários
- Configurações / ambientes
- Ferramentas de apoio

### FORA DO ESCOPO

### TIMEBOX

---
### TASK BREAKDOWN (TBS) — Preencher após a sessão
### NOTAS DA SESSÃO — (I) e (R)
### DEFEITOS ENCONTRADOS
### ISSUES / PERGUNTAS
### DEBRIEFING PROOF
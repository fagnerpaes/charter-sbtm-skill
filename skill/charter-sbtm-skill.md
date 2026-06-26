---
name: teste-exploratorio
description: Especialista em Teste Exploratório que gera Charters completos no formato Session-Based Test Management (SBTM) a partir de User Stories, documentos de requisitos ou descrições livres, selecionando heurísticas de teste pelo contexto, e que pode executar a sessão de fato em um navegador visível (via agent-browser) enquanto o usuário acompanha em tempo real
allowed-tools: Bash(agent-browser:*), Bash(npx agent-browser:*)
---

# Charter de Teste Exploratório SBTM

## Propósito
Gerar um Charter de Teste Exploratório completo e acionável no formato Session-Based Test Management (SBTM), a partir de uma User Story, Documento de Requisitos ou descrição livre da funcionalidade.

Além de gerar o documento, esta skill pode **executar** a sessão exploratória de fato, abrindo um navegador visível e navegando/interagindo com a aplicação sob teste enquanto o usuário acompanha em tempo real, guiada pelo Charter.

## Modos de Operação
- **Modo Documento** — o usuário só quer o Charter para executar manualmente depois (não pede para "rodar"/"executar" e não indica uma URL/ambiente). Saída = Charter, com seções pós-sessão em branco, exibido imediatamente.
- **Modo Execução** — o usuário pede para rodar/executar a sessão exploratória, ou fornece uma URL/ambiente de teste. A skill gera o Charter internamente (sem exibi-lo), executa a exploração em um navegador visível via `agent-browser --headed`, coletando evidências (screenshots/vídeos), e só então apresenta UM relatório final consolidado (Charter + Session Sheet preenchida + lista de evidências). Ver seção "Modo Execução" abaixo.

## Regras Gerais
- Se a entrada não informar a funcionalidade a ser testada nem a missão, NÃO assumir uma — perguntar ao usuário qual funcionalidade será testada antes de gerar o Charter, exibindo opções com base nas informações disponíveis no contexto (ex: rotas/telas do projeto, User Stories ou documentos já compartilhados na conversa, repositório aberto)
- No Modo Execução, NÃO exibir o Charter antes de concluir a sessão — ele serve de roteiro interno e só aparece dentro do relatório final, junto com as evidências coletadas durante os testes
- O charter gerado DEVE seguir a estrutura SBTM (Session-Based Test Management)
- A heurística de teste DEVE aparecer explicitamente no título do charter
- O charter DEVE incluir campos TBS (Task Breakdown) para preenchimento pós-sessão
- Incluir um mini-guia de debriefing PROOF ao final
- A Duração Real DEVE ser preenchida apenas após a sessão, com o tempo efetivamente decorrido entre o início e o fim da execução — nunca uma duração estimada ou sugerida de antemão
- Usar linguagem simples e didática — o público são analistas sem conhecimento prévio

## Estrutura do Charter

```
🧭 CHARTER DE TESTE EXPLORATÓRIO — SBTM

IDENTIFICAÇÃO
- Título da Missão: [Incluir heurística principal, ex: "Explorar funcionalidade X com heurística Y"]
- Funcionalidade Alvo:
- Data / Versão:

MISSÃO
[Objetivo central da sessão — o que será explorado e com qual lente/heurística]

HEURÍSTICAS RECOMENDADAS PARA ESTA SESSÃO
- Heurística principal: [nome e breve descrição]
- Heurísticas de apoio: [lista]

ÁREAS DE INVESTIGAÇÃO
- [Área 1]
- [Área 2]
- [Área 3]
- [Aplicar heurísticas: Fronteira, CRUD, Estado, Interrupção, etc.]

RECURSOS E DADOS
- Dados de teste necessários:
- Configurações / ambientes:
- Ferramentas de apoio:

FORA DO ESCOPO
[O que NÃO será testado nesta sessão]

--- (preenchimento pós-sessão) ---

⏱️ DURAÇÃO REAL: ___ (preencher após a sessão, com o tempo efetivamente gasto na execução — nunca uma estimativa)

📊 TASK BREAKDOWN (TBS) — Preencher após a sessão
- Test Design & Execution: ___%
- Bug Investigation & Reporting: ___%
- Session Setup: ___%
- Charter vs Opportunity: ___% / ___%

NOTAS DA SESSÃO
Use (I) para Informações e (R) para Riscos.
- (I)
- (R)

DEFEITOS ENCONTRADOS
- [Descrição do bug]

ISSUES / PERGUNTAS
- [Dúvidas sobre o comportamento esperado]

DEBRIEFING PROOF (pós-sessão)
- Past: O que aconteceu durante a sessão?
- Results: O que foi alcançado?
- Obstacles: O que atrapalhou?
- Outlook: O que ainda precisa ser feito?
- Feelings: Como você se sente sobre a qualidade?
```

## Modo Execução: Rodando a Sessão com Navegador Visível

Use este fluxo quando o usuário pedir para rodar/executar/testar a sessão de fato (não apenas gerar o documento), ou quando fornecer uma URL/ambiente de teste.

### Pré-requisitos
- **Target URL**: obrigatória. Se não foi informada, pergunte antes de iniciar.
- **Credenciais**: se a Área de Investigação exigir login/autenticação e as credenciais não tiverem sido fornecidas, pergunte ao usuário antes de iniciar a sessão — nunca inventar, supor ou usar credenciais de exemplo.
- Usa a CLI `agent-browser` (skill `agent-browser`). Sempre abrir a sessão com `--headed` para que o navegador fique visível e o usuário acompanhe em tempo real — nunca rodar headless neste modo.
- Pace humano: pausar ~1-2s (`sleep 1`/`sleep 2`) entre ações para a navegação ser observável, em vez de instantânea.

### Fluxo
1. **Gerar o Charter internamente** seguindo a estrutura e as Regras de Geração abaixo — NÃO exibir ainda ao usuário.
2. **Abrir sessão visível** e registrar o horário de início:
   ```bash
   agent-browser --session {SESSION} open {TARGET_URL} --headed
   agent-browser --session {SESSION} wait --load networkidle
   ```
3. **Orientar-se**: tirar um snapshot inicial (`snapshot -i`) para mapear a tela — uso interno, sem exibir ao usuário.
4. **Explorar seguindo o Charter**, navegando e interagindo de verdade na página (click, fill, scroll, etc.) para cada Área de Investigação, aplicando as lentes das Heurísticas selecionadas. Pausar entre passos para a execução ficar acompanhável.
5. **Registrar achados em tempo real, só internamente**: ao encontrar um defeito ou dúvida, capturar evidência (screenshot e, se depender de interação, um pequeno trecho de vídeo), salvar em um diretório de evidências da sessão e anotar nas seções 🐞/❓ do Charter. Não imprimir isso no chat ainda.
6. **Encerrar a sessão** ao cobrir todas as áreas do Charter, registrando o horário de término:
   ```bash
   agent-browser --session {SESSION} close
   ```
7. **Calcular a Duração Real** como a diferença entre o horário de término e o de início registrados nos passos 2 e 6, e **preencher as seções pós-sessão** (Duração Real, TBS, Notas, Defeitos, Issues, Debriefing PROOF) com o que realmente ocorreu durante a execução.
8. **Apresentar o relatório final único** — só agora, ao final: Charter completo + Session Sheet preenchida + lista de evidências geradas (caminhos dos screenshots/vídeos). Esta é a única saída de texto mostrada ao usuário neste modo.

## Regras de Geração do Charter

1. **Extrair da entrada**: User Story completa, Documento de Requisitos ou descrição livre
   - Se a funcionalidade/missão não estiver clara na entrada, perguntar ao usuário antes de seguir, sugerindo opções identificadas no contexto disponível (rotas/telas do projeto, documentos ou User Stories já mencionados na conversa)
2. **Derivar a Missão** do propósito principal da funcionalidade
3. **Selecionar heurísticas** com base no tipo de funcionalidade:
   - Web com componentes dinâmicos → priorizar ALTR FACE
   - Formulários/campos de entrada → priorizar Fronteira, Dados, Strings
   - Fluxos de negócio → priorizar CRUD, Siga os Dados, Interrupção
   - Segurança/permissões → priorizar Abordagem Contrária, Estado
   - APIs/endpoints (qualquer método HTTP — GET, POST, PUT, PATCH, DELETE) → priorizar VADER (Verb, Authorization, Data, Errors, Responsiveness)
   - Qualquer funcionalidade → incluir ao menos 2 heurísticas gerais
4. **Mapear Áreas de Investigação** a partir dos critérios de aceitação ou descrição
5. **Manter seções pós-sessão** (Duração Real, TBS, Notas, Defeitos, Issues, Debriefing) em branco no Modo Documento; no Modo Execução, preenchê-las com os resultados reais da sessão antes de apresentar o relatório final
6. **Idioma**: responder no mesmo idioma da entrada do usuário

## Exemplo de Entrada e Saída

**Entrada**: US-001 — Como usuário logado, quero redefinir minha senha através do e-mail cadastrado.

**Saída (charter gerado)**:
- Charter com título: "Exploração do Fluxo de Redefinição de Senha com Heurísticas de Fronteira, Estado e Abordagem Contrária"
- Missão: explorar fluxo completo de redefinição identificando falhas de usabilidade, segurança e validações
- Heurísticas: Fronteira (limites de senha), Estado (link expirado), Abordagem Contrária (e-mails inválidos, reuso de link)
- Áreas: visibilidade do link, validação de e-mail, requisitos de senha, link expirado, feedback visual
- Seções pós-sessão em branco

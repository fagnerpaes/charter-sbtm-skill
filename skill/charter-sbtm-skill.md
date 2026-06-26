# Charter de Teste Exploratório SBTM

## Propósito
Gerar um Charter de Teste Exploratório completo e acionável no formato Session-Based Test Management (SBTM), a partir de uma User Story, Documento de Requisitos ou descrição livre da funcionalidade. A saída deve sempre incluir uma breve introdução sobre testes exploratórios e heurísticas para apoiar analistas iniciantes.

## Regras Gerais
- A saída DEVE começar com a seção "## Introdução: Testes Exploratórios com Heurísticas" (texto fixo abaixo)
- O charter gerado DEVE seguir a estrutura SBTM (Session-Based Test Management)
- A heurística de teste DEVE aparecer explicitamente no título do charter
- O charter DEVE incluir campos TBS (Task Breakdown) para preenchimento pós-sessão
- Incluir um mini-guia de debriefing PROOF ao final
- Usar linguagem simples e didática — o público são analistas sem conhecimento prévio

## Introdução Fixa (sempre incluir no início da saída)

```
## Introdução: Testes Exploratórios com Heurísticas

**Teste Exploratório** é uma abordagem onde o analista **aprende, projeta e executa testes ao mesmo tempo**, usando conhecimento, criatividade e experiência para explorar o software em busca de comportamentos inesperados.

Diferente do teste com script pré-definido, no teste exploratório cada sessão é única e guiada por uma **missão** (o Charter).

### O que são Heurísticas de Teste?
Heurísticas são **atalhos mentais, regras práticas ou guias** que ajudam o analista a decidir **o que testar, como testar e onde procurar bugs**. Elas funcionam como lentes que você aplica sobre a funcionalidade para enxergar riscos que o "caminho feliz" não mostra.

### Exemplos de Heurísticas

| Heurística | O que investigar |
|---|---|
| **Fronteira** | Testar nos limites (0, 1, 255, 256 caracteres) |
| **CRUD** | Create, Read, Update, Delete — todas as operações? |
| **Interrupção** | O que acontece se o fluxo for interrompido? |
| **Estado** | O comportamento muda conforme o estado do sistema? |
| **Duplicidade** | Dados repetidos são permitidos? |
| **ALTR FACE** | Activation, Layers, Timing, Removable, Float, Achievable, Collision, Expansion (para Web components) |
| **Abordagem Contrária** | Testar o que o sistema "não deveria fazer" |

### Session-Based Test Management (SBTM)
O SBTM organiza o teste exploratório em **sessões** — blocos ininterruptos de teste com um Charter (missão), timebox definido e um relatório ao final (Session Sheet). Cada sessão gera: descobertas, bugs, issues e métricas TBS (Task Breakdown).
```

## Estrutura do Charter (gerar após a Introdução)

```
CHARTER DE TESTE EXPLORATÓRIO — SBTM

IDENTIFICAÇÃO
- Título da Missão: [Incluir heurística principal, ex: "Explorar funcionalidade X com heurística Y"]
- Funcionalidade Alvo:
- Data / Versão:
- Duração sugerida: [30-90 min]

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

TIMEBOX: [minutos]

--- (preenchimento pós-sessão) ---

TASK BREAKDOWN (TBS) — Preencher após a sessão
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

## Regras de Geração do Charter

1. **Extrair da entrada**: User Story completa, Documento de Requisitos ou descrição livre
2. **Derivar a Missão** do propósito principal da funcionalidade
3. **Selecionar heurísticas** com base no tipo de funcionalidade:
   - Web com componentes dinâmicos → priorizar ALTR FACE
   - Formulários/campos de entrada → priorizar Fronteira, Dados, Strings
   - Fluxos de negócio → priorizar CRUD, Siga os Dados, Interrupção
   - Segurança/permissões → priorizar Abordagem Contrária, Estado
   - Qualquer funcionalidade → incluir ao menos 2 heurísticas gerais
4. **Mapear Áreas de Investigação** a partir dos critérios de aceitação ou descrição
5. **Sugerir timebox** entre 30-90 min (default 45 min)
6. **Manter seções pós-sessão** (TBS, Notas, Defeitos, Issues, Debriefing) em branco para preenchimento manual
7. **Idioma**: responder no mesmo idioma da entrada do usuário

## Exemplo de Entrada e Saída

**Entrada**: US-042 — Como usuário logado, quero redefinir minha senha através do e-mail cadastrado.

**Saída (charter gerado)**:
- Introdução fixa sobre Testes Exploratórios com Heurísticas
- Charter com título: "Exploração do Fluxo de Redefinição de Senha com Heurísticas de Fronteira, Estado e Abordagem Contrária"
- Missão: explorar fluxo completo de redefinição identificando falhas de usabilidade, segurança e validações
- Heurísticas: Fronteira (limites de senha), Estado (link expirado), Abordagem Contrária (e-mails inválidos, reuso de link)
- Áreas: visibilidade do link, validação de e-mail, requisitos de senha, link expirado, feedback visual
- Timebox: 45 min
- Seções pós-sessão em branco
🧭 CHARTER DE TESTE EXPLORATÓRIO — SBTM

📋 IDENTIFICAÇÃO
- Título da Missão: Exploração do Fluxo de Redefinição de Senha com Heurísticas de Fronteira, Estado e Abordagem Contrária
- Funcionalidade Alvo: Autenticação / Recuperação de Senha
- Duração sugerida: 45 min

🎯 MISSÃO
Explorar o fluxo completo de redefinição de senha, identificando falhas de usabilidade, segurança e consistência nas validações.

🔍 HEURÍSTICAS RECOMENDADAS PARA ESTA SESSÃO
- Heurística principal: Fronteira — limites de senha (7, 8, 255, 256 caracteres)
- Heurísticas de apoio: Estado (link expirado), Abordagem Contrária (e-mails inválidos, reuso de link)

🔎 ÁREAS DE INVESTIGAÇÃO
- Visibilidade e acesso ao link "Esqueci minha senha" em diferentes estados (login, mobile, sessão expirada)
- Comportamento com e-mails válidos, inválidos e não cadastrados
- Validação dos requisitos da nova senha (8+ chars, número, especial)
- Experiência com link expirado (após 30 min) e reuso do link
- Feedback visual em cada etapa (sucesso, erro, carregamento)

🧩 RECURSOS E DADOS
- Conta de e-mail para teste (acesso ao inbox)
- Cronômetro para validar expiração do link
- Navegador e dispositivo mobile

🚫 FORA DO ESCOPO
- Autenticação por provedor externo (Google/Apple)
- Alteração de senha com usuário já logado

⏱️ TIMEBOX: 45 min

---
📊 TASK BREAKDOWN (TBS) — Preencher após a sessão
- Test Design & Execution: ___%
- Bug Investigation & Reporting: ___%
- Session Setup: ___%
- Charter vs Opportunity: ___% / ___%

📝 NOTAS DA SESSÃO
- (I)
- (R)

🐞 DEFEITOS ENCONTRADOS
- [Descrição do bug]

❓ ISSUES / PERGUNTAS
- [Dúvidas sobre o comportamento esperado]

🔄 DEBRIEFING PROOF (pós-sessão)
- Past: O que aconteceu?
- Results: O que foi alcançado?
- Obstacles: O que atrapalhou?
- Outlook: O que ainda precisa ser feito?
- Feelings: Como você se sente sobre a qualidade?
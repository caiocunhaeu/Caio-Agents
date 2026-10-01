---
name: agent-architect
description: Use sempre que o pedido for desenhar, criar, planejar ou estruturar um agente de IA, subagente, orquestrador ou sistema multiagente — inclusive pedidos genéricos como "crie um agente para X", "monte um subagente que faça Y", "preciso automatizar isso com IA", "como estruturo um orquestrador", "isso devia ser um time de agentes?". Não aciona para simplesmente usar um agente/skill já existente.
---

# Agent Architect

Framework operacional para construir qualquer agente, subagente ou orquestrador de forma consistente, em vez de decidir a estrutura de improviso a cada pedido. É a "regra mor" deste repositório: todo agente novo criado aqui passa por este fluxo antes de qualquer linha de instrução ser escrita.

## Distinção central

**Agente** — sistema principal que fala com o usuário final, recebe o objetivo macro, planeja e usa ferramentas com autonomia.
**Subagente** — agente menor, especialista em uma única tarefa técnica, acionado por um agente principal ou orquestrador. Não fala direto com o usuário, devolve resultado pronto.
**Orquestrador** — agente que administra outros agentes: decide quem faz o quê e em que ordem, valida o resultado, manda refazer se estiver ruim antes de seguir adiante.

## As quatro peças de qualquer agente

1. **Cérebro** — o modelo (aqui, Claude). Só decide e pede; não executa nada sozinho.
2. **Ferramentas** — ações reais no mundo. Cada uma tem uma descrição (o que o cérebro lê para saber quando usar) e uma execução (o que roda de fato). Use só ferramentas que existem de verdade nesta sessão — nunca invente uma.
3. **Instruções** — o manual do agente: quem ele é, como pensa, o que pode e não pode fazer, o que conta como sucesso, o que nunca deve fazer. Neste repositório isso é o `SKILL.md`.
4. **Memória** — o que o agente lembra entre execuções. Formatos: arquivo `.md` simples (preferências, estado em andamento), banco relacional (consulta estruturada), banco vetorial/RAG (busca por similaridade). Neste repositório, memória de referência vive em `references/*.md` dentro da pasta da skill; a maioria dos agentes aqui não precisa de memória persistente além disso.

## Escada de complexidade — escolha o nível mais baixo que resolve o problema

| Nível | O que é | Use quando | Risco principal |
|---|---|---|---|
| 1 — Loop único | Um agente, uma lista de ferramentas, loop pergunta-resposta | Tarefa curta e bem definida | Estoura janela de contexto em tarefa longa |
| 2 — Linha sequencial | Vários agentes em sequência fixa (pesquisa → escreve → revisa) | Responsabilidades claras e separáveis | Erro cumulativo: se o passo 1 falha, ninguém volta atrás |
| 3 — Orquestração centralizada | Um gerente divide, aciona especialistas, valida, manda refazer | Problema aberto e ambíguo | Monocultura de validação se orquestrador e especialista usam o mesmo modelo |
| 4 — Grafo de estado cíclico | Máquina de estados em código, loops deliberados, checkpoints, pausa para aprovação humana | Fluxo crítico, longo, que precisa retomar de onde parou | Curva de aprendizado e sobre-engenharia em tarefa simples |

Só suba de nível quando o nível atual falhar de um jeito específico e observado (contexto estourando, erro se propagando sem correção, decisão ambígua demais para regra fixa) — nunca por precaução.

## Economia de contexto quando há orquestração

Cada novo passo relê todo o histórico acumulado: o custo cresce de forma aproximadamente quadrática com o número de passos, não linear. Três táticas contêm isso:

- **Isolamento de contexto** — o subagente consome o material pesado (páginas, arquivos, dados brutos) na própria sessão isolada e devolve só o essencial ao orquestrador, nunca o histórico inteiro. É o que a ferramenta `Agent` já faz nativamente aqui: o subagente roda isolado e só o resumo final volta para a conversa principal.
- **Exposição seletiva de ferramentas** — não carregue a descrição de todas as ferramentas do sistema a cada passo, só as poucas relevantes para aquele passo.
- **Prefix caching** — mantenha a parte estática do prompt (instruções, definição de ferramentas) sempre no início e só varie o conteúdo dinâmico no fim, para aproveitar cache de prompt do provedor.

## Rodando fora de uma conversa (agendado, por evento, 24/7)

Neste ambiente Claude Code já existe o mecanismo nativo — use-o antes de cogitar infraestrutura própria (VPS, serverless):

- Horário fixo ou recorrente → Routine agendada (`create_trigger` com `cron_expression`, ou `ScheduleWakeup` dentro de uma sessão já em andamento).
- Disparo único no futuro → `send_later` ou `create_trigger` com `run_once_at`.
- Evento externo (PR, webhook) → `subscribe_pr_activity` para GitHub, `watch_url` para webhook genérico.

Só recomende infraestrutura própria (VPS/serverless) se o agente precisar existir fora do ecossistema Claude Code por completo.

## As 9 etapas antes de construir qualquer agente ou subagente novo

1. **Propósito e escopo** — que problema ele resolve, especificamente, não em geral.
2. **Modelo** — qual Claude, e por quê (custo, janela de contexto, exigência da tarefa).
3. **Ferramentas e integrações** — quais, reais e disponíveis nesta sessão.
4. **Memória** — arquivo simples, banco relacional, banco vetorial, ou nenhuma.
5. **Padrão de trabalho** — sozinho ou com outros agentes; como decide que terminou; como lida com erro (admite que não sabe ou busca alternativa).
6. **Audiência** — só você usa, ou outras pessoas/sistemas também.
7. **Onde construir** — neste repositório, sempre como skill em `.claude/skills/<nome>/SKILL.md`, a menos que o pedido peça outra plataforma explicitamente.
8. **Instruções e memória** — escrever o `SKILL.md` (curto, gatilhos claros na `description`) e as `references/*.md` (detalhe carregado sob demanda, não inline).
9. **Testar** — rodar frases de gatilho reais mentalmente contra a `description`; conferir que as ferramentas citadas existem de fato.

## Nota de confiança

O artigo-fonte cita um estudo da ETH Zurich (AGENTS.md gerado por IA reduziria o sucesso em até 3% e elevaria o custo em mais de 20%; versão curta escrita por humano aumentaria o sucesso em até 4%) sem link nem referência direta ao paper — é uma claim de fonte única, não verificada por mim, e deve ser tratada com confiança baixa. A direção da recomendação (instrução curta, revisada por humano, abaixo de 200 linhas) é consistente com o princípio geral de degradação de contexto por excesso de instrução e vale seguir independentemente do número exato.

---
Fonte: framework adaptado do artigo "Como fazer um agente de IA" (Júlia Perissé, Substack), ajustado às ferramentas e mecanismos reais deste ambiente Claude Code.

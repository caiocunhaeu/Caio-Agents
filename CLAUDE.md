# CLAUDE.md

Regra mor deste repositório. `caio-agents` é a casa dos agentes e skills que Caio constrói para Claude Code focados na própria marca pessoal: construção e melhoria de marca, criação de conteúdo, voz e presença nos canais próprios. Trabalho ligado ao Furla vive em repositório separado, não aqui. Todo agente, subagente ou skill novo criado aqui segue o framework em `.claude/skills/agent-architect/SKILL.md` — carregue essa skill antes de desenhar um agente novo. Este arquivo carrega só as regras específicas deste repositório; o raciocínio profundo fica na skill, carregada sob demanda, para não inchar a memória sempre carregada.

## Domínio

Os agentes daqui giram em torno de conteúdo, marca pessoal e carreira de Caio: ideação e captura de ideias, escrita aplicando a voz própria dele, repurposing de conteúdo longo em formatos derivados por canal, acompanhamento de calendário editorial, e apoio a candidatura de vaga (adaptação de currículo para uma vaga específica, sempre fornecida manualmente por Caio, nunca busca ou scraping automatizado de portal de emprego). Nenhuma skill aqui deve carregar contexto, tom ou convenção específica da Furla; isso pertence ao repositório dela.

## Comandos

Não há build nem teste automatizado — os agentes deste repositório são arquivos Markdown (skills). Antes de entregar uma skill nova, valide manualmente: front matter YAML válido com `name` e `description`; `description` com gatilhos em linguagem natural reconhecíveis; arquivo principal (`SKILL.md`) abaixo de ~200 linhas, com detalhe pesado movido para `references/`.

## Arquitetura e convenções

Cada agente vive em `.claude/skills/<nome-em-kebab-case>/SKILL.md`. Material de referência extenso vai em `.claude/skills/<nome>/references/*.md`, nunca inline no `SKILL.md`. Neste repositório: "agente" = uma skill do Claude Code; "subagente" = uma chamada da ferramenta `Agent` com `subagent_type`, isolada da conversa principal; "orquestrador" = o próprio Claude Code decidindo qual skill/subagente acionar. Não existe `manager.py` separado aqui — o Claude Code cumpre esse papel nativamente.

## Diretrizes de "teste"

Antes de entregar uma skill nova: teste mentalmente 2-3 frases de gatilho reais contra a `description`; confirme que toda ferramenta citada existe de fato nesta sessão (nunca invente ferramenta); confirme que existe uma seção "nunca fazer" sempre que o domínio tiver modos de falha conhecidos.

## Estilo

Conteúdo em português. Sem travessão em-dash em nenhum arquivo. Nome de pasta em kebab-case igual ao campo `name` da skill. Arquivos de referência nomeados pelo conteúdo, nunca `part1.md`/`parte2.md`.

## Fluxo de git

Repositório de uso individual: commits vão direto para `main` enquanto não houver necessidade de revisão por terceiros. Mensagem de commit descreve o porquê, não só o quê. Cada skill nova é seu próprio commit.

## Limites estritos

Nunca apresente estatística não verificada (achada em uma única fonte secundária) como fato estabelecido dentro de uma skill sem sinalizar a confiança. Nunca construa um agente novo sem antes declarar propósito e escopo (etapa 1 do checklist em `agent-architect`). Nunca hardcode segredo ou chave de API em nenhum arquivo aqui. Nunca publique um rascunho de conteúdo pessoal como se fosse aprovado sem revisão do Caio.

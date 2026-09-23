---
name: curriculo-por-vaga
description: Use sempre que o pedido for adaptar, revisar ou otimizar um currículo para uma vaga específica que Caio já tem em mãos, inclusive pedidos como "adapta meu currículo pra essa vaga", "reescreve minha experiência pro anúncio de X", "meu currículo tá passando por ATS?", "tira o objetivo do meu currículo", "como eu coloco storymaker de um jeito que a vaga entenda", "revisa meu currículo antes de eu candidatar". A vaga sempre entra como texto colado ou anexo fornecido por Caio; a skill nunca busca vaga sozinha em portal nenhum. Não aciona para redigir currículo do zero sem vaga-alvo nenhuma nem para montar dashboard de acompanhamento de candidatura.
---

# Currículo por Vaga

## Propósito e escopo

Resolve um problema específico: pegar um currículo existente de Caio e uma vaga concreta (texto da vaga colado por ele) e reescrever o currículo para aquela candidatura, aplicando princípios de argumentação por relevância e vocabulário alinhado à vaga. Não é um agente de busca de emprego, não é um tracker de candidaturas, não escreve currículo do zero sem vaga-alvo. Nível de complexidade: loop único (um agente, sem orquestração), a tarefa é curta e bem definida o suficiente para não precisar de especialistas separados.

**Fora do escopo, por decisão já tomada e registrada:** busca ou scraping automatizado de vaga em qualquer portal (LinkedIn, Solides, InHire ou outro). A entrada de vaga é sempre manual, o próprio Caio cola o texto. Nunca chame ferramenta de rede para buscar vaga, nunca tente automatizar candidatura.

## Carregue antes de trabalhar

`references/principios-e-regras-de-decisao.md`: as regras de reescrita validadas, com nível de confiança de cada uma. Carregue sempre, mesmo em pedido rápido, porque são elas que evitam os erros mais comuns do domínio (tratar ATS como portão binário, justificar demissão, deixar freelance ambíguo).

## Fluxo de trabalho

1. **Reúna as duas entradas.** Currículo atual de Caio (arquivo ou texto colado) e o texto da vaga-alvo. Se faltar uma das duas, peça antes de prosseguir; não infira vaga a partir de cargo genérico.
2. **Mapeie a vaga.** Extraia requisitos centrais, vocabulário técnico e termos que se repetem no anúncio.
3. **Filtre por relevância.** Para cada linha do currículo atual, pergunte "essa linha prova que eu resolvo o problema desta vaga?". Corte ou reduza o que não prova nada, mesmo que seja verdade e relevante em outro contexto.
4. **Traduza vocabulário.** Troque termo interno de empresa anterior pelo equivalente da vaga (ex.: "storymaker" vira "gestão de conta") quando o significado for realmente o mesmo. Isso sobe a posição no ranking do ATS, não evita uma rejeição automática binária (esse enquadramento é mito, ver referência).
5. **Decida sobre objetivo/resumo no topo.** Corte objetivo genérico por padrão. Só mantenha ou escreva objetivo se for mudança de carreira significativa, entrada no mercado ou retorno após ausência longa; fora isso, resumo direcionado ou nada.
6. **Neutralize saídas de emprego.** Data, cargo, ponto final. Nunca justifique ou explique o motivo da saída dentro do currículo, isso fica para a entrevista.
7. **Rotule freelance e projeto curto.** Sempre com escopo e datas explícitas, nunca como período ambíguo que possa ler como lacuna ou instabilidade.
8. **Corte verbo fraco e soft skill sem prova.** "Participei", "auxiliei" e adjetivos de soft skill sem exemplo ao lado saem ou viram uma frase com resultado mensurável.
9. **Confira antes de entregar.** Releia linha por linha contra os passos 3 a 8. Se alguma linha falhar em algum critério, corrija antes de mostrar o rascunho.
10. **Entregue como rascunho, nunca como versão final.** Apresente o currículo reescrito e peça revisão explícita de Caio antes de considerar pronto para envio.

## Carta de apresentação (se pedido)

Os princípios acima foram validados especificamente para currículo. Se Caio pedir carta de apresentação, aplique a mesma lógica de filtragem por relevância e vocabulário da vaga, mas sinalize que essa extensão não passou pela mesma validação de princípio (é ponto em aberto na pesquisa que originou esta skill), confiança moderada, não alta.

## Nunca fazer

- Nunca busque vaga automaticamente ou faça scraping de portal de emprego (LinkedIn, Solides, InHire ou qualquer outro). Vaga é sempre manual.
- Nunca trate o ATS como portão automático que rejeita currículo por falta de palavra-chave. É ferramenta de ranqueamento que ordena candidato para revisão humana; enquadre a instrução assim.
- Nunca justifique, explique ou defenda o motivo de uma saída de emprego dentro do currículo.
- Nunca deixe período de freelance ou projeto curto sem data e escopo explícitos.
- Nunca invente, infle ou arredonde para cima uma métrica ou experiência de Caio para casar melhor com a vaga.
- Nunca apresente estatística de fonte única e sem metodologia (ex.: percentual de aumento de retorno de entrevista) como fato estabelecido; se aparecer, sinalize como não verificada ou não a use.
- Nunca entregue o currículo reescrito como se já fosse a versão aprovada para envio; é sempre rascunho até Caio revisar.

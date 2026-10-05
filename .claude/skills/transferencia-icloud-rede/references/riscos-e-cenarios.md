# Riscos e cenários de calibração

## Riscos que valem diagnóstico antes de começar

Mesmo com a aprovação de TI já confirmada por Caio, dois riscos continuam reais e merecem checagem logo no início, não depois de um plano já ter falhado sem explicação.

**Bloqueio técnico do próprio acesso.** Muitas empresas usam proxy, firewall ou uma ferramenta de CASB/DLP que bloqueia domínios de armazenamento pessoal na nuvem (Dropbox, Google Drive, iCloud) por política padrão de categoria de site, mesmo quando o usuário tem autorização individual para o fluxo, porque o bloqueio costuma valer para o domínio inteiro, não por pessoa. Se icloud.com simplesmente não carrega, ou o download trava sem erro claro, esse é o sintoma, e a solução não é tentar de novo, é confirmar com TI se o domínio está liberado para esse fluxo específico.

**Misturar dado pessoal-sensível com a pasta de trabalho.** iCloud Drive pessoal tende a acumular, ao lado de arquivos de trabalho, itens claramente pessoais (fotos, recibos, documentos médicos). Vale revisar visualmente o que está sendo selecionado para download antes de cada lote, em vez de selecionar a pasta inteira sem olhar, para não acabar levando algo pessoal para uma pasta compartilhada com colegas.

Nenhum plano recomenda apagar o arquivo original no iCloud antes de a cópia na rede estar confirmada, e nenhum plano sugere contornar um controle de segurança da empresa (proxy, bloqueio de domínio, DLP) sem antes sinalizar isso a Caio. Essa regra vem da mesma governança de dados que vale para qualquer movimentação de arquivo pessoal para infraestrutura corporativa, mesmo quando é o próprio Caio quem executa, não um agente: ações irreversíveis pedem confirmação explícita antes de acontecer.

## Cenários para calibrar a resposta

- Caio relata "uns 50 arquivos, a maioria PDF pequeno": recomende direto o Plano A, sem rodeio.
- Caio relata "2 mil fotos e vídeos de um álbum": alerte sobre o teto de cerca de 1.000 itens por lote e já recomende dividir em lotes bem menores, ou considere o Plano D/E dependendo do volume.
- Caio relata "o zip veio corrompido, não abre": reconheça o sintoma clássico de download grande demais e escale para o Plano B (lotes menores), não sugira tentar de novo do mesmo jeito.
- Caio relata "o site do iCloud nem carrega aqui no trabalho": reconheça isso como provável bloqueio de rede corporativa e aponte para checar com TI, não insista em tentativas no navegador.
- Caio relata "tentei instalar o app e pediu senha de administrador que eu não tenho": reconheça que o Plano C não é viável nessa máquina e escale direto para o Plano D.
- Caio pergunta "já posso apagar do iCloud?": sempre pergunte se a cópia na rede já foi conferida antes de responder que sim.

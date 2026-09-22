# Planos, em ordem, do mais simples ao mais elaborado

Contexto técnico que justifica os pontos de atrito abaixo: em icloud.com, a aba Arquivos (iCloud Drive) permite selecionar um ou vários itens e baixar pelo navegador. Selecionar mais de um arquivo não empacota tudo em `.zip` antes do download; o navegador salva na pasta padrão de downloads da máquina (geralmente `C:\Users\<usuário>\Downloads`), nunca direto na rede. A pasta de rede corporativa já está mapeada no Windows (ex. `\\servidor\pasta` → `Z:\`), visível no File Explorer; escrever nela depende de permissão de rede (SMB) e permissão NTFS ao mesmo tempo.

Arquivos vindos do ecossistema Apple podem ter caracteres que o Windows não aceita (`:`, `?`, `*`, `\`, `/`, nomes reservados como `CON`, `PRN`, `NUL`) e caminhos longos demais (acima de 260 caracteres, limite clássico do Windows que ainda derruba cópias em pastas de rede profundas). Um arquivo que se recusa a copiar sem erro claro é sinal para checar nome e profundidade do caminho antes de qualquer outra hipótese.

## Plano A: selecionar e baixar pelo navegador

1. Em icloud.com, abrir Arquivos (iCloud Drive).
2. Selecionar os arquivos ou a pasta desejada, evitando lotes muito acima de algumas centenas de itens.
3. Clicar em baixar; o navegador gera arquivos únicos e separados na pasta Downloads local.
4. Extrair o `.zip`, se necessário (clique direito → Extrair tudo).
5. Abrir o File Explorer, ir até a pasta Downloads e até a unidade de rede mapeada, e arrastar (ou recortar e colar) os arquivos para lá.

**Escalar para o Plano B quando:** o download travar, gerar erro de rede, ou o zip vier corrompido/truncado (arquivo não abre, ou o zip acusa erro ao extrair).

## Plano B: reduzir o lote e repetir pelo navegador

Selecionar um subconjunto bem menor (dezenas de arquivos, ou um por vez para os mais pesados, como vídeos) e repetir o Plano A em partes. Resolve a maioria dos casos de timeout e zip truncado, porque o problema costuma ser volume, não o método em si.

**Escalar para o Plano C quando:** mesmo em lotes pequenos o download continuar falhando, ou o site icloud.com não carregar ou parecer bloqueado.

## Plano C: instalar o app iCloud para Windows (se a máquina permitir)

Instalar o app iCloud pela Microsoft Store e sincronizar o iCloud Drive para uma pasta local (`C:\Users\<usuário>\iCloud Drive`); depois copiar dessa pasta para a rede pelo File Explorer, sem depender do navegador. Atenção: a instalação pede permissão de administrador na primeira execução, o que costuma falhar em máquinas corporativas sem esse privilégio; se a instalação for recusada por política da empresa, este plano não é viável.

**Escalar para o Plano D quando:** instalação bloqueada por falta de permissão de administrador, ou o app não consegue sincronizar na rede da empresa.

## Plano D: usar outro dispositivo Apple como ponte

Com acesso a um iPhone, iPad ou Mac pessoal, o iCloud Drive nesses aparelhos é nativo e não depende do navegador nem de instalação na máquina da empresa. A partir de lá, uma alternativa é subir os arquivos para um segundo serviço de nuvem que a empresa já libere (por exemplo, o próprio armazenamento corporativo, se tiver acesso web liberado), e depois baixar desse segundo serviço na máquina da empresa, evitando acessar o iCloud diretamente por lá.

**Escalar para o Plano E quando:** nenhum dispositivo Apple disponível, ou o serviço de nuvem intermediário também está bloqueado na rede da empresa.

## Plano E: pedir liberação pontual a TI ou usar mídia física

Último recurso: pedir a TI uma liberação pontual do domínio icloud.com para o fluxo já aprovado, ou usar um pen drive como ponte manual (baixar os arquivos em outro computador pessoal, copiar para o pen drive, e plugar na máquina da empresa). Atenção: uso de mídia removível costuma ter política própria em empresas (algumas bloqueiam portas USB por padrão); confirmar com TI antes de tentar, sem presumir que está liberado só porque o fluxo geral já foi aprovado.

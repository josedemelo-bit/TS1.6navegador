# Tactical Strike — FPS tático para navegador

Protótipo original em primeira pessoa com cenário 3D, mira, rifle, disparos, recarga, HUD, colisões simples, bots e sincronização multiplayer básica via Socket.IO.

## Requisitos
- Node.js 18 ou mais recente
- Navegador atualizado com suporte a WebGL
- Conexão à internet para carregar Three.js pelo CDN (as músicas são locais)

## Executar no PC
1. Extraia o ZIP.
2. Abra um terminal dentro da pasta `tactical_strike_web`.
3. Instale as dependências: `npm install`
4. Inicie o servidor: `npm start`
5. Abra `http://localhost:3000` no navegador.
6. Clique em **TREINO COM BOTS** para jogar offline, ou **SALA ONLINE** para testar a conexão multiplayer.

O servidor serve o jogo a partir da pasta `public/`.

## Música local
Os seis MP3 estão em `public/audio/`. Não são enviados pelo Socket.IO: cada navegador toca os arquivos localmente.

- **Menu:** Devil In A New Dress, That's What I Like, Shabang.
- **Partida:** POWER, 24K Magic, Smells Like Teen Spirit.

A playlist de cada modo toca em sequência e repete. Ao iniciar a partida, a música muda para a playlist de gameplay; ao clicar em **MENU**, retorna à playlist do menu. A troca entre faixas usa uma transição curta entre dois reprodutores de áudio, sem reiniciar a faixa em cada atualização do jogo. Os controles de música e volume estão no menu e no HUD.

Navegadores modernos podem bloquear áudio antes de uma interação do usuário. Por isso, a reprodução é desbloqueada no primeiro clique/toque. Se não ouvir música, clique uma vez na página e confira se o controle está em **MÚSICA: LIGADA** e se o volume está acima de zero.

## Colocar online para jogar com amigos
1. Publique a pasta do projeto em um host que aceite Node.js e WebSockets (por exemplo, um VPS ou serviço de hospedagem Node).
2. Configure a porta conforme a variável de ambiente `PORT`.
3. No jogo, preencha o endereço público do servidor e clique em **SALA ONLINE**.
4. Todos os jogadores precisam usar o mesmo endereço público.

## Controles
- `W A S D`: movimentação
- `Mouse`: mirar
- `Clique esquerdo`: disparar
- `Shift`: correr
- `R`: recarregar
- `Esc`: liberar o cursor
- Botão **MENU** no HUD: voltar ao menu

## Limitações honestas deste protótipo
- O visual 3D é um ponto de partida, não equivale ao nível de produção de Counter-Strike 2.
- O multiplayer sincroniza posições e mensagens de disparo em uma implementação inicial; não sincroniza ainda dano, munição, bots ou placar entre clientes.
- Para um jogo competitivo real, ainda seriam necessários movimento e combate autoritativos no servidor, interpolação, validação anticheat, salas, equipes, objetivos, sons, animações, modelos/texturas próprios, testes de rede e segurança.
- O mapa e os personagens usam formas 3D simples e materiais procedurais.
- O jogo usa Three.js pelo CDN; é necessária internet para carregar a biblioteca.

## Estrutura
- `public/index.html`: jogo 3D e controle de música
- `public/audio/`: seis arquivos MP3 locais
- `server.js`: servidor HTTP + Socket.IO
- `package.json`: dependências e comando de inicialização

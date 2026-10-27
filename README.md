# Tactical Strike — FPS tático para navegador

Protótipo original em primeira pessoa com cenário 3D, mira, rifle, disparos, recarga, HUD, colisões simples, bots e sincronização multiplayer básica via Socket.IO.

## Requisitos
- Node.js 18 ou mais recente
- Navegador atualizado com suporte a WebGL
- Conexão à internet para carregar Three.js pelo CDN (as músicas, se houver, são locais)

## Executar no PC
1. Extraia o ZIP.
2. Abra um terminal dentro da pasta `tactical_strike_web`.
3. Instale as dependências: `npm install`
4. Inicie o servidor: `npm start`
5. Abra `http://localhost:3000` no navegador.
6. Clique em **TREINO COM BOTS** para jogar offline, ou **SALA ONLINE** para testar a conexão multiplayer.

O servidor serve o jogo a partir da pasta `public/`.

## Música local
O jogo toca música a partir de arquivos MP3 na pasta `public/audio/`. **Os MP3 não estão incluídos neste repositório** (músicas comerciais têm direitos autorais), então você precisa colocar os seus. O jogo funciona normalmente sem eles, só fica sem trilha.

Nomes de arquivo esperados (editáveis na lista `musicTracks` em `public/index.html`):

- **Menu:** `devil-in-a-new-dress.mp3`, `thats-what-i-like.mp3`, `shabang.mp3`
- **Partida:** `power.mp3`, `24k-magic.mp3`, `smells-like-teen-spirit.mp3`

Para usar outras músicas, copie seus MP3 para `public/audio/` e ajuste os `title` e `src` em `musicTracks`. Músicas livres de direitos (Creative Commons, domínio público ou compradas com licença) são a melhor escolha se você for publicar o jogo online.

A playlist de cada modo toca em sequência e repete. Ao iniciar a partida, a música muda para a playlist de gameplay; ao clicar em **MENU**, volta para a do menu. A troca entre faixas usa uma transição curta entre dois reprodutores. Se um arquivo estiver faltando, o jogo pula para o próximo. Os controles de música e volume ficam no menu e no HUD.

Navegadores bloqueiam áudio antes de uma interação do usuário. Por isso a reprodução é desbloqueada no primeiro clique, toque ou tecla. Se não ouvir nada, clique uma vez na página e confira se está em **MÚSICA: LIGADA** e com volume acima de zero.

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
- `public/audio/`: coloque aqui seus MP3 (ignorados pelo Git)
- `server.js`: servidor HTTP + Socket.IO
- `package.json`: dependências e comando de inicialização

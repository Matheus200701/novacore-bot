# NovaCore Bot

Bot Discord profissional, modular e escalável feito em Python 3.11+ com `discord.py 2.x`, slash commands, Cogs, SQLite, embeds, botões interativos, tickets, moderação, AutoMod, logs, XP, economia, sorteios e música.

> O projeto é original. Ele é inspirado em funcionalidades comuns de bots grandes, mas não copia marca, nome, textos internos, identidade visual ou código de outros bots.

## Recursos principais

- Slash commands em português e sem acentos nos nomes.
- Sistema modular com Cogs.
- SQLite assíncrono com `aiosqlite`.
- `.env` para token e configurações.
- Tratamento global de erros.
- Embeds profissionais.
- Tickets com botão persistente.
- AutoMod com bloqueio de links, palavras proibidas e caps lock excessivo.
- Logs de mensagens, membros, canais e punições.
- Sistema de XP com cooldown anti-farm e recompensas por nível.
- Economia com daily, trabalho, apostas, loja e inventário.
- Música com `yt-dlp`, FFmpeg e suporte de voz do `discord.py`.
- Preparado para PC, Termux e Discloud.

## Estrutura

```text
bot/
├── main.py
├── config.py
├── requirements.txt
├── .env.example
├── README.md
├── discloud.config
├── database/
│   └── database.py
├── utils/
│   ├── embeds.py
│   ├── checks.py
│   └── time.py
└── cogs/
    ├── moderacao.py
    ├── configuracao.py
    ├── automod.py
    ├── logs.py
    ├── tickets.py
    ├── boas_vindas.py
    ├── niveis.py
    ├── economia.py
    ├── utilidade.py
    ├── diversao.py
    ├── sorteios.py
    ├── musica.py
    └── ajuda.py
```

## Como criar o bot no Discord Developer Portal

1. Acesse o Discord Developer Portal.
2. Crie uma aplicação.
3. Vá em **Bot** e clique em **Add Bot**.
4. Copie o token do bot.
5. Ative estas intents em **Privileged Gateway Intents**:
   - Server Members Intent
   - Message Content Intent
6. Em **OAuth2 > URL Generator**, selecione:
   - `bot`
   - `applications.commands`
7. Permissões recomendadas para começar:
   - Administrator, ou configure manualmente permissões de moderação, canais, cargos, mensagens, voz e embeds.
8. Convide o bot pelo link gerado.

## Instalação no PC

```bash
cd bot
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/macOS
source venv/bin/activate

pip install -U pip
pip install -r requirements.txt
copy .env.example .env  # Windows
# cp .env.example .env  # Linux/macOS
```

Edite o arquivo `.env`:

```env
DISCORD_TOKEN=SEU_TOKEN_REAL_AQUI
OWNER_ID=SEU_ID_DO_DISCORD
SYNC_GUILD_ID=0
DATABASE_PATH=data/novacore.sqlite3
```

Rodar:

```bash
python main.py
```

## Instalação no Termux

```bash
pkg update && pkg upgrade -y
pkg install python ffmpeg -y
cd bot
python -m venv venv
source venv/bin/activate
pip install -U pip
pip install -r requirements.txt
cp .env.example .env
nano .env
python main.py
```

Observação: em alguns celulares, bibliotecas de voz podem exigir dependências extras. Se o módulo `PyNaCl` falhar, instale/atualize com:

```bash
pip install -U PyNaCl "discord.py[voice]"
```

## Hospedagem na Discloud

1. Deixe o arquivo `discloud.config` na raiz do projeto.
2. Configure a variável `DISCORD_TOKEN` no painel da Discloud, ou envie um `.env` privado.
3. Garanta que o plano/ambiente tenha FFmpeg. O arquivo `discloud.config` inclui `APT=ffmpeg`.
4. Envie o projeto para a Discloud.

## Comandos principais

### Moderação

`/banir`, `/desbanir`, `/expulsar`, `/castigar`, `/remover_castigo`, `/avisar`, `/avisos`, `/remover_aviso`, `/limpar`, `/trancar`, `/destrancar`, `/modo_lento`, `/nick`, `/cargo_adicionar`, `/cargo_remover`, `/anunciar`, `/falar`

### Configuração

`/config_logs`, `/config_boasvindas`, `/config_saida`, `/config_autocargo`, `/config_ticket`, `/config_automod`, `/config_xp`, `/config_economia`, `/config_ver`

### Tickets

`/painel_ticket`, `/fechar_ticket`, `/adicionar_ticket`, `/remover_ticket`, `/renomear_ticket`

### XP e níveis

`/rank`, `/ranking`, `/xp_adicionar`, `/xp_remover`, `/nivel_definir`, `/recompensa_nivel`, `/recompensas`

### Economia

`/saldo`, `/daily`, `/trabalhar`, `/apostar`, `/transferir`, `/loja`, `/loja_adicionar`, `/loja_remover`, `/comprar`, `/inventario`, `/ranking_moedas`, `/moedas_adicionar`, `/moedas_remover`

### Utilidade

`/ping`, `/usuario`, `/servidor`, `/avatar`, `/banner`, `/botinfo`, `/canal`, `/cargo`, `/emoji`, `/convite`, `/calcular`, `/enquete`, `/lembrete`

### Diversão

`/dado`, `/moeda`, `/bola8`, `/escolher`, `/ship`, `/abracar`, `/tapa`, `/beijar`, `/piada`, `/meme_texto`, `/ascii`, `/ppt`

### Sorteios

`/sorteio_criar`, `/sorteio_rapido`

### Música

`/entrar_voz`, `/sair_voz`, `/tocar`, `/pausar_musica`, `/continuar_musica`, `/parar_musica`, `/pular_musica`, `/fila_musica`, `/volume_musica`

### Ajuda

`/ajuda`, `/comandos`

## Segurança aplicada

- Token nunca fica no código.
- Comandos administrativos verificam permissões.
- Moderação bloqueia ação contra si mesmo.
- Moderação bloqueia membros com cargo maior ou igual.
- Bot também valida a própria hierarquia antes de moderar.
- Dados persistidos são apenas IDs públicos do Discord e configurações do servidor.

## Observações sobre música

Para música funcionar, o ambiente precisa ter:

- FFmpeg instalado e acessível no PATH.
- `PyNaCl` instalado.
- `yt-dlp` atualizado.

Se músicas não carregarem, atualize:

```bash
pip install -U yt-dlp
```

## Solução de problemas

### `DISCORD_TOKEN não encontrado`

Você não criou o `.env` ou não colocou o token real.

### Comandos slash não aparecem

- Confira se o bot foi convidado com `applications.commands`.
- Use `SYNC_GUILD_ID` com o ID do seu servidor de testes para aparecer mais rápido.
- Comandos globais podem demorar para aparecer.

### `PyNaCl library needed in order to use voice`

Instale:

```bash
pip install -U "discord.py[voice]" PyNaCl
```

### `ffmpeg was not found`

Instale FFmpeg:

```bash
# Termux
pkg install ffmpeg

# Ubuntu/Debian
sudo apt install ffmpeg
```

No Windows, instale FFmpeg e coloque a pasta `bin` no PATH.

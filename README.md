<p align="center">
  <img src="assets/moltbot-migration.jpg" alt="ClawdBot ê¢â â MoltBot" width="100%">
</p>

# ê°Å¸Â¤â Docker Moltbot

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


<p align="center">
  <img src="assets/moltbot-robot.jpg" alt="MoltBot" width="400">
</p>

[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Node.js](https://img.shields.io/badge/Node.js-22-339933?logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Security Hardened](https://img.shields.io/badge/Security-Hardened-green?logo=shieldsdotio)](SECURITY.md)
[![Docs](https://img.shields.io/badge/Docs-docs.molt.bot-blue)](https://docs.molt.bot)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/clawd)

Setup Docker para o [Moltbot](https://molt.bot) ê¢â¬â um assistente pessoal de IA com seguranêÂ§a reforêÂ§ada de fêÂ¡brica.

> **Moltbot** (antigo Clawdbot) êÂ© um assistente de IA que roda na sua prêÂ³pria mêÂ¡quina. Ele se conecta a LLMs (Claude, GPT, Gemini, etc.), tem ferramentas (busca na web, execuêÂ§êÂ£o de cêÂ³digo, gerenciamento de arquivos, controle de navegador) e conversa com vocêÂª via Telegram, WhatsApp, Discord, webchat e mais. Este repo te dêÂ¡ um setup Docker pronto pra rodar com boas prêÂ¡ticas de seguranêÂ§a jêÂ¡ configuradas.

> ê¢Å¡Â ê¯Â¸Â **Nota (Jan 2026):** O rebrand para Moltbot estêÂ¡ em andamento. O pacote npm `moltbot` êÂ© atualmente um shim de compatibilidade. Este setup Docker instala o `clawdbot` (o runtime completo) e vai trocar automaticamente para `moltbot` quando o pacote completo for publicado. NêÂ£o precisa fazer nada ê¢â¬â êÂ© sêÂ³ rebuildar quando uma nova versêÂ£o for anunciada.

---

## ê¢ÅÂ¨ Funcionalidades

- ê°Å¸ââ **SeguranêÂ§a reforêÂ§ada** ê¢â¬â segue o [Checklist Top 10 de SeguranêÂ§a](SECURITY.md)
- ê°Å¸ÂÂ³ **Setup em um comando** ê¢â¬â `docker compose up -d`
- ê°Å¸âÂ **Secrets via variêÂ¡veis de ambiente** ê¢â¬â sem credenciais em texto puro nos arquivos de config
- ê°Å¸âÂ¤ **Container nêÂ£o-root** ê¢â¬â roda como usuêÂ¡rio sem privilêÂ©gios `moltbot`
- ê°Å¸âÂ **Logging habilitado** ê¢â¬â trilha de auditoria por padrêÂ£o
- ê°Å¸âÂ± **Multi-canal** ê¢â¬â Telegram, WhatsApp, Discord, Slack, webchat e mais
- ê°Å¸Å½â¢ê¯Â¸Â **TranscriêÂ§êÂ£o de êÂ¡udio** ê¢â¬â Faster Whisper incluso (opcional)
- ê°Å¸âºÂ ê¯Â¸Â **Ferramentas integradas** ê¢â¬â acesso ao shell, busca na web, controle de navegador, execuêÂ§êÂ£o de cêÂ³digo
- ê°Å¸Â§Â  **200+ modelos via OpenRouter** ê¢â¬â Claude, GPT, Gemini, Llama, DeepSeek e mais com uma êÂºnica API key
- ê°Å¸ÂªÅ¸ **CompatêÂ­vel com Windows** ê¢â¬â `.gitattributes` forêÂ§a terminaêÂ§êÂµes LF, Dockerfile corrige CRLF
- ê°Å¸ââ **Auto-restart** ê¢â¬â polêÂ­tica de reinêÂ­cio `unless-stopped`
- ê°Å¸ÅÂ **Rede segura** ê¢â¬â gateway vinculado ao loopback, isolamento de rede Docker disponêÂ­vel

---

## ê°Å¸ââ¹ PrêÂ©-requisitos

| Plataforma | Requisito | InstalaêÂ§êÂ£o |
|------------|-----------|------------|
| **Windows** | Docker Desktop | [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) |
| **Windows** | Git | [git-scm.com](https://git-scm.com/download/win) |
| **Mac** | Docker Desktop | [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) |
| **Linux** | Docker Engine + Compose V2 | Ver instruêÂ§êÂµes abaixo |

---

## ê°Å¸ÂÂ³ InstalaêÂ§êÂ£o do Docker

### Windows

1. **Baixe o Docker Desktop:**
   - Acesse [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
   - Clique em "Download for Windows"

2. **Execute o instalador:**
   - Abra o arquivo `.exe` baixado
   - Aceite os termos e siga o wizard de instalaêÂ§êÂ£o
   - O instalador vai pedir para habilitar o **WSL 2** ê¢â¬â aceite

3. **Reinicie o computador** (se solicitado)

4. **Inicie o Docker Desktop:**
   - Abra pelo menu Iniciar
   - Espere atêÂ© aparecer "Docker is running" (êÂ­cone ê°Å¸ÂÂ³ na bandeja do sistema)

5. **Verifique a instalaêÂ§êÂ£o:**
   ```powershell
   docker --version
   docker compose version
   ```

> ê¢Å¡Â ê¯Â¸Â **WSL 2 nêÂ£o instalado?** Se o Docker Desktop pedir para instalar o WSL 2, siga as instruêÂ§êÂµes na tela. Isso êÂ© necessêÂ¡rio para rodar containers Linux no Windows.

> ê¢Å¡Â ê¯Â¸Â **Erro "WSL docker-desktop Stopped"?** Abra o Docker Desktop pelo menu Iniciar ê¢â¬â ele inicia o WSL automaticamente.

### Linux (Ubuntu/Debian)

O Docker Compose V2 jêÂ¡ vem integrado ao Docker Engine (comando `docker compose`, sem hêÂ­fen).

1. **Instale o Docker** (script oficial):
   ```bash
   curl -fsSL https://get.docker.com | sh
   ```

2. **Inicie o serviêÂ§o:**
   ```bash
   sudo systemctl start docker
   ```

3. **Habilite no boot:**
   ```bash
   sudo systemctl enable docker
   ```

4. **Verifique se estêÂ¡ rodando:**
   ```bash
   sudo systemctl status docker
   ```
   > Deve mostrar `Active: active (running)`. Pressione `q` para sair.

5. **Adicione seu usuêÂ¡rio ao grupo docker** (para rodar sem `sudo`):
   ```bash
   sudo usermod -aG docker $USER
   ```

6. **FaêÂ§a logout e login novamente** para aplicar a mudanêÂ§a

7. **Verifique a instalaêÂ§êÂ£o:**
   ```bash
   docker --version
   docker compose version
   docker ps  # Deve mostrar lista vazia (sem erro)
   ```

### Linux (Alternativa: via apt)

Se preferir usar o pacote do Ubuntu (pode ser versêÂ£o mais antiga):

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker  # Verificar se estêÂ¡ rodando
sudo usermod -aG docker $USER
# FaêÂ§a logout e login novamente
```

### Mac

1. **Baixe o Docker Desktop:**
   - Acesse [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
   - Escolha a versêÂ£o para seu chip (Intel ou Apple Silicon)

2. **Arraste para Applications** e abra o Docker Desktop

3. **Verifique a instalaêÂ§êÂ£o:**
   ```bash
   docker --version
   docker compose version
   ```

### Subindo o Container (Linux/Mac)

ApêÂ³s instalar o Docker, siga estes passos para colocar o Moltbot no ar:

1. **Clone o repositêÂ³rio:**
   ```bash
   git clone https://github.com/linnoff88-dev/docker-moltbot-open.git
   cd docker-moltbot-open
   ```

2. **Configure o arquivo `.env`:**
   ```bash
   cp .env.example .env
   nano .env  # ou use seu editor preferido
   ```

3. **Preencha as variêÂ¡veis obrigatêÂ³rias no `.env`:**
   ```env
   GATEWAY_AUTH_TOKEN=seu-token-seguro-aqui    # Gere com: openssl rand -hex 24
   OPENROUTER_API_KEY=sk-or-v1-sua-chave-aqui  # Obtenha em openrouter.ai/keys
   ```

4. **Configure canais de mensagem** (opcional):
   ```env
   # Telegram - crie um bot com @BotFather no Telegram
   TELEGRAM_BOT_TOKEN=123456:ABC-seu-token-do-botfather
   ```

5. **Suba o container:**
   ```bash
   docker compose up -d
   ```

6. **Verifique se estêÂ¡ rodando:**
   ```bash
   docker compose ps      # Status do container
   docker compose logs    # Ver logs (Ctrl+C para sair)
   ```

7. **Configure o WhatsApp** (opcional):
   ```bash
   docker exec -it moltbot clawdbot channels login whatsapp
   # Escaneie o QR code com seu celular
   ```

8. **Acesse o webchat:**
   ```
   http://localhost:18789/chat
   ```
   > Use o `GATEWAY_AUTH_TOKEN` que vocêÂª configurou no `.env` para autenticar.

> ê°Å¸âÂ¡ Veja as seêÂ§êÂµes [ConfiguraêÂ§êÂ£o do Telegram](#-configuraêÂ§êÂ£o-do-telegram) e [ConfiguraêÂ§êÂ£o do WhatsApp](#-configuraêÂ§êÂ£o-do-whatsapp) para instruêÂ§êÂµes detalhadas.

---

## ê°Å¸Å¡â¬ InêÂ­cio RêÂ¡pido

### Passo 1: Clone o repo

**Linux / Mac:**
```bash
git clone https://github.com/linnoff88-dev/docker-moltbot-open.git
cd docker-moltbot-open
```

**Windows (CMD):**
```cmd
git clone https://github.com/linnoff88-dev/docker-moltbot-open.git
cd docker-moltbot-open
```

**Windows (PowerShell):**
```powershell
git clone https://github.com/linnoff88-dev/docker-moltbot-open.git
cd docker-moltbot-open
```

### Passo 2: Configure o ambiente

**Linux / Mac:**
```bash
cp .env.example .env
nano .env  # Fill in your API keys
```

**Windows (CMD):**
```cmd
copy .env.example .env
notepad .env
```

**Windows (PowerShell):**
```powershell
Copy-Item .env.example .env
notepad .env
```

> ê¢Å¡Â ê¯Â¸Â **IMPORTANTE:** VocêÂª **PRECISA** criar E editar o arquivo `.env` antes de rodar `docker compose up`. O container nêÂ£o vai funcionar com os valores de exemplo.

Abra o arquivo `.env` e substitua os valores de exemplo pelas suas chaves reais:

```env
# ê¢ÂÅ ERRADO ê¢â¬â esses sêÂ£o placeholders, nêÂ£o vêÂ£o funcionar:
OPENROUTER_API_KEY=sk-or-your-key-here
GATEWAY_AUTH_TOKEN=your-secure-token-here

# ê¢Åâ¦ CERTO ê¢â¬â suas chaves reais:
OPENROUTER_API_KEY=sk-or-v1-abc123-your-actual-real-key
GATEWAY_AUTH_TOKEN=a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6
DEFAULT_MODEL=openrouter/anthropic/claude-sonnet-4.5
```

### Passo 3: Gere um token seguro para o gateway

O `GATEWAY_AUTH_TOKEN` protege a API do seu gateway contra acesso nêÂ£o autorizado. Gere um aleatêÂ³rio:

**Linux / Mac:**
```bash
openssl rand -hex 24
```

**Windows (PowerShell):**
```powershell
-join ((1..48) | ForEach-Object { '{0:x}' -f (Get-Random -Max 16) })
```

**Ou** use qualquer string aleatêÂ³ria longa (pelo menos 24 caracteres). VocêÂª pode usar um gerenciador de senhas para gerar uma.

Copie o token gerado para o seu arquivo `.env` como `GATEWAY_AUTH_TOKEN`.

### Passo 4: Configure sua chave OpenRouter

Este setup usa **OpenRouter** como gateway unificado de LLMs. Com uma êÂºnica API key, vocêÂª tem acesso a 200+ modelos:

| Categoria | Modelos DisponêÂ­veis |
|-----------|---------------------|
| **Claude** | Sonnet 4.5, Opus 4, Haiku 3.5, etc. |
| **GPT** | GPT-4o, GPT-4 Turbo, o1-preview, etc. |
| **Gemini** | Gemini 2.0 Flash (FREE), Pro, etc. |
| **Open Source** | Llama 3.3 70B (FREE), DeepSeek R1 (FREE), Qwen, etc. |
| **Especializados** | Mistral, Claude, Grok, e mais |

**Obtenha sua chave:**
1. Acesse [openrouter.ai](https://openrouter.ai/)
2. FaêÂ§a login com Google/GitHub
3. VêÂ¡ para [Keys](https://openrouter.ai/keys) e crie uma nova API key
4. Copie a key (comeêÂ§a com `sk-or-v1-...`)
5. Cole no seu `.env` como `OPENROUTER_API_KEY`

**Escolha seu modelo padrêÂ£o:**

Edite `DEFAULT_MODEL` no `.env` para escolher qual modelo usar.

ê¢Å¡Â ê¯Â¸Â **IMPORTANTE:** O formato correto êÂ© `openrouter/<provider>/<model>` (com o prefixo `openrouter/`)

```env
# OpêÂ§êÂ£o 1: Claude Sonnet 4.5 (melhor qualidade, recomendado) ê¢Â­Â
DEFAULT_MODEL=openrouter/anthropic/claude-sonnet-4.5

# OpêÂ§êÂ£o 2: Claude 3.5 Sonnet (êÂ³timo custo-benefêÂ­cio)
DEFAULT_MODEL=openrouter/anthropic/claude-3.5-sonnet

# OpêÂ§êÂ£o 3: GPT-4o (excelente para cêÂ³digo)
DEFAULT_MODEL=openrouter/openai/gpt-4o

# OpêÂ§êÂ£o 4: Gemini 2.0 Flash (GRêÂTIS, muito rêÂ¡pido) ê°Å¸â â
DEFAULT_MODEL=openrouter/google/gemini-2.0-flash-exp

# OpêÂ§êÂ£o 5: Llama 3.3 70B (GRêÂTIS, open source) ê°Å¸â â
DEFAULT_MODEL=openrouter/meta-llama/llama-3.3-70b-instruct

# OpêÂ§êÂ£o 6: DeepSeek R1 (GRêÂTIS, raciocêÂ­nio avanêÂ§ado) ê°Å¸â â
DEFAULT_MODEL=openrouter/deepseek/deepseek-r1
```

> ê¢Å¡Â ê¯Â¸Â **ATENêâ¡êÆO:** NêÆO esqueêÂ§a do prefixo `openrouter/` no inêÂ­cio! Sem ele o modelo nêÂ£o serêÂ¡ reconhecido.

> ê°Å¸âÂ¡ **Dica:** VocêÂª pode trocar de modelo a qualquer momento editando o `.env` e executando:
> ```bash
> docker compose down -v && docker compose up -d
> ```

> ê°Å¸âÂ° **Modelos GrêÂ¡tis:** Gemini 2.0 Flash, Llama 3.3 70B e DeepSeek R1 sêÂ£o totalmente gratuitos no OpenRouter. Perfeito para testar!

> ê°Å¸âÅ  **PreêÂ§os e limites:** Consulte [openrouter.ai/models](https://openrouter.ai/models) para ver preêÂ§os, limites de contexto e velocidade de cada modelo.

> ê°Å¸ââ **Guia completo:** Ver [SETUP-OPENROUTER.md](SETUP-OPENROUTER.md) para troubleshooting e mais opêÂ§êÂµes de modelos.

### Passo 5: Build e execuêÂ§êÂ£o

```bash
docker compose up -d
```

> ê°Å¸âÂ¡ **Primeira execuêÂ§êÂ£o** leva alguns minutos para buildar a imagem (baixa Node.js, FFmpeg, Python, etc). As execuêÂ§êÂµes seguintes iniciam instantaneamente.

> ê¢Å¡Â ê¯Â¸Â **Erro no Windows `open //./pipe/dockerDesktopLinuxEngine`?** O Docker Desktop nêÂ£o estêÂ¡ rodando. Abra-o pelo menu Iniciar e espere atêÂ© mostrar "Docker is running", depois tente novamente.

> ê¢ÅÂ¨ **ConfiguraêÂ§êÂ£o automêÂ¡tica:** O script `entrypoint.sh` detecta automaticamente qual provedor de LLM vocêÂª configurou no `.env` e cria a configuraêÂ§êÂ£o ideal. VocêÂª **nêÂ£o precisa** editar arquivos JSON manualmente!

### Passo 6: Acesse o Webchat

Abra no seu navegador:
```
http://localhost:18789/chat
```

Quando solicitado, digite seu `GATEWAY_AUTH_TOKEN` do arquivo `.env` para autenticar.

> ê°Å¸âÂ¡ **Dica:** VocêÂª tambêÂ©m pode acessar diretamente com: `http://localhost:18789/?token=SEU_TOKEN`

### Passo 7: Verifique o status

```bash
# Acompanhe os logs (Ctrl+C para parar)
docker compose logs -f

# Ou veja sêÂ³ as êÂºltimas 50 linhas
docker compose logs --tail 50
```

VocêÂª deve ver uma saêÂ­da como:
```
ê°Å¸Â¤â First run ê¢â¬â creating config from template...
ê°Å¸ââ Setting gateway auth token...
ê°Å¸âÂ± Enabling Telegram...
ê°Å¸ÅÂ Setting gateway bind to lan (required for Docker port mapping)...
ê°Å¸âÂ Enabling logging...
ê°Å¸Â¤â Starting Moltbot...
```

### Passo 8: ConfiguraêÂ§êÂ£o pêÂ³s-instalaêÂ§êÂ£o

Depois que o container estiver rodando, use esses comandos para ajustar seu setup:

```bash
# Auto-detecte e corrija problemas de config
docker exec moltbot clawdbot doctor --fix

# Verifique a saêÂºde geral
docker exec moltbot clawdbot status

# Execute uma auditoria de seguranêÂ§a
docker exec moltbot clawdbot security audit
```

| Comando | O que faz |
|---------|-----------|
| `clawdbot doctor --fix` | Auto-detecta e corrige problemas de config (ex: Telegram configurado mas nêÂ£o habilitado) |
| `clawdbot doctor` | Mesma verificaêÂ§êÂ£o, mas sêÂ³ **mostra** os problemas sem corrigir |
| `clawdbot status` | Mostra status do gateway, canais conectados, info do modelo |
| `clawdbot security audit` | Verifica seu setup contra boas prêÂ¡ticas de seguranêÂ§a |

> ê°Å¸âÂ¡ **Nota:** O comando CLI ainda êÂ© `clawdbot` nesta versêÂ£o (2026.1.24-3). A migraêÂ§êÂ£o para `moltbot` estêÂ¡ em andamento.

---

## ê°Å¸âÂ± ConfiguraêÂ§êÂ£o do Telegram

O Telegram êÂ© a forma mais fêÂ¡cil de falar com seu Moltbot de qualquer lugar.

### Passo a passo:

1. **Crie um bot** ê¢â¬â Abra o Telegram e mande mensagem pro [@BotFather](https://t.me/BotFather)
2. **Envie `/newbot`** ê¢â¬â Siga as instruêÂ§êÂµes para nomear seu bot
3. **Copie o token** ê¢â¬â O BotFather te dêÂ¡ um token tipo `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`
4. **Adicione ao `.env`:**
   ```env
   TELEGRAM_BOT_TOKEN=123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11
   ```
5. **Reinicie o container:**
   ```bash
   docker compose restart
   ```
6. **Mande mensagem pro seu bot** no Telegram ê¢â¬â ele vai te dar um **cêÂ³digo de pareamento**
7. **Aprove o pareamento** dentro do container:
   ```bash
   docker exec moltbot clawdbot pairing approve telegram <code>
   ```

> ê°Å¸âÂ¡ O sistema de pareamento garante que sêÂ³ usuêÂ¡rios aprovados possam falar com seu bot. êâ° uma funcionalidade de seguranêÂ§a ê¢â¬â sem aprovaêÂ§êÂ£o, o bot nêÂ£o responde a estranhos.

### Opcional: Configure as opêÂ§êÂµes do BotFather

Ainda no BotFather, vocêÂª tambêÂ©m pode:
- `/setdescription` ê¢â¬â Adicionar uma descriêÂ§êÂ£o pro seu bot
- `/setabouttext` ê¢â¬â Adicionar texto "Sobre"
- `/setuserpic` ê¢â¬â Definir uma foto de perfil
- `/setcommands` ê¢â¬â Definir comandos do bot (opcional)

---

## ê°Å¸âÂ² ConfiguraêÂ§êÂ£o do WhatsApp

VocêÂª pode conectar o Moltbot ao WhatsApp via pareamento por QR code.

### Passo a passo:

1. **Execute o comando de login:**
   ```bash
   docker exec -it moltbot clawdbot channels login whatsapp
   ```
2. **Escaneie o QR code** com seu WhatsApp (ConfiguraêÂ§êÂµes ê¢â â Aparelhos Conectados ê¢â â Conectar um Aparelho)
3. **Pronto!** Seu Moltbot agora estêÂ¡ conectado ao WhatsApp

### ê¢Å¡Â ê¯Â¸Â NêÂºmero Pessoal vs. NêÂºmero Dedicado

**Usando seu nêÂºmero pessoal:**
- O bot vai ver mensagens de todos os seus contatos
- Por padrêÂ£o, a polêÂ­tica de DM êÂ© `pairing` ê¢â¬â outros podem receber um prompt de pareamento
- **Recomendado:** Defina `dmPolicy: allowlist` com apenas o seu nêÂºmero:

```json
{
  "channels": {
    "whatsapp": {
      "selfChatMode": true,
      "dmPolicy": "allowlist",
      "allowFrom": ["+5511999999999"]
    }
  }
}
```

**Usando um nêÂºmero dedicado (recomendado):**
- Pegue um chip prêÂ©-pago barato ou um nêÂºmero do Google Voice
- Instale o WhatsApp num celular secundêÂ¡rio ou use o WhatsApp Web
- SeparaêÂ§êÂ£o mais limpa entre mensagens pessoais e do bot

> ê°Å¸âÂ¡ **Modo self-chat:** Fale consigo mesmo no WhatsApp ê¢â¬â mensagens para o seu prêÂ³prio nêÂºmero vêÂ£o pro Moltbot. NinguêÂ©m mais êÂ© afetado.

---

## ê°Å¸ââ SeguranêÂ§a

Este setup Docker implementa **7 de 10** medidas de hardening de seguranêÂ§a automaticamente. Veja o [SECURITY.md](SECURITY.md) para o checklist completo.

### O que o Docker faz automaticamente:
| ProteêÂ§êÂ£o | Status |
|----------|--------|
| Gateway vinculado apenas ao `127.0.0.1` (lado do host) | ê¢Åâ¦ AutomêÂ¡tico |
| PolêÂ­tica de DM requer aprovaêÂ§êÂ£o de pareamento | ê¢Åâ¦ AutomêÂ¡tico |
| Arquivos de config com `chmod 600` | ê¢Åâ¦ AutomêÂ¡tico |
| Container roda como usuêÂ¡rio nêÂ£o-root | ê¢Åâ¦ AutomêÂ¡tico |
| Sem escalaêÂ§êÂ£o de privilêÂ©gios (`no-new-privileges`) | ê¢Åâ¦ AutomêÂ¡tico |
| Logging e diagnêÂ³sticos habilitados | ê¢Åâ¦ AutomêÂ¡tico |
| Secrets via variêÂ¡veis de ambiente | ê¢Åâ¦ AutomêÂ¡tico |

### O que VOCêÅ  deve fazer:
- [ ] Configurar o `AGENTS.md` para bloquear comandos perigosos (veja [SECURITY.md](SECURITY.md))
- [ ] Revisar o acesso a ferramentas MCP e restringir ao mêÂ­nimo necessêÂ¡rio
- [ ] Considerar rede `internal: true` se nêÂ£o precisar de internet (bloqueia chamadas de API tambêÂ©m)

### Auditoria de seguranêÂ§a:
```bash
docker exec moltbot clawdbot security audit
```

### Modelo de ameaêÂ§as (simplificado)

**O que o Moltbot pode fazer:**
- Executar comandos shell no container
- Ler/escrever arquivos no workspace
- Fazer requisiêÂ§êÂµes HTTP (chamadas de API, busca na web)
- Controlar um navegador (se configurado)
- Enviar mensagens nos canais conectados

**O que atacantes podem tentar:**
- **InjeêÂ§êÂ£o de prompt:** Enganar o bot via conteêÂºdo web ou mensagens maliciosas
- **Escape de shell:** Fazer o bot rodar comandos perigosos (`rm -rf /`, `curl | bash`)
- **Roubo de token:** Roubar chaves de API dos configs ou logs
- **Acesso nêÂ£o autorizado:** Mandar mensagem pro bot sem aprovaêÂ§êÂ£o
- **ExposiêÂ§êÂ£o de rede:** Acessar o gateway de fora do localhost

### Vulnerabilidades comuns e mitigaêÂ§êÂµes:

| Vulnerabilidade | Risco | MitigaêÂ§êÂ£o |
|----------------|-------|-----------|
| **InjeêÂ§êÂ£o de prompt** | MêÂ©dio | Moltbot envolve conteêÂºdo nêÂ£o-confiêÂ¡vel em tags de seguranêÂ§a; configure o AGENTS.md para bloquear padrêÂµes perigosos |
| **Acesso ao shell** | MêÂ©dio | Isolamento do container + usuêÂ¡rio nêÂ£o-root; bloqueie `rm -rf`, `curl \| bash` no AGENTS.md |
| **Logs de sessêÂ£o em texto puro** | Baixo | Logs ficam dentro de volumes Docker com permissêÂµes restritas; habilite `redactSensitive` na config |
| **Plugins nêÂ£o verificados** | Baixo | Instale plugins apenas de fontes confiêÂ¡veis; revise permissêÂµes de ferramentas MCP |
| **WhatsApp com nêÂºmero pessoal** | MêÂ©dio | Use dmPolicy `allowlist` ou um nêÂºmero dedicado |
| **ExposiêÂ§êÂ£o de rede** | Baixo | Gateway vinculado a 127.0.0.1; use têÂºnel SSH ou Tailscale para acesso remoto |
| **Controle de navegador** | MêÂ©dio | Navegador roda em sandbox; restrinja apenas a sites confiêÂ¡veis |

---

## ê°Å¸âÂ¦ Volumes

Volumes Docker persistem seus dados entre reinêÂ­cios e rebuilds do container.

| Volume | Caminho no Container | Finalidade |
|--------|---------------------|------------|
| `moltbot-data` | `/home/moltbot/.clawdbot` | Config, dados de sessêÂ£o, tokens de auth, info de pareamento |
| `moltbot-workspace` | `/home/moltbot/workspace` | Workspace do agente ê¢â¬â AGENTS.md, arquivos de memêÂ³ria, arquivos de projeto |
| `moltbot-logs` | `/home/moltbot/logs` | Arquivos de log (NêÆO em /tmp ê¢â¬â sobrevive a reinêÂ­cios) |

> ê°Å¸âÂ¡ **Nota:** O diretêÂ³rio de config ainda êÂ© `~/.clawdbot` nesta versêÂ£o. SerêÂ¡ migrado para `~/.moltbot` em versêÂµes futuras.

### FaêÂ§a backup dos seus dados:
```bash
# Backup de todos os volumes
docker run --rm -v moltbot-data:/data -v $(pwd):/backup alpine tar czf /backup/moltbot-data.tar.gz -C /data .
docker run --rm -v moltbot-workspace:/data -v $(pwd):/backup alpine tar czf /backup/moltbot-workspace.tar.gz -C /data .
```

### Resetar tudo:
```bash
docker compose down -v  # ê¢Å¡Â ê¯Â¸Â Apaga TODOS os dados incluindo config e workspace
```

---

## ê°Å¸âºÂ ê¯Â¸Â Comandos êÅ¡teis

```bash
# === Ciclo de vida ===
docker compose up -d              # Start in background
docker compose down               # Stop and remove container
docker compose restart            # Restart
docker compose stop               # Stop without removing

# === Logs ===
docker compose logs -f            # Follow logs (Ctrl+C to stop)
docker compose logs --tail 100    # Last 100 lines

# === Acesso ao shell ===
docker compose exec moltbot bash  # Open shell inside container

# === Clawdbot CLI ===
docker exec moltbot clawdbot status          # Gateway status
docker exec moltbot clawdbot doctor --fix    # Auto-fix issues
docker exec moltbot clawdbot security audit  # Security check

# === Atualizar Moltbot ===
docker compose build --no-cache   # Rebuild image (pulls latest moltbot)
docker compose up -d              # Restart with new image

# === Limpeza ===
docker system prune -a            # Remove unused images (reclaim disk space)
```

---

## ê°Å¸ÅÂ Isolamento de Rede

Por padrêÂ£o, o container tem acesso êÂ  internet ê¢â¬â isso êÂ© **necessêÂ¡rio** para chamadas de API êÂ  Anthropic, OpenAI, etc.

### Isolamento total (sem internet):
```yaml
# No docker-compose.yml, altere:
networks:
  moltbot-net:
    internal: true  # No internet access
```

> ê¢Å¡Â ê¯Â¸Â **AtenêÂ§êÂ£o:** Isso bloqueia TODAS as conexêÂµes de saêÂ­da, incluindo chamadas de API para provedores de LLM. Use apenas se vocêÂª tiver um **setup de modelo local** (ex: Ollama rodando na mesma rede).

### Isolamento parcial (permitir apenas hosts especêÂ­ficos):
Para usuêÂ¡rios avanêÂ§ados, use polêÂ­ticas de rede Docker ou regras iptables para permitir apenas endpoints de API especêÂ­ficos.

---

## ê°Å¸âÂ¡ Canais de Acesso

O Moltbot suporta mêÂºltiplos canais de comunicaêÂ§êÂ£o simultaneamente. Todos os canais compartilham o mesmo agente, memêÂ³ria e workspace.

| Canal | Tipo | Acesso | Dificuldade de Setup | Melhor Para |
|-------|------|--------|---------------------|-------------|
| ê°Å¸âÂ± **Telegram** | Mensagens | Qualquer lugar (mobile/desktop) | ê¢Â­Â FêÂ¡cil | Uso diêÂ¡rio, acesso rêÂ¡pido |
| ê°Å¸âÂ² **WhatsApp** | Mensagens | Qualquer lugar (mobile/desktop) | ê¢Â­Â FêÂ¡cil | Se vocêÂª jêÂ¡ usa WhatsApp |
| ê°Å¸âÂ¬ **Webchat** | Interface Web | Rede local / VPN | ê¢Â­Â FêÂ¡cil | Interface rica, upload de arquivos |
| ê°Å¸ÅÂ **Webchat (pêÂºblico)** | Interface Web | Qualquer lugar | ê¢Â­Âê¢Â­Âê¢Â­Â AvanêÂ§ado | Bot pêÂºblico |
| ê°Å¸ââ **Tailscale** | VPN | Qualquer lugar (zero-trust) | ê¢Â­Âê¢Â­Â MêÂ©dio | Acesso remoto mais seguro |
| ê°Å¸âÅ **Discord** | Mensagens | Qualquer lugar | ê¢Â­Âê¢Â­Â MêÂ©dio | Times, comunidades |
| ê°Å¸âÂ¼ **Slack** | Mensagens | Qualquer lugar | ê¢Â­Âê¢Â­Â MêÂ©dio | Trabalho/empresarial |
| ê°Å¸âÂµ **Signal** | Mensagens | Qualquer lugar | ê¢Â­Âê¢Â­Âê¢Â­Â AvanêÂ§ado | Privacidade mêÂ¡xima |
| ê°Å¸Å¸Â¢ **Matrix** | Mensagens | Qualquer lugar | ê¢Â­Âê¢Â­Âê¢Â­Â AvanêÂ§ado | Self-hosted, federado |

### Qual devo usar?

- **Setup mais simples:** Telegram ê¢â¬â um token de bot e pronto
- **Mais privado:** Signal ou Tailscale + Webchat
- **Acesso de qualquer lugar sem apps extras:** Telegram + WhatsApp (vocêÂª jêÂ¡ tem)
- **Melhor para times/trabalho:** Slack ou Discord
- **Webchat remoto mais seguro:** Tailscale ê¢â¬â VPN zero-trust, sem portas abertas

### Multi-canal

VocêÂª pode habilitar **mêÂºltiplos canais simultaneamente**. Todos os canais compartilham o mesmo agente, memêÂ³ria e workspace. Mensagens de qualquer canal chegam no mesmo assistente.

> ê¢Å¡Â ê¯Â¸Â **Mensagens entre canais sêÂ£o restritas** por design ê¢â¬â o bot nêÂ£o vai vazar dados de conversa entre canais.

---

## ê°Å¸âÂ¥ê¯Â¸Â Acesso ao Webchat (Remoto)

O gateway êÂ© vinculado ao `127.0.0.1` (apenas loopback). Para acessar o webchat de outra mêÂ¡quina, use um **têÂºnel SSH**:

```bash
# Na sua mêÂ¡quina local (a que tem o navegador):
ssh -L 18789:localhost:18789 user@your-server-ip

# Depois abra no navegador:
# http://127.0.0.1:18789/chat
```

Esta êÂ© a forma mais segura de acessar a interface web remotamente ê¢â¬â sem portas expostas, todo trêÂ¡fego criptografado via SSH.

### Alternativa: Tailscale (recomendado para uso frequente)

Se vocêÂª acessa o webchat com frequêÂªncia, configure o [Tailscale](https://tailscale.com) para acesso VPN transparente:

```bash
# No seu servidor:
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up

# Nos seus dispositivos:
# Instale o app Tailscale, faêÂ§a login com a mesma conta
# Acesse o webchat via: http://<tailscale-ip>:18789/chat
```

---

## ê°Å¸Â§Â° Ferramentas e Skills Recomendados

Turbine seu Moltbot com estas ferramentas adicionais:

### ê°Å¸âºÂ  Ferramentas CLI

| Ferramenta | InstalaêÂ§êÂ£o | Finalidade |
|------------|------------|------------|
| FFmpeg | PrêÂ©-instalado na imagem Docker | Processamento de êÂ¡udio/vêÂ­deo |
| Faster Whisper | PrêÂ©-instalado na imagem Docker | TranscriêÂ§êÂ£o local de êÂ¡udio |

> ê¢âÂ¹ê¯Â¸Â **Nota:** Ferramentas como Codex CLI e agent-browser sêÂ£o para outros frameworks e nêÂ£o sêÂ£o compatêÂ­veis com este projeto Moltbot.

### ê°Å¸Å½Â¨ ServiêÂ§os de API

| ServiêÂ§o | Finalidade | PreêÂ§o |
|---------|------------|-------|
| [OpenRouter](https://openrouter.ai) | Gateway para mêÂºltiplos LLMs (modelos gratuitos disponêÂ­veis) | Tier gratuito + pay-per-use |
| [Kie.ai](https://kie.ai) | GeraêÂ§êÂ£o de imagem, vêÂ­deo e mêÂºsica (Veo 3.1, Flux, Suno) | CrêÂ©ditos |
| [ElevenLabs](https://elevenlabs.io) | Text-to-speech (vozes realistas) | Tier gratuito + pago |
| [Gamma](https://gamma.app) | ApresentaêÂ§êÂµes e documentos com IA | Tier gratuito + pago |
| [HeyGen](https://heygen.com) | Avatares de vêÂ­deo com IA | CrêÂ©ditos |

### ê°Å¸âÅ¡ MCP Tools (Model Context Protocol)

O Moltbot suporta ferramentas MCP para estender funcionalidades. Consulte a [documentaêÂ§êÂ£o oficial](https://docs.molt.bot/mcp) para mais informaêÂ§êÂµes sobre como adicionar ferramentas personalizadas.

> ê¢âÂ¹ê¯Â¸Â **Nota:** Skills/Codex sêÂ£o para outros frameworks (Claude Code). Para Moltbot, use ferramentas MCP.

---

## ê°Å¸Â§Â  OrganizaêÂ§êÂ£o de LLMs

EstratêÂ©gia recomendada de modelos para diferentes tarefas:

| Modelo | Provedor | Nome do Modelo | Caso de Uso | Custo |
|--------|----------|----------------|-------------|-------|
| **Claude Sonnet 4.5** | Anthropic | `openrouter/anthropic/claude-sonnet-4.5` | Assistente principal ê¢â¬â conversas, tarefas complexas (recomendado) | Pago (via OpenRouter) |
| **Claude 3.5 Sonnet** | Anthropic | `openrouter/anthropic/claude-3.5-sonnet` | Alternativa mais rêÂ¡pida e econêÂ´mica | Pago (via OpenRouter) |
| **GPT-4o** | OpenAI | `openrouter/openai/gpt-4o` | GeraêÂ§êÂ£o de cêÂ³digo, anêÂ¡lise | Pago (via OpenRouter) |
| **Gemini 2.0 Flash** | Google | `openrouter/google/gemini-2.0-flash-exp` | Tarefas rêÂ¡pidas, consultas simples | GRêÂTIS (via OpenRouter) |

> ê¢Å¡Â ê¯Â¸Â **Importante:** Use os **nomes exatos** dos modelos listados acima. SEMPRE inclua o prefixo `openrouter/` antes do nome do modelo.

> ê°Å¸âÂ¡ **PadrêÂ£o:** Se vocêÂª nêÂ£o especificar um modelo, serêÂ¡ usado `openrouter/anthropic/claude-sonnet-4.5` como padrêÂ£o.

### Como mudar o modelo

Se vocêÂª quiser usar um modelo diferente do padrêÂ£o, use o script `change-model.sh`:

```bash
# Mudar para Claude 3.5 Sonnet (mais rêÂ¡pido e econêÂ´mico)
./change-model.sh "openrouter/anthropic/claude-3.5-sonnet"

# Ou mudar diretamente:
docker exec moltbot sh -c "cat > /tmp/change-model.js << 'EOJS'
const fs = require('fs');
const cfg = JSON.parse(fs.readFileSync('/home/moltbot/.clawdbot/clawdbot.json', 'utf8'));
cfg.agents = cfg.agents || {};
cfg.agents.defaults = cfg.agents.defaults || {};
cfg.agents.defaults.model = { primary: 'openrouter/anthropic/claude-3.5-sonnet' };
fs.writeFileSync('/home/moltbot/.clawdbot/clawdbot.json', JSON.stringify(cfg, null, 2));
EOJS
node /tmp/change-model.js"

docker compose restart
```

> ê¢Å¡Â ê¯Â¸Â **Use nomes exatos:** Modelos devem SEMPRE incluir o prefixo `openrouter/` seguido do provedor (ex: `openrouter/anthropic/`, `openrouter/openai/`, `openrouter/google/`).

---

## ê°Å¸âÂ» Requisitos

| Recurso | MêÂ­nimo | Recomendado |
|---------|--------|-------------|
| **RAM** | 2 GB | 4 GB (com Whisper) |
| **Disco** | 5 GB | 10+ GB |
| **CPU** | 1 core | 2+ cores |
| **Docker** | Engine 24+ / Compose v2+ | êÅ¡ltima versêÂ£o estêÂ¡vel |
| **SO** | Linux, macOS, Windows 10+ | Ubuntu 22.04+ / macOS 13+ |
| **Rede** | Acesso êÂ  internet | Banda larga estêÂ¡vel |

---

## ê°Å¸âÂ§ SoluêÂ§êÂ£o de Problemas

### Problemas no Windows

| Erro | Causa | SoluêÂ§êÂ£o |
|------|-------|---------|
| `open //./pipe/dockerDesktopLinuxEngine: O sistema nêÂ£o pode encontrar o arquivo` | Docker Desktop nêÂ£o estêÂ¡ rodando | Abra o Docker Desktop pelo menu Iniciar, espere por "Docker is running" |
| `.env not found` | Arquivo de config faltando | Execute `copy .env.example .env` e depois `notepad .env` |
| `the attribute version is obsolete` | Formato antigo do docker-compose | Aviso inofensivo ê¢â¬â ignore (este repo nêÂ£o usa `version:`) |
| `WSL docker-desktop Stopped` | WSL nêÂ£o iniciou | Abra o Docker Desktop ê¢â¬â ele inicia o WSL automaticamente |
| Build trava ou falha | RAM insuficiente | Docker Desktop ê¢â â Settings ê¢â â Resources ê¢â â aumente para 4GB+ |
| `exec entrypoint.sh: no such file or directory` | TerminaêÂ§êÂµes de linha CRLF do Windows | Clone o repo novamente: `git config --global core.autocrlf input` e depois `git clone` |
| `npm ERR! Error while executing` | Problemas de rede/proxy | Verifique sua conexêÂ£o com a internet; se estiver atrêÂ¡s de proxy, configure as opêÂ§êÂµes de proxy do Docker |

### Problemas no Linux / Mac

| Erro | Causa | SoluêÂ§êÂ£o |
|------|-------|---------|
| `permission denied` | NêÂ£o estêÂ¡ no grupo docker | `sudo usermod -aG docker $USER` e depois **faêÂ§a logout e login novamente** |
| `port already in use` | Outro serviêÂ§o na porta 18789 | Mude a porta no `docker-compose.yml` ou pare o outro serviêÂ§o |
| `no space left on device` | Disco cheio | `docker system prune -a` para limpar imagens antigas |
| Build falha em Mac ARM | Incompatibilidade de arquitetura | Geralmente funciona; se tiver problemas, tente `docker compose build --platform linux/amd64` |

### Problemas do Docker / Container

| Erro | Causa | SoluêÂ§êÂ£o |
|------|-------|---------|
| `exec entrypoint.sh: no such file or directory` | TerminaêÂ§êÂµes de linha CRLF no entrypoint.sh | **Corrigido automaticamente** pelo Dockerfile (`sed -i 's/\r$//'`). Se ainda acontecer: abra o `entrypoint.sh` no VS Code ê¢â â mude CRLF para LF (canto inferior direito) ê¢â â salve ê¢â â rebuild |
| `error: unknown option '--foreground'` | Sintaxe de comando antiga | O CMD deve ser `["moltbot", "gateway", "run"]` ê¢â¬â atualize seu Dockerfile |
| `npm error: spawn git ENOENT` | Git nêÂ£o estêÂ¡ na imagem Docker | Git estêÂ¡ incluêÂ­do neste Dockerfile. Se estiver usando uma imagem customizada, adicione `git` no `apt-get install` |
| Container fica reiniciando | VêÂ¡rios ê¢â¬â verifique os logs | `docker compose logs --tail 50` e procure o erro |
| Gateway vincula a 127.0.0.1 dentro do container | Bind padrêÂ£o êÂ© loopback | **Corrigido automaticamente** pelo entrypoint.sh (define `bind: "lan"`). Docker precisa de 0.0.0.0 dentro, mas o `docker-compose.yml` restringe acesso do host a 127.0.0.1 |
| Logs em /tmp desaparecem | tmpfs limpa ao reiniciar | Logs sêÂ£o armazenados no volume `/home/moltbot/logs` (NêÆO em /tmp). Isso jêÂ¡ êÂ© o padrêÂ£o. |

### Problemas Gerais

| Problema | SoluêÂ§êÂ£o |
|----------|---------|
| Bot nêÂ£o responde mensagens | Verifique os logs: `docker compose logs -f`. Confirme que as chaves de API e token do bot estêÂ£o corretos. |
| Erros de API / rate limiting | Verifique se as chaves de API no `.env` estêÂ£o corretas e têÂªm crêÂ©ditos |
| NêÂ£o consegue acessar o webchat remotamente | Use têÂºnel SSH: `ssh -L 18789:localhost:18789 user@server` |
| Bot responde devagar | Verifique sua conexêÂ£o com a internet; considere um modelo de LLM mais rêÂ¡pido |
| Mensagem "Pairing required" | Isso êÂ© esperado ê¢â¬â aprove com `clawdbot pairing approve <channel> <code>` |
| MudanêÂ§as de config nêÂ£o aplicadas | Reinicie: `docker compose restart` |

### Problemas de TêÂºnel SSH / Acesso Remoto

Se vocêÂª nêÂ£o consegue acessar o webchat localmente na sua mêÂ¡quina apêÂ³s criar um têÂºnel SSH, siga estes passos:

**1. Remova a chave SSH antiga (se o IP do servidor mudou):**
```bash
ssh-keygen -R seu-servidor-ip
```

**2. Teste a conexêÂ£o SSH:**
```bash
ssh -o StrictHostKeyChecking=accept-new -o BatchMode=yes usuario@seu-servidor-ip "echo 'ConexêÂ£o SSH OK!' && hostname"
```

> ê°Å¸âÂ¡ Se falhar, adicione sua chave pêÂºblica ao `~/.ssh/authorized_keys` do servidor.

**3. Crie o têÂºnel SSH:**
```bash
# TêÂºnel em foreground (fecha quando vocêÂª sair do terminal)
ssh -L 18789:127.0.0.1:18789 usuario@seu-servidor-ip

# TêÂºnel em background (roda silenciosamente)
ssh -f -N -L 18789:127.0.0.1:18789 usuario@seu-servidor-ip
```

**4. Acesse o webchat:**
```
http://127.0.0.1:18789/chat
```

| Problema | Causa | SoluêÂ§êÂ£o |
|----------|-------|---------|
| `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED` | IP do servidor mudou ou reinstalou | `ssh-keygen -R seu-servidor-ip` e reconecte |
| `Permission denied (publickey)` | Chave SSH nêÂ£o configurada | Adicione sua chave pêÂºblica ao servidor: `ssh-copy-id usuario@servidor` |
| `Connection refused` na porta 18789 | TêÂºnel nêÂ£o criado ou container parado | Verifique se o têÂºnel estêÂ¡ ativo e se o container estêÂ¡ rodando |
| `bind: Address already in use` | Porta local jêÂ¡ em uso | Use outra porta: `ssh -L 18790:127.0.0.1:18789 ...` e acesse via `http://127.0.0.1:18790/chat` |

### Problemas de ConfiguraêÂ§êÂ£o

| Problema | Causa | SoluêÂ§êÂ£o |
|----------|-------|---------|
| **"Unknown model: anthropic/claude-sonnet-4.5"** | Falta o prefixo `openrouter/` | Use `openrouter/anthropic/claude-sonnet-4.5` (sempre inclua o prefixo `openrouter/`). Veja [SETUP-OPENROUTER.md](SETUP-OPENROUTER.md) para mais detalhes. |
| **Bot nêÂ£o responde apêÂ³s mudar o modelo** | Config corrompida ou modelo invêÂ¡lido | Execute `docker compose down -v` (ê¢Å¡Â ê¯Â¸Â apaga dados), depois `docker compose up -d` para comeêÂ§ar do zero |
| **MudanêÂ§as no .env nêÂ£o aplicadas** | `docker compose restart` nêÂ£o recarrega variêÂ¡veis de ambiente | Use `docker compose down && docker compose up -d` para recarregar o `.env` |
| **Config manual nêÂ£o funciona** | EdiêÂ§êÂ£o manual causou inconsistêÂªncias | ê¢Å¡Â ê¯Â¸Â **NêÆO edite** `/home/moltbot/.clawdbot/clawdbot.json` manualmente. Deixe o `entrypoint.sh` configurar automaticamente via variêÂ¡veis de ambiente no `.env` |
| **"No API key found for provider 'anthropic'"** | Falta o prefixo `openrouter/` no modelo | Sempre use modelos com prefixo `openrouter/`, ex: `openrouter/anthropic/claude-sonnet-4.5`. Consulte [SETUP-OPENROUTER.md](SETUP-OPENROUTER.md). |

> ê°Å¸âÂ¡ **Melhor prêÂ¡tica:** Configure tudo via arquivo `.env` e deixe o `entrypoint.sh` fazer a configuraêÂ§êÂ£o automêÂ¡tica. Evite editar `clawdbot.json` manualmente!

---

## ê°Å¸ââ MigraêÂ§êÂ£o do Clawdbot

Se vocêÂª estêÂ¡ atualizando do setup antigo `docker-clawdbot`, aqui estêÂ¡ o que mudou:

### O que êÂ© diferente:

| Antigo (Clawdbot) | Novo (Moltbot) |
|-------------------|----------------|
| Pacote: `clawdbot` (npm) | Pacote: `moltbot` (npm) |
| CLI: `clawdbot` | CLI: `moltbot` |
| Comando: `clawdbot gateway start --foreground` | Comando: `moltbot gateway run` |
| Repo: `linnoff88-dev/docker-clawdbot` | Repo: `linnoff88-dev/docker-moltbot` |
| Docs: `docs.clawd.bot` | Docs: `docs.molt.bot` (redirects funcionam) |
| Dir de config: `~/.clawdbot` | Dir de config: `~/.moltbot` (com fallback para `~/.clawdbot`) |
| UsuêÂ¡rio: `clawdbot` | UsuêÂ¡rio: `moltbot` |
| Container: `clawdbot` | Container: `moltbot` |

### Passos da migraêÂ§êÂ£o:

1. **FaêÂ§a backup dos seus dados:**
   ```bash
   # Do setup antigo
   cd docker-clawdbot
   docker run --rm -v clawdbot-data:/data -v $(pwd):/backup alpine tar czf /backup/clawdbot-data-backup.tar.gz -C /data .
   docker run --rm -v clawdbot-workspace:/data -v $(pwd):/backup alpine tar czf /backup/clawdbot-workspace-backup.tar.gz -C /data .
   ```

2. **Pare o container antigo:**
   ```bash
   cd docker-clawdbot
   docker compose down
   ```

3. **Clone o novo repo:**
   ```bash
   git clone https://github.com/linnoff88-dev/docker-moltbot-open.git
   cd docker-moltbot-open
   ```

4. **Copie seu .env:**
   ```bash
   cp ../docker-clawdbot/.env .env
   ```

5. **Inicie o novo container:**
   ```bash
   docker compose up -d
   ```

6. **Restaure os dados (opcional):**
   ```bash
   # Restaurar workspace
   docker run --rm -v moltbot-workspace:/data -v $(pwd):/backup alpine tar xzf /backup/clawdbot-workspace-backup.tar.gz -C /data
   ```

### Notas de compatibilidade:
- O pacote npm antigo `clawdbot` agora êÂ© um **shim** que redireciona para `moltbot`
- Seus arquivos de config existentes sêÂ£o compatêÂ­veis ê¢â¬â o Moltbot faz fallback para `~/.clawdbot` se `~/.moltbot` nêÂ£o existir
- Tokens de bot do Telegram, aprovaêÂ§êÂµes de pareamento e chaves de API sêÂ£o mantidos sem alteraêÂ§êÂ£o
- Pode ser necessêÂ¡rio **re-parear** em alguns canais apêÂ³s a migraêÂ§êÂ£o

### Problemas conhecidos corrigidos nesta versêÂ£o:
- ê¢Åâ¦ Pacote `git` incluêÂ­do no Dockerfile (estava faltando ê¢â â npm install falhava)
- ê¢Åâ¦ TerminaêÂ§êÂµes de linha CRLF corrigidas automaticamente pelo Dockerfile + `.gitattributes` (causava "no such file" no Windows)
- ê¢Åâ¦ Gateway vincula a `lan` dentro do container (estava vinculando a 127.0.0.1 ê¢â â inacessêÂ­vel do host)
- ê¢Åâ¦ Comando correto: `moltbot gateway run` (era `clawdbot gateway start --foreground`)
- ê¢Åâ¦ Logs em volume `/home/moltbot/logs` (estava em /tmp ê¢â â perdido ao reiniciar)
- ê¢Åâ¦ `.dockerignore` e `.gitignore` incluêÂ­dos

---

## ê°Å¸Â¤Â Contribuindo

PRs sêÂ£o bem-vindos! Siga o checklist de seguranêÂ§a em [SECURITY.md](SECURITY.md).

1. FaêÂ§a fork do repo
2. Crie uma branch de feature: `git checkout -b my-feature`
3. FaêÂ§a commit das suas mudanêÂ§as: `git commit -m 'Add my feature'`
4. FaêÂ§a push: `git push origin my-feature`
5. Abra um Pull Request

### Diretrizes:
- Mantenha as boas prêÂ¡ticas de seguranêÂ§a em mente
- Teste no Linux e Windows se possêÂ­vel
- Atualize a documentaêÂ§êÂ£o para qualquer mudanêÂ§a voltada ao usuêÂ¡rio
- Siga o estilo de cêÂ³digo existente

---

## ê°Å¸âÅ LicenêÂ§a

[MIT](LICENSE) ê¢â¬â use como quiser.

---

<p align="center">
  <a href="https://molt.bot">molt.bot</a> ê¢â¬Â¢
  <a href="https://docs.molt.bot">DocumentaêÂ§êÂ£o</a> ê¢â¬Â¢
  <a href="https://discord.gg/clawd">Discord</a> ê¢â¬Â¢
  <a href="https://github.com/moltbot/moltbot">GitHub</a>
</p>

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>
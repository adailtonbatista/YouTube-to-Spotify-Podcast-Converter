# Guia de Instalação Detalhado - YouTube to Spotify Podcast

## Introdução

Este guia fornece instruções passo a passo para instalar e configurar o sistema YouTube to Spotify Podcast Converter em diferentes sistemas operacionais. Siga as instruções específicas para seu sistema operacional.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

1. **Acesso administrativo** ao seu computador
2. **Conexão com a internet** estável
3. **Conta no Spotify** (para submeter o podcast)
4. **Servidor web** ou serviço de hospedagem (para publicação)

## Instalação no Ubuntu/Debian

### Passo 1: Atualizar o Sistema

```bash
sudo apt update
sudo apt upgrade -y
```

### Passo 2: Instalar Python e pip

```bash
sudo apt install python3 python3-pip python3-venv -y
```

### Passo 3: Instalar FFmpeg

```bash
sudo apt install ffmpeg -y
```

### Passo 4: Verificar Instalações

```bash
python3 --version
pip3 --version
ffmpeg -version
```

### Passo 5: Baixar o Projeto

```bash
cd ~
mkdir projetos
cd projetos
# Se você tem o código em um repositório Git:
# git clone <url-do-repositorio>
# cd youtube-to-spotify-podcast

# Ou crie o diretório manualmente:
mkdir youtube-to-spotify-podcast
cd youtube-to-spotify-podcast
```

### Passo 6: Criar Ambiente Virtual (Recomendado)

```bash
python3 -m venv venv
source venv/bin/activate
```

### Passo 7: Instalar Dependências Python

```bash
pip install yt-dlp feedgen flask flask-cors
```

### Passo 8: Copiar os Scripts

Copie todos os arquivos Python fornecidos para o diretório do projeto.

### Passo 9: Testar a Instalação

```bash
python3 youtube_to_podcast.py --help
```

## Instalação no macOS

### Passo 1: Instalar Homebrew (se não tiver)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Passo 2: Instalar Python

```bash
brew install python
```

### Passo 3: Instalar FFmpeg

```bash
brew install ffmpeg
```

### Passo 4: Verificar Instalações

```bash
python3 --version
pip3 --version
ffmpeg -version
```

### Passo 5: Criar Diretório do Projeto

```bash
cd ~
mkdir projetos
cd projetos
mkdir youtube-to-spotify-podcast
cd youtube-to-spotify-podcast
```

### Passo 6: Criar Ambiente Virtual

```bash
python3 -m venv venv
source venv/bin/activate
```

### Passo 7: Instalar Dependências

```bash
pip install yt-dlp feedgen flask flask-cors
```

### Passo 8: Testar a Instalação

```bash
python3 youtube_to_podcast.py --help
```

## Instalação no Windows

### Passo 1: Instalar Python

1. Acesse https://www.python.org/downloads/
2. Baixe a versão mais recente do Python 3
3. Execute o instalador
4. **IMPORTANTE**: Marque "Add Python to PATH" durante a instalação

### Passo 2: Instalar FFmpeg

1. Acesse https://ffmpeg.org/download.html
2. Baixe a versão para Windows
3. Extraia o arquivo para `C:\ffmpeg`
4. Adicione `C:\ffmpeg\bin` ao PATH do sistema:
   - Abra "Configurações do Sistema" → "Variáveis de Ambiente"
   - Edite a variável PATH
   - Adicione `C:\ffmpeg\bin`

### Passo 3: Verificar Instalações

Abra o Prompt de Comando (cmd) e execute:

```cmd
python --version
pip --version
ffmpeg -version
```

### Passo 4: Criar Diretório do Projeto

```cmd
cd %USERPROFILE%
mkdir projetos
cd projetos
mkdir youtube-to-spotify-podcast
cd youtube-to-spotify-podcast
```

### Passo 5: Criar Ambiente Virtual

```cmd
python -m venv venv
venv\Scripts\activate
```

### Passo 6: Instalar Dependências

```cmd
pip install yt-dlp feedgen flask flask-cors
```

### Passo 7: Testar a Instalação

```cmd
python youtube_to_podcast.py --help
```

## Configuração Inicial

### Passo 1: Criar Configuração

Execute o script para criar o arquivo de configuração padrão:

```bash
python3 youtube_to_podcast.py --list
```

### Passo 2: Editar Configurações

Abra o arquivo `config.json` criado e edite com suas informações:

```json
{
  "podcast_title": "Meu Canal - Podcast",
  "podcast_description": "Versão em áudio dos vídeos do meu canal do YouTube",
  "podcast_author": "Seu Nome Completo",
  "podcast_email": "seu.email@gmail.com",
  "podcast_language": "pt-BR",
  "podcast_category": "Technology",
  "audio_directory": "audio",
  "rss_file": "podcast.xml",
  "base_url": "https://seudominio.com/audio/"
}
```

**Campos Obrigatórios para o Spotify:**

- `podcast_email`: Deve ser um email válido e verificado
- `base_url`: URL onde os arquivos serão hospedados publicamente

### Passo 3: Testar com um Vídeo

**IMPORTANTE**: Use apenas vídeos dos quais você possui os direitos!

```bash
python3 youtube_to_podcast.py --url "https://www.youtube.com/watch?v=SEU_VIDEO_ID" --title "Teste - Episódio 1"
```

### Passo 4: Verificar Arquivos Criados

Após o processamento, você deve ter:

- `audio/` - Diretório com o arquivo de áudio
- `podcast.xml` - RSS feed gerado
- `episodes.json` - Lista de episódios

### Passo 5: Testar o Servidor Web

```bash
python3 web_server.py
```

Acesse http://localhost:5000 para ver a página do podcast.

## Configuração de Hospedagem

### Opção 1: Servidor Web Próprio

Se você tem um servidor web:

1. Faça upload da pasta `audio/` e do arquivo `podcast.xml`
2. Atualize `base_url` no `config.json`
3. Regenere o RSS feed executando o script novamente

### Opção 2: GitHub Pages (Gratuito)

1. Crie um repositório no GitHub
2. Faça upload dos arquivos de áudio e RSS
3. Ative GitHub Pages nas configurações
4. Use a URL do GitHub Pages como `base_url`

### Opção 3: Netlify (Gratuito)

1. Crie uma conta no Netlify
2. Faça upload dos arquivos
3. Use a URL fornecida pelo Netlify como `base_url`

### Opção 4: Serviços de Hospedagem de Podcast

Considere usar serviços especializados como:

- Anchor.fm (gratuito)
- Buzzsprout
- Libsyn
- Transistor

## Submissão ao Spotify

### Passo 1: Verificar RSS Feed

Certifique-se de que seu RSS feed está acessível publicamente:

```
https://seudominio.com/podcast.xml
```

### Passo 2: Acessar Spotify for Podcasters

1. Vá para https://podcasters.spotify.com/
2. Faça login com sua conta Spotify
3. Clique em "Add your podcast"

### Passo 3: Submeter RSS Feed

1. Cole a URL do seu RSS feed
2. Preencha as informações solicitadas
3. Aguarde a verificação (pode levar 1-5 dias)

### Passo 4: Verificar Status

Você receberá um email quando o podcast for aprovado ou se houver problemas.

## Automação (Opcional)

### Script de Automação Diária

Crie um script para processar novos vídeos automaticamente:

```bash
#!/bin/bash
# automation.sh

cd /caminho/para/youtube-to-spotify-podcast
source venv/bin/activate

# Lista de URLs para processar (atualize conforme necessário)
VIDEOS=(
    "https://www.youtube.com/watch?v=VIDEO1"
    "https://www.youtube.com/watch?v=VIDEO2"
)

for url in "${VIDEOS[@]}"; do
    python3 youtube_to_podcast.py --url "$url"
done

# Fazer upload dos arquivos para o servidor (exemplo com rsync)
# rsync -av audio/ usuario@servidor:/caminho/para/audio/
# rsync -av podcast.xml usuario@servidor:/caminho/para/podcast.xml
```

### Cron Job (Linux/macOS)

Para executar automaticamente:

```bash
crontab -e
```

Adicione uma linha como:

```
0 6 * * * /caminho/para/automation.sh
```

## Solução de Problemas Comuns

### Erro: "python3: command not found"

**Solução**: Instale Python ou use `python` em vez de `python3`.

### Erro: "ffmpeg: command not found"

**Ução**: Instale FFmpeg e certifique-se de que está no PATH.

### Erro: "Permission denied"

**Solução**: Use `chmod +x` para tornar os scripts executáveis.

### Erro: "Module not found"

**Solução**: Ative o ambiente virtual e reinstale as dependências.

### RSS Feed não funciona no Spotify

**Verificações**:

1. RSS feed está publicamente acessível?
2. Email no config.json é válido?
3. URLs dos arquivos de áudio estão corretas?
4. Arquivos de áudio estão acessíveis?

## Manutenção

### Atualizar Dependências

```bash
pip install --upgrade yt-dlp feedgen flask flask-cors
```

### Backup dos Dados

Faça backup regular de:

- `config.json`
- `episodes.json`
- Pasta `audio/`
- `podcast.xml`

### Monitoramento

Verifique regularmente:

- Status do servidor de hospedagem
- Acessibilidade do RSS feed
- Funcionamento do script de conversão

## Próximos Passos

Após a instalação bem-sucedida:

1. **Teste com conteúdo próprio** antes de usar em produção
2. **Configure hospedagem confiável** para os arquivos
3. **Submeta ao Spotify** e aguarde aprovação
4. **Configure automação** se necessário
5. **Monitore o desempenho** e faça ajustes conforme necessário

## Suporte

Se encontrar problemas durante a instalação:

1. Verifique os logs de erro
2. Consulte a seção de solução de problemas
3. Verifique se todas as dependências estão instaladas
4. Teste cada componente individualmente

---

**Nota**: Este guia assume uso responsável e legal da ferramenta. Sempre respeite os direitos autorais e os Termos de Serviço das plataformas utilizadas.


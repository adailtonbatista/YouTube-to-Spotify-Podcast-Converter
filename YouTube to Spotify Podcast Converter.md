# YouTube to Spotify Podcast Converter

## Visão Geral

Este projeto fornece uma solução automatizada para extrair áudio de vídeos do YouTube e publicá-los como podcasts no Spotify. O sistema utiliza ferramentas modernas de extração de áudio e geração de RSS feeds para criar um fluxo de trabalho completo de conversão de conteúdo de vídeo para podcast.

**⚠️ IMPORTANTE: AVISO LEGAL**

Este script é destinado apenas para uso educacional e para conteúdo do qual você possui os direitos autorais. Antes de usar este script, certifique-se de que:

1. Você é o proprietário do conteúdo do YouTube que está convertendo
2. Você tem permissão explícita do criador do conteúdo
3. O uso está em conformidade com os Termos de Serviço do YouTube
4. O uso está em conformidade com as leis de direitos autorais aplicáveis

O uso inadequado desta ferramenta pode resultar em violação de direitos autorais e dos Termos de Serviço do YouTube.

## Características Principais

- **Extração de Áudio de Alta Qualidade**: Utiliza yt-dlp para extrair áudio em formato MP3 com qualidade de 192 kbps
- **Geração Automática de RSS Feed**: Cria feeds RSS compatíveis com o Spotify e outras plataformas de podcast
- **Servidor Web Integrado**: Inclui servidor Flask para hospedar arquivos de áudio e RSS feed
- **Interface de Linha de Comando**: Ferramenta fácil de usar via terminal
- **Configuração Flexível**: Sistema de configuração baseado em JSON
- **Metadados Automáticos**: Extrai automaticamente título, descrição e data dos vídeos do YouTube

## Arquitetura do Sistema

O sistema é composto por três componentes principais:

1. **youtube_to_podcast.py**: Script principal para extração de áudio e geração de RSS
2. **web_server.py**: Servidor web para hospedar conteúdo do podcast
3. **config.json**: Arquivo de configuração com metadados do podcast

## Requisitos do Sistema

### Dependências Python

- Python 3.7 ou superior
- yt-dlp (para extração de áudio do YouTube)
- feedgen (para geração de RSS feeds)
- flask (para servidor web)
- flask-cors (para suporte CORS)

### Dependências do Sistema

- FFmpeg (para processamento de áudio)

## Instalação

### 1. Clonar ou Baixar o Projeto

```bash
git clone <url-do-repositorio>
cd youtube-to-spotify-podcast
```

### 2. Instalar Dependências Python

```bash
pip3 install -r requirements.txt
```

### 3. Instalar FFmpeg

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install ffmpeg
```

**macOS (com Homebrew):**
```bash
brew install ffmpeg
```

**Windows:**
Baixe o FFmpeg do site oficial e adicione ao PATH do sistema.

## Configuração

### 1. Configuração Inicial

Execute o script uma vez para criar o arquivo de configuração padrão:

```bash
python3 youtube_to_podcast.py --list
```

### 2. Editar Configurações

Edite o arquivo `config.json` criado com suas informações:

```json
{
  "podcast_title": "Seu Podcast do YouTube",
  "podcast_description": "Descrição do seu podcast",
  "podcast_author": "Seu Nome",
  "podcast_email": "seu.email@exemplo.com",
  "podcast_language": "pt-BR",
  "podcast_category": "Technology",
  "audio_directory": "audio",
  "rss_file": "podcast.xml",
  "base_url": "https://seudominio.com/audio/"
}
```

**Campos Importantes:**

- `base_url`: URL base onde os arquivos de áudio serão hospedados
- `podcast_email`: Email válido (obrigatório para submissão ao Spotify)
- `podcast_category`: Categoria do podcast (Technology, Education, Entertainment, etc.)

## Uso Básico

### Converter um Vídeo do YouTube

```bash
python3 youtube_to_podcast.py --url "https://www.youtube.com/watch?v=VIDEO_ID"
```

### Converter com Título Personalizado

```bash
python3 youtube_to_podcast.py --url "https://www.youtube.com/watch?v=VIDEO_ID" --title "Episódio 1 - Meu Podcast"
```

### Listar Episódios Existentes

```bash
python3 youtube_to_podcast.py --list
```

## Hospedagem e Publicação

### 1. Servidor Web Local

Para testar localmente, use o servidor web incluído:

```bash
python3 web_server.py
```

Acesse:
- Página principal: http://localhost:5000
- RSS Feed: http://localhost:5000/podcast.xml

### 2. Hospedagem em Produção

Para publicar no Spotify, você precisa hospedar os arquivos em um servidor web público:

1. **Upload dos Arquivos**: Faça upload da pasta `audio/` e do arquivo `podcast.xml` para seu servidor web
2. **Atualizar base_url**: Edite `config.json` com a URL real do seu servidor
3. **Regenerar RSS**: Execute o script novamente para atualizar as URLs no RSS feed

### 3. Submeter ao Spotify

1. Acesse [Spotify for Podcasters](https://podcasters.spotify.com/)
2. Faça login com sua conta Spotify
3. Clique em "Add your podcast"
4. Insira a URL do seu RSS feed (ex: https://seudominio.com/podcast.xml)
5. Aguarde a aprovação (pode levar alguns dias)

## Estrutura de Arquivos

```
youtube-to-spotify-podcast/
├── youtube_to_podcast.py    # Script principal
├── web_server.py           # Servidor web
├── example_usage.py        # Exemplo de uso
├── requirements.txt        # Dependências
├── config.json            # Configurações (criado automaticamente)
├── episodes.json          # Lista de episódios (criado automaticamente)
├── podcast.xml            # RSS feed (criado automaticamente)
├── audio/                 # Diretório dos arquivos de áudio
└── README.md             # Esta documentação
```

## Uso Programático

Você também pode usar o conversor programaticamente:

```python
from youtube_to_podcast import YouTubeToPodcast

# Criar instância
converter = YouTubeToPodcast("config.json")

# Processar vídeo
success = converter.process_video(
    "https://www.youtube.com/watch?v=VIDEO_ID",
    "Título do Episódio"
)

if success:
    print("Episódio criado com sucesso!")
```

## Solução de Problemas

### Erro: "FFmpeg not found"

Certifique-se de que o FFmpeg está instalado e disponível no PATH do sistema.

### Erro: "Unable to extract audio"

1. Verifique se a URL do YouTube é válida
2. Certifique-se de que o vídeo não é privado ou restrito
3. Verifique sua conexão com a internet

### RSS Feed não aparece no Spotify

1. Verifique se o email no config.json é válido
2. Certifique-se de que o RSS feed está acessível publicamente
3. Aguarde até 24 horas para processamento pelo Spotify

### Arquivos de áudio muito grandes

Ajuste a qualidade do áudio no script (linha com `'audioquality': '192'`) para um valor menor como `'128'`.

## Limitações e Considerações

### Termos de Serviço do YouTube

O YouTube não permite oficialmente o download de conteúdo através de ferramentas de terceiros. Este script deve ser usado apenas para:

- Conteúdo do qual você possui os direitos autorais
- Conteúdo com permissão explícita do criador
- Uso educacional e pessoal

### Limitações Técnicas

- Qualidade do áudio limitada pela qualidade original do vídeo
- Dependência de ferramentas externas (yt-dlp, FFmpeg)
- Necessidade de hospedagem web para publicação

### Requisitos do Spotify

- RSS feed deve estar publicamente acessível
- Email válido obrigatório no RSS feed
- Processo de aprovação pode levar alguns dias
- Conteúdo deve seguir as diretrizes do Spotify

## Contribuição

Este projeto é open source. Contribuições são bem-vindas através de:

- Relatórios de bugs
- Sugestões de melhorias
- Pull requests
- Documentação

## Licença

Este projeto é fornecido "como está" para fins educacionais. Os usuários são responsáveis por garantir o cumprimento de todas as leis e termos de serviço aplicáveis.

## Suporte

Para suporte e dúvidas:

1. Consulte esta documentação
2. Verifique a seção de solução de problemas
3. Abra uma issue no repositório do projeto

---

**Desenvolvido por Manus AI** - Ferramenta para automação de conversão de conteúdo YouTube para podcast.


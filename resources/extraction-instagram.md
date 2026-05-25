# Introdução
Este documento apresenta um conjunto de ferramentas especializadas em OSINT voltado principalmente para o Instagram: Toutatis, Osintgram e Instaloader.
O objetivo é oferecer uma visão prática ajudando analistas a operarem as ferramentas mais adequadas a cada tipo de caso.
A documentação está organizada em capítulos dedicados seguindo a mesma estrutura: visão geral, sites oficiais, principais funcionalidades, guia de instalação, modos de uso, exemplos de comandos, limitações e boas práticas. 
Ao final, há uma seção comparativa que destaca os pontos fortes e fracos de cada solução, bem como cenários recomendados de uso combinado entre elas.

# Toutatis

Toutatis foca em extrair informações públicas de contas do Instagram, como nome, bio, contagem de seguidores, foto de perfil e, em alguns casos, e-mail ou telefone expostos publicamente.

## Sites

- Repositório: [GitHub](https://github.com/megadose/toutatis)
- Biblioteca: [lib.rs](https://lib.rs/crates/toutatis)

## O que ela faz

- Consulta perfis do Instagram por `username` ou `instagram ID`.
- Exibe metadados públicos do perfil, como biografia, foto de perfil e estatísticas da conta.
- Pode mostrar contatos públicos associados ao perfil, se existirem.

## Como utilizar

### 1. Preparação do ambiente

#### 1.1 Verificar instalação do Python

Certifique-se de que o Python 3.7 ou superior está instalado:

```bash
python3 --version
```

#### 1.2 Instalar o Toutatis

Recomendação: instale a versão 1.3, que é mais estável:

```bash
pip install toutatis==1.3
```

Se preferir instalar via GitHub:

```bash
git clone https://github.com/megadose/toutatis
cd toutatis
sudo python3 setup.py install
```

#### 1.3 Verificar a instalação

Após instalar, teste se a ferramenta está funcionando:

```bash
toutatis -h
```

Esse comando exibe a ajuda com todos os parâmetros disponíveis.

### 2. Obter o Instagram Session ID

O Toutatis requer autenticação via `sessionid` do Instagram para funcionar. Veja como extrair:

#### Passo a passo no navegador Chrome/Edge

1. Faça login no Instagram pelo navegador desktop.
2. Pressione `F12` para abrir as Ferramentas de Desenvolvedor.
3. Vá para a aba **Application** (Chrome) ou **Storage** (Firefox).
4. No painel esquerdo, expanda **Cookies** e clique em `https://www.instagram.com`.
5. Procure pela entrada `sessionid`.
6. Copie o valor completo do cookie.

#### Alternativa: usar extensão de cookies

Instale uma extensão como **EditThisCookie** ou similar, abra o Instagram, clique na extensão e copie o valor do `sessionid`.

> ⚠️ Importante: o `sessionid` dá acesso à sua conta. Nunca compartilhe e use em ambiente seguro.

### 3. Comandos de execução

#### 3.1 Buscar informações por nome de usuário

```bash
toutatis -u nome_de_usuario -s SEU_SESSIONID
```

Exemplo:

```bash
toutatis -u geeksforgeeks -s 12345abcdefghijk
```

#### 3.2 Buscar informações por ID do Instagram

```bash
toutatis -i ID_NUMERICO -s SEU_SESSIONID
```

Exemplo:

```bash
toutatis -i 123456789 -s 12345abcdefghijk
```

### 4. Interpretação dos resultados

Exemplo de saída típica:

```text
Informations about : geeksforgeeks
Full Name : GeeksforGeeks | userID : 123456789
Verified : False | Is business Account : True
Is private Account : False
Follower : 50000 | Following : 200
Number of posts : 1500
External url : https://geeksforgeeks.org
Public Email : contact@geeksforgeeks.org
Public Phone : +91 XX XXXX XXXX
Profile Picture : [URL da foto de perfil]
```

#### O que cada campo significa

- **Full Name**: nome completo exibido no perfil.
- **userID**: identificador numérico único da conta no Instagram.
- **Verified**: indica se a conta possui selo de verificação.
- **Is business Account**: informa se é conta comercial ou criador de conteúdo.
- **Is private Account**: indica se o perfil é privado, embora alguns dados públicos ainda possam ser exibidos.
- **Follower / Following**: contadores de seguidores e contas seguidas.
- **Number of posts**: total de publicações.
- **External url**: link exibido na bio.
- **Public Email / Public Phone**: contatos públicos, se disponíveis na conta comercial.

# Osintgram

Osintgram é uma ferramenta especializada de OSINT de código aberto projetada para coletar e analisar dados publicamente disponíveis de perfis do Instagram de forma estruturada e eficiente. Construída para investigadores digitais, pesquisadores e analistas, ela transforma informações dispersas de redes sociais em insights significativos que apoiam tomadas de decisão mais inteligentes.

## Sites

- Site oficial: [osintgram.com](https://osintgram.com/)
- Repositório GitHub: [Datalux/Osintgram](https://github.com/Datalux/Osintgram)
- Rust crates: [lib.rs/crates/toutatis](https://lib.rs/crates/toutatis)

## O que ela faz

Usando uma interface de linha de comando baseada em Python, o Osintgram permite extrair detalhes-chave como:

- Informações de perfil (nome, bio, verificação, tipo de conta)
- Posts, legendas e descrições de fotos
- Hashtags mais usadas e padrões de conteúdo
- Comentários e padrões de engajamento
- Seguidores e contas seguidas
- Dados de geolocalização quando disponíveis
- Endereços de e-mail e telefones públicos (se expostos em contas comerciais)
- Usuários marcados e que mais comentam

## Como utilizar

### 1. Preparação do ambiente

#### 1.1 Pré-requisitos

Certifique-se de que o sistema atende aos requisitos necessários:

- **Python 3.8 ou superior**
- **Git** para clonar o repositório
- **pip** (gerenciador de pacotes Python)
- Conta ativa do Instagram
- Sistema operacional: Linux, macOS ou Windows (WSL recomendado)

#### 1.2 Verificar instalação do Python

```bash
python3 --version
```

#### 1.3 Instalar o Osintgram

**Via GitHub (recomendado):**

```bash
# Clonar o repositório
git clone https://github.com/Datalux/Osintgram.git

# Navegar para o diretório
cd Osintgram

# Instalar dependências
pip install -r requirements.txt
```

#### 1.4 Verificar a instalação

Teste se a ferramenta está funcionando:

```bash
python main.py -h
```

Este comando exibe a ajuda com todos os parâmetros disponíveis.

### 2. Configurar credenciais do Instagram

#### 2.1 Adicionar credenciais

O Osintgram requer autenticação via conta do Instagram. Durante a primeira execução, você será solicitado a fornecer suas credenciais.

**Método 1: Configuração manual**

Edite o arquivo `config/credentials.ini`:

```bash
echo "seu_usuario_instagram" > config/credentials.ini
```

Durante a execução, você será solicitado a inserir a senha.

**Método 2: Via prompt interativo**

Ao executar o Osintgram pela primeira vez, ele solicitará automaticamente suas credenciais.

> ⚠️ **Importante**: Use uma conta secundária dedicada para análise OSINT, nunca sua conta pessoal principal. O Instagram pode detectar comportamento automatizado e aplicar restrições ou bloqueios temporários.

### 3. Comandos de execução

#### 3.1 Iniciar análise de um perfil

```bash
python main.py nome_de_usuario_alvo
```

Isso iniciará uma sessão interativa onde você pode executar comandos específicos.

#### 3.2 Comandos disponíveis (20+ opções)

Uma vez dentro da sessão interativa, você pode usar os seguintes comandos:

| Comando | Descrição |
|---------|-----------|
| `info` | Exibe informações do perfil (nome, ID, verificação, tipo de conta) |
| `followers` | Lista seguidores da conta |
| `followings` | Lista contas seguidas |
| `fwersemail` | Extrai e-mails de seguidores (se públicos) |
| `fwingsemail` | Extrai e-mails de contas seguidas |
| `fwersnumber` | Extrai telefones de seguidores (se públicos) |
| `hashtags` | Mostra hashtags mais usadas |
| `captions` | Extrai legendas de posts |
| `comments` | Conta total de comentários |
| `likes` | Mostra total de curtidas |
| `photodes` | Exibe descrições de fotos |
| `photos` | Baixa todas as fotos do perfil |
| `propic` | Baixa foto de perfil em alta resolução |
| `stories` | Baixa stories (se disponíveis) |
| `tagged` | Lista usuários marcados nas publicações |
| `addrs` | Todos os endereços registrados por localização |
| `mediatype` | Tipos de mídia nos posts (foto, vídeo, carrossel) |
| `wcommented` | Usuários que mais comentaram |
| `wtagged` | Usuários mais marcados |
| `target` | Define novo alvo para análise |

#### 3.3 Exemplo de uso prático

```bash
# Iniciar sessão
python main.py exemplo_usuario

# Dentro da sessão interativa:
> info              # Ver informações básicas
> followers         # Listar seguidores
> hashtags          # Hashtags mais usadas
> photos            # Baixar todas as fotos
> exit              # Sair da sessão
```

### 4. Interpretação dos resultados

#### 4.1 Exemplo de saída do comando `info`

```text
Username: exemplo_usuario
Full Name: Nome Completo
User ID: 123456789
Is Verified: False
Is Business Account: True
Is Private Account: False
Followers: 50000
Following: 200
Number of Posts: 1500
Biography: Descrição da bio...
External URL: https://exemplo.com
Public Email: contato@exemplo.com
Public Phone: +55 11 XXXX-XXXX
```

#### 4.2 O que cada campo significa

- **Username**: Nome de usuário (@exemplo_usuario)
- **Full Name**: Nome completo exibido no perfil
- **User ID**: Identificador numérico único da conta
- **Is Verified**: Indica se possui selo de verificação
- **Is Business Account**: Se é conta comercial ou criador de conteúdo
- **Is Private Account**: Se o perfil é privado (dados públicos ainda são exibidos)
- **Followers / Following**: Contadores de seguidores e seguindo
- **Number of Posts**: Total de publicações
- **Biography**: Texto da biografia
- **External URL**: Link na bio
- **Public Email / Phone**: Contatos públicos disponíveis em contas comerciais

### 5. Exportação e documentação de dados

#### 5.1 Salvar resultados

O Osintgram permite salvar dados coletados em diversos formatos para análise posterior:

```bash
# Dentro da sessão, redirecionar output
python main.py usuario_alvo > resultado_analise.txt

# Ou usar comandos específicos de download
> photos    # Salva fotos em pasta local
> propic    # Salva foto de perfil
```

#### 5.2 Organização de evidências

- Registre data/hora da coleta
- Documente comandos executados
- Capture screenshots de resultados importantes
- Armazene em formato estruturado (JSON, CSV, TXT)
- Mantenha cadeia de custódia para uso em investigações formais

### 6. Limitações técnicas e operacionais

#### 6.1 Dependência de autenticação

- Requer conta Instagram válida para funcionar
- Instagram pode detectar automação e aplicar rate limiting
- Bloqueios temporários podem ocorrer em caso de uso excessivo

#### 6.2 Dados limitados a informações públicas

- Não acessa conteúdo privado, DMs ou stories de contas privadas
- Mesmo em contas privadas, exibe dados públicos básicos (foto de perfil, nome, bio)
- Seguidores e seguindo de contas privadas não são acessíveis

#### 6.3 Mudanças na plataforma

- Instagram pode alterar APIs e endpoints, quebrando funcionalidades
- Atualizações regulares da ferramenta podem ser necessárias
- Algumas funcionalidades podem parar de funcionar sem aviso prévio

### 7. Resolução de problemas comuns

#### Erro: "Módulo Python não encontrado"

```bash
# Reinstalar dependências
pip install -r requirements.txt --upgrade
```

#### Erro: "Credenciais inválidas"

- Verifique usuário e senha
- Confirme que a conta não está bloqueada
- Tente fazer login manual no navegador primeiro
- Use autenticação de dois fatores se necessário

#### Erro: "Rate limit excedido"

- Reduza frequência de comandos
- Aguarde algumas horas antes de tentar novamente
- Use conta diferente
- Configure delays entre requisições

#### Erro: "Instagram checkpoint required"

- Faça login manual no Instagram pelo navegador
- Complete verificações de segurança solicitadas
- Aguarde liberação da conta
- Use conta menos restrita

### 8. Exemplo completo de fluxo de trabalho

```bash
# 1. Clonar repositório
git clone https://github.com/Datalux/Osintgram.git
cd Osintgram

# 2. Instalar dependências
pip install -r requirements.txt

# 3. Configurar credenciais (primeira execução)
echo "conta_osint_pesquisa" > config/credentials.ini

# 4. Executar análise
python main.py usuario_alvo

# 5. Comandos dentro da sessão interativa
> info              # Informações gerais
> followers         # Listar seguidores
> hashtags          # Hashtags mais usadas
> photos            # Baixar fotos
> wcommented        # Quem mais comentou

# 6. Documentar e salvar
> exit
mv output/* /caminho/pasta/investigacao/

# 7. Análise e relatório
# Compilar resultados em relatório estruturado
```

# Instaloader

Instaloader é uma ferramenta poderosa de código aberto em Python especializada em download e análise de conteúdo do Instagram. Com mais de 11.000 stars no GitHub, ela permite baixar fotos, vídeos, stories, highlights, reels e metadados associados de perfis públicos e privados, sendo amplamente utilizada para pesquisa OSINT, preservação de evidências digitais e análise forense de redes sociais.

## Sites

- Site oficial: [instaloader.github.io](https://instaloader.github.io)
- Repositório GitHub: [instaloader/instaloader](https://github.com/instaloader/instaloader)
  
## O que ela faz

Instaloader oferece funcionalidades abrangentes para coleta e análise de dados do Instagram:

- Download de perfis públicos e privados completos
- Extração de posts, vídeos, reels, IGTV e carrosséis
- Captura de stories e highlights (incluindo stories de seguidores)
- Download de posts salvos e feed pessoal (quando autenticado)
- Coleta de comentários, geotags e legendas de cada post
- Busca e download por hashtags
- Busca por localização (location ID)
- Download de contas seguidas por um perfil (@profile)
- Detecção automática de mudanças de nome de perfil
- Retomada automática de downloads interrompidos
- Personalização avançada de filtros e organização de arquivos

## Como utilizar

### 1. Preparação do ambiente

#### 1.1 Pré-requisitos

Certifique-se de que o sistema atende aos requisitos necessários:

- **Python 3.8 ou superior**
- **pip** (gerenciador de pacotes Python)
- Conexão estável com a internet
- Sistema operacional: Linux, macOS, Windows ou Android (via Termux)

#### 1.2 Verificar instalação do Python

```bash
python3 --version
```

#### 1.3 Instalar o Instaloader

**Método recomendado (via pip):**

```bash
pip3 install instaloader
```

**Atualizar para a versão mais recente:**

```bash
pip3 install --upgrade instaloader
```

**Instalar versão de pré-lançamento (para testar novos recursos):**

```bash
pip3 install --pre instaloader
```

**Instalação manual (alternativa):**

```bash
# Baixar do GitHub
git clone https://github.com/instaloader/instaloader.git
cd instaloader
python3 setup.py install
```

#### 1.4 Verificar a instalação

```bash
instaloader --help
```

Este comando exibe todas as opções e parâmetros disponíveis.

### 2. Uso básico via linha de comando

#### 2.1 Download de perfil completo

```bash
instaloader nome_do_perfil
```

Baixa todas as fotos, vídeos e metadados do perfil especificado.

**Múltiplos perfis:**

```bash
instaloader perfil1 perfil2 perfil3
```

#### 2.2 Download apenas da foto de perfil

```bash
instaloader --profile-pic-only nome_do_perfil
```

#### 2.3 Atualização rápida de perfis

```bash
instaloader --fast-update nome_do_perfil
```

Para quando interrompe no primeiro post já baixado anteriormente.

**Com controle de timestamp:**

```bash
instaloader --latest-stamps -- nome_do_perfil
```

Armazena timestamp da última execução e baixa apenas conteúdo novo.

### 3. Download de conteúdo específico

#### 3.1 Stories

**Stories do próprio feed (requer login):**

```bash
instaloader --login seu_usuario :stories
```

**Stories de um perfil específico:**

```bash
instaloader --stories nome_do_perfil
```

#### 3.2 Highlights

```bash
instaloader --highlights nome_do_perfil
```

#### 3.3 Reels e IGTV

```bash
instaloader --reels nome_do_perfil
instaloader --igtv nome_do_perfil
```

#### 3.4 Posts marcados (tagged)

```bash
instaloader --tagged nome_do_perfil
```

#### 3.5 Hashtags

```bash
instaloader "#nome_da_hashtag"
```

**Importante:** Use aspas para evitar problemas com o caractere `#`.

#### 3.6 Localização

```bash
instaloader %123456789
```

Onde `123456789` é o ID numérico da localização no Instagram.

#### 3.7 Feed pessoal (requer login)

```bash
instaloader --login seu_usuario :feed
```

#### 3.8 Posts salvos (requer login)

```bash
instaloader --login seu_usuario :saved
```

#### 3.9 Perfis seguidos por uma conta

```bash
instaloader @nome_do_perfil
```

Baixa todos os perfis que `nome_do_perfil` está seguindo.

### 4. Autenticação e perfis privados

#### 4.1 Login interativo

```bash
instaloader --login seu_usuario nome_do_perfil
```

Você será solicitado a inserir sua senha na primeira execução.

#### 4.2 Autenticação de dois fatores

Se sua conta usa 2FA, o Instaloader solicitará o código de verificação após a senha.

#### 4.3 Sessão persistente

Após o primeiro login bem-sucedido, o Instaloader armazena cookies de sessão no diretório temporário do sistema. Nas próximas execuções com `--login`, a autenticação é automática sem solicitar senha novamente.

**Localização dos cookies (Linux/macOS):**
```
/tmp/instaloader-session-seu_usuario
```

**Localização dos cookies (Windows):**
```
%TEMP%\instaloader-session-seu_usuario
```

> ⚠️ **Importante**: Use uma conta secundária dedicada para OSINT. Nunca use sua conta pessoal principal, pois o Instagram pode detectar comportamento automatizado e aplicar restrições.

### 5. Opções avançadas de download

#### 5.1 Incluir comentários e geotags

```bash
instaloader --comments --geotags nome_do_perfil
```

#### 5.2 Definir intervalo de datas

**Baixar posts desde uma data:**

```bash
instaloader --post-filter="date_utc >= datetime(2024, 1, 1)" nome_do_perfil
```

**Baixar posts até uma data:**

```bash
instaloader --post-filter="date_utc <= datetime(2024, 12, 31)" nome_do_perfil
```

**Intervalo específico:**

```bash
instaloader --post-filter="datetime(2024, 1, 1) <= date_utc <= datetime(2024, 12, 31)" nome_do_perfil
```

#### 5.3 Filtros por tipo de mídia

**Apenas fotos:**

```bash
instaloader --post-filter="not is_video" nome_do_perfil
```

**Apenas vídeos:**

```bash
instaloader --post-filter="is_video" nome_do_perfil
```

#### 5.4 Filtros por engajamento

**Posts com mais de 1000 curtidas:**

```bash
instaloader --post-filter="likes >= 1000" nome_do_perfil
```

**Posts com comentários:**

```bash
instaloader --post-filter="comments >= 1" nome_do_perfil
```

#### 5.5 Controle de velocidade (rate limiting)

```bash
instaloader --sleep-on-download 2 nome_do_perfil
```

Adiciona 2 segundos de pausa entre downloads para evitar detecção.

### 6. Uso como módulo Python

#### 6.1 Script básico para download de perfil

```python
import instaloader

# Criar instância
L = instaloader.Instaloader()

# Baixar perfil
L.download_profile('nome_do_perfil', profile_pic_only=False)
```

#### 6.2 Extrair metadados de perfil

```python
import instaloader

L = instaloader.Instaloader()
profile = instaloader.Profile.from_username(L.context, 'nome_do_perfil')

# Acessar dados
print(f"Nome completo: {profile.full_name}")
print(f"ID do usuário: {profile.userid}")
print(f"Seguidores: {profile.followers}")
print(f"Seguindo: {profile.followees}")
print(f"Biografia: {profile.biography}")
print(f"É verificado: {profile.is_verified}")
print(f"É privado: {profile.is_private}")
print(f"É conta comercial: {profile.is_business_account}")
print(f"Total de posts: {profile.mediacount}")
print(f"URL externa: {profile.external_url}")
```

#### 6.3 Download com autenticação

```python
import instaloader

L = instaloader.Instaloader()

# Login
L.login('seu_usuario', 'sua_senha')

# Baixar perfil privado
L.download_profile('perfil_privado')
```

#### 6.4 Iterar sobre posts e extrair dados

```python
import instaloader

L = instaloader.Instaloader()
profile = instaloader.Profile.from_username(L.context, 'nome_do_perfil')

# Iterar sobre posts
for post in profile.get_posts():
    print(f"Data: {post.date}")
    print(f"Legenda: {post.caption}")
    print(f"Curtidas: {post.likes}")
    print(f"Comentários: {post.comments}")
    print(f"É vídeo: {post.is_video}")
    print(f"URL: {post.url}")
    print("---")
```

#### 6.5 Download apenas de foto de perfil

```python
import instaloader

L = instaloader.Instaloader()
L.download_profile('nome_do_perfil', profile_pic_only=True)
```

#### 6.6 Salvar metadados em JSON

```python
import instaloader
import json

L = instaloader.Instaloader()
profile = instaloader.Profile.from_username(L.context, 'nome_do_perfil')

# Criar dicionário com dados
dados = {
    'username': profile.username,
    'full_name': profile.full_name,
    'userid': profile.userid,
    'followers': profile.followers,
    'following': profile.followees,
    'biography': profile.biography,
    'is_verified': profile.is_verified,
    'is_private': profile.is_private,
    'is_business': profile.is_business_account,
    'posts_count': profile.mediacount,
    'external_url': profile.external_url
}

# Salvar em JSON
with open('perfil_dados.json', 'w', encoding='utf-8') as f:
    json.dump(dados, f, ensure_ascii=False, indent=4)
```

### 7. Interpretação dos resultados

#### 7.1 Estrutura de arquivos baixados

Após o download, o Instaloader cria a seguinte estrutura:

```
nome_do_perfil/
├── 2024-05-24_12-34-56_UTC.jpg         # Post (imagem)
├── 2024-05-24_12-34-56_UTC.txt         # Legenda do post
├── 2024-05-24_12-34-56_UTC.json.xz     # Metadados (compactado)
├── 2024-05-24_12-34-56_UTC_comments.json  # Comentários
├── profile_pic.jpg                      # Foto de perfil
└── id                                   # ID numérico do perfil
```

#### 7.2 Conteúdo do arquivo JSON

O arquivo JSON contém metadados completos:

```json
{
  "node": {
    "id": "123456789",
    "shortcode": "AbCdEfG",
    "display_url": "https://...",
    "owner": {
      "id": "987654321",
      "username": "nome_do_perfil"
    },
    "edge_media_to_caption": {
      "edges": [
        {
          "node": {
            "text": "Texto da legenda..."
          }
        }
      ]
    },
    "edge_media_to_comment": {
      "count": 42
    },
    "edge_liked_by": {
      "count": 1500
    },
    "taken_at_timestamp": 1716556496,
    "location": {
      "id": "123456789",
      "name": "Nome do Local"
    }
  }
}
```

#### 7.3 O que cada campo significa

- **id**: Identificador único do post
- **shortcode**: Código curto usado na URL do post
- **display_url**: URL da imagem/vídeo
- **owner**: Dados do proprietário (ID e username)
- **edge_media_to_caption**: Legenda completa do post
- **edge_media_to_comment**: Total de comentários
- **edge_liked_by**: Total de curtidas
- **taken_at_timestamp**: Data/hora de publicação (Unix timestamp)
- **location**: Dados de geolocalização (se disponível)

### 8. Exportação e documentação de dados

#### 8.1 Organização de evidências

**Estrutura recomendada:**

```
investigacao_AAAA-MM-DD/
├── perfis/
│   ├── perfil_alvo/
│   └── perfis_relacionados/
├── hashtags/
│   └── #hashtag_relevante/
├── relatorios/
│   ├── metadados_consolidados.json
│   ├── analise_temporal.csv
│   └── relatorio_final.pdf
└── logs/
    └── execucao_AAAA-MM-DD.log
```

#### 8.2 Automatização de backup

```bash
#!/bin/bash
# Script de backup automatizado

DATA=$(date +%Y-%m-%d)
PERFIS=("perfil1" "perfil2" "perfil3")

for PERFIL in "${PERFIS[@]}"; do
    instaloader --login usuario_osint --fast-update --stories --highlights "$PERFIL"
    echo "[$DATA] Backup de $PERFIL concluído" >> backup.log
done
```

### 9. Limitações técnicas e operacionais

#### 9.1 Rate limiting do Instagram

- Instagram aplica limites de requisições por IP e por conta
- Downloads muito rápidos podem resultar em bloqueios temporários (429 Too Many Requests)
- Use `--sleep-on-download` para adicionar delays

#### 9.2 Detecção de automação

- Instagram pode identificar comportamento automatizado
- Contas podem ser temporariamente suspensas ou bloqueadas
- Use contas secundárias dedicadas para OSINT

#### 9.3 Conteúdo privado

- Perfis privados requerem autenticação e que você siga a conta
- Stories e highlights de contas privadas não são acessíveis sem permissão
- DMs nunca são acessíveis

#### 9.4 Mudanças na plataforma

- Instagram frequentemente altera APIs e estruturas internas
- Atualizações do Instaloader podem ser necessárias
- Algumas funcionalidades podem parar temporariamente após mudanças

### 10. Resolução de problemas comuns

#### Erro: "Login error: Bad credentials"

- Verifique usuário e senha
- Confirme que a conta não está bloqueada
- Tente fazer login manual no navegador
- Verifique se 2FA está ativado

#### Erro: "429 Too Many Requests"

```bash
# Adicionar delay entre downloads
instaloader --sleep-on-download 3 nome_do_perfil
```

#### Erro: "Checkpoint required"

- Instagram solicitou verificação de segurança
- Faça login manual no navegador e complete o checkpoint
- Aguarde algumas horas antes de tentar novamente

#### Erro: "Profile not found"

- Verifique se o nome de usuário está correto
- Confirme que a conta ainda existe
- Perfil pode ter sido deletado ou renomeado

#### Download interrompido

```bash
# Instaloader retoma automaticamente
instaloader nome_do_perfil
```

#### Atualizar Instaloader para corrigir bugs

```bash
pip3 install --upgrade instaloader
```

### 11. Exemplo completo de fluxo de trabalho

#### 11.1 Investigação básica de perfil

```bash
# 1. Instalar Instaloader
pip3 install instaloader

# 2. Download inicial de perfil público
instaloader nome_do_perfil

# 3. Download com dados completos
instaloader --comments --geotags --stories --highlights nome_do_perfil

# 4. Login para perfil privado
instaloader --login usuario_osint nome_do_perfil_privado

# 5. Atualização periódica
instaloader --login usuario_osint --fast-update nome_do_perfil
```

#### 11.2 Script Python para análise automatizada

```python
import instaloader
import json
from datetime import datetime

# Configuração
L = instaloader.Instaloader(
    download_comments=True,
    download_geotags=True,
    compress_json=False
)

# Login
L.login('usuario_osint', 'senha_segura')

# Carregar perfil
profile = instaloader.Profile.from_username(L.context, 'perfil_alvo')

# Coletar metadados
dados_perfil = {
    'data_coleta': datetime.now().isoformat(),
    'username': profile.username,
    'full_name': profile.full_name,
    'userid': profile.userid,
    'seguidores': profile.followers,
    'seguindo': profile.followees,
    'biografia': profile.biography,
    'verificado': profile.is_verified,
    'privado': profile.is_private,
    'comercial': profile.is_business_account,
    'total_posts': profile.mediacount,
    'url_externa': profile.external_url
}

# Analisar posts recentes (últimos 10)
posts_dados = []
for post in profile.get_posts():
    if len(posts_dados) >= 10:
        break
    posts_dados.append({
        'data': post.date.isoformat(),
        'legenda': post.caption,
        'curtidas': post.likes,
        'comentarios': post.comments,
        'tipo': 'video' if post.is_video else 'imagem',
        'url': post.url
    })

# Salvar relatório
relatorio = {
    'perfil': dados_perfil,
    'posts_recentes': posts_dados
}

with open(f'relatorio_{profile.username}.json', 'w', encoding='utf-8') as f:
    json.dump(relatorio, f, ensure_ascii=False, indent=4)

print(f"Relatório salvo: relatorio_{profile.username}.json")
```

#### 11.3 Monitoramento de hashtag

```bash
# Coletar posts de hashtag específica
instaloader "#compliance" --count 100

# Com filtro de data (últimos 30 dias)
instaloader --post-filter="date_utc >= datetime.now() - timedelta(days=30)" "#compliance"
```

# Comparação entre as ferramentas

## Visão geral

| Ferramenta   | Foco principal                                      | Escopo de dados                  | Interface              | Nível de complexidade | Licença / Custo                     |
|-------------|------------------------------------------------------|----------------------------------|------------------------|-----------------------|--------------------------------------|
| Toutatis    | Extração de metadados públicos de perfis Instagram   | Instagram (perfil e contatos)    | CLI (linha de comando) | Baixo                  | Open source, gratuito                |
| Osintgram   | Análise estrutural e interativa de perfis Instagram  | Instagram (perfil, rede, mídia)  | CLI interativa         | Médio                  | Open source, gratuito                |
| Instaloader | Coleta massiva de mídia e metadados do Instagram     | Instagram (mídia + metadados)    | CLI + biblioteca Python| Médio                  | Open source, gratuito (MIT)         |


## Quando usar cada uma

- **Toutatis**: adequado para checagens rápidas de exposição de contas específicas, obtendo visão imediata de metadados e contatos públicos.
- **Osintgram**: ideal para investigações mais aprofundadas de um perfil, com comandos interativos que exploram rede, engajamento e padrões de conteúdo.
- **Instaloader**: indicado para coleta forense e arquivamento de grande volume de posts, stories, reels e metadados, com possibilidade de automação em scripts.

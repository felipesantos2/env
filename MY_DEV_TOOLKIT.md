# My Dev Toolkit

Ferramentas úteis para desenvolvimento web com Laravel, terminal, Git, APIs e análise de código.

---

## Busca e Navegação

### `rg` / ripgrep

Busca texto em arquivos de forma rápida, respeitando `.gitignore` por padrão. É um `grep` mais moderno para projetos de código.

Link: <https://github.com/BurntSushi/ripgrep>

```bash
rg "valor_total_devido"
rg -n "timeline" app resources routes tests
```

---

### `grep`

Busca texto em arquivos. É mais antigo, mais universal e quase sempre disponível em qualquer Linux.

Link: <https://www.gnu.org/software/grep/>

```bash
grep -Rni "timeline" app resources routes tests
```

Use quando estiver em um ambiente mínimo onde `rg` não existe.

---

### `fd`

Alternativa moderna ao `find`. Serve para encontrar arquivos e diretórios com sintaxe mais simples.

Link: <https://github.com/sharkdp/fd>

```bash
fd TaxDebit
fd ".blade.php" resources/views
```

No Ubuntu, o binário pode ser instalado como `fdfind`.

---

### `fzf`

Busca fuzzy interativa. Muito útil para escolher arquivos, comandos do histórico, branches e resultados de outros comandos.

Link: <https://github.com/junegunn/fzf>

```bash
git branch | fzf
fd . | fzf
history | fzf
```

---

### `zoxide`

Substitui o uso repetitivo de `cd`. Ele aprende os diretórios que você acessa e permite pular para eles rapidamente.

Link: <https://www.zoxide.org/>

```bash
z obras3
z docs
zi tax
```

---

## Leitura e Listagem

### `bat`

Alternativa ao `cat` com syntax highlight, numeração de linhas e integração com Git.

Link: <https://github.com/sharkdp/bat>

```bash
bat routes/web.php
bat -n app/Models/TaxDebit.php
```

No Ubuntu, pode aparecer como `batcat`.

---

### `eza`

Alternativa moderna ao `ls`, com melhor visualização de permissões, ícones, Git status e árvore.

Link: <https://eza.rocks/>

```bash
eza -la
eza --tree --level=2
eza -la --git
```

---

### `tree`

Mostra estrutura de pastas em árvore.

Link: <https://mama.indstate.edu/users/ice/tree/>

```bash
tree -L 2
tree app/Livewire -L 3
```

---

## HTTP, APIs e JSON

### `curl`

Cliente HTTP muito flexível. Excelente para testar APIs, baixar conteúdo, inspecionar headers e montar requisições detalhadas.

Link: <https://curl.se/>

```bash
curl -L https://example.com
curl -I https://example.com
curl -H "Accept: application/json" https://api.github.com
```

Use quando precisar de controle fino da requisição.

---

### `wget`

Ferramenta forte para baixar arquivos. Também faz requisições HTTP, mas seu foco principal é download, espelhamento e retomada.

Link: <https://www.gnu.org/software/wget/>

```bash
wget https://example.com/file.zip
wget -c https://example.com/big-file.zip
wget --mirror https://example.com/docs
```

Diferença prática:

```text
curl: melhor para testar e compor requisições HTTP/API.
wget: melhor para baixar arquivos e espelhar conteúdo.
```

---

### `HTTPie`

Cliente HTTP mais legível que `curl`, pensado para APIs. Tem saída colorida e JSON amigável.

Link: <https://httpie.io/cli>

```bash
http GET https://api.github.com
http POST https://example.com/api/users name=Felipe
```

Use quando quiser testar APIs com menos sintaxe.

---

### `jq`

Processa JSON no terminal. Essencial para ler respostas de APIs e filtrar dados.

Link: <https://github.com/jqlang/jq>

```bash
curl -s https://api.github.com/repos/laravel/framework | jq ".stargazers_count"
cat response.json | jq ".data[] | .name"
```

---

## Git e GitHub

### `git`

Controle de versão.

Link: <https://git-scm.com/>

```bash
git status --short
git diff
git log --oneline --graph --decorate -10
```

---

### `gh`

CLI oficial do GitHub. Permite trabalhar com PRs, issues, Actions e releases sem sair do terminal.

Link: <https://docs.github.com/en/github-cli/github-cli>

```bash
gh auth status
gh pr list
gh pr view --web
gh run list
```

---

### `lazygit`

Interface terminal para Git. Ajuda muito com staging parcial, logs, branches, stash e rebase.

Link: <https://lazygit.dev/>

```bash
lazygit
```

Use dentro de um repositório Git.

---

## Ajuda e Aprendizado

### `tldr`

Mostra exemplos práticos de comandos. É mais direto que `man` para uso diário.

Link: <https://tldr.sh/>

```bash
tldr tar
tldr curl
tldr git rebase
```

---

### `cheat.sh`

Consulta rápida de exemplos via terminal ou navegador.

Link: <https://cheat.sh/>

```bash
curl cheat.sh/tar
curl cheat.sh/php/date
curl cheat.sh/laravel/artisan
```

---

## Automação de Projeto

### `make`

Ferramenta clássica para automatizar comandos. Muito comum em projetos antigos e ambientes Unix.

Link: <https://www.gnu.org/software/make/>

```bash
make test
make build
```

---

### `just`

Command runner moderno e mais simples que `make`. Bom para criar atalhos de comandos do projeto.

Link: <https://github.com/casey/just>

```bash
just test
just pint
just build
```

Exemplo de `justfile`:

```make
test:
    ./vendor/bin/sail artisan test --compact

pint:
    ./vendor/bin/sail pint --dirty --format agent

build:
    ./vendor/bin/sail npm run build
```

---

## Banco e Debug Local

### `sqlite3`

Cliente SQLite no terminal. Útil para inspecionar bancos locais e bancos de teste.

Link: <https://www.sqlite.org/cli.html>

```bash
sqlite3 database/database.sqlite
.tables
.schema users
```

---

## Instalação Base no WSL

```bash
sudo apt update
sudo apt install ripgrep jq curl wget git gh fzf bat fd-find eza zoxide tldr tree sqlite3
```

Ferramentas que talvez exijam outro método de instalação:

```text
lazygit
httpie
just
```

---

## Ordem Recomendada Para Aprender

1. `grep`, `rg`, `fd`
2. `cat`, `bat`, `less`, `tree`, `eza`
3. `curl`, `wget`, `HTTPie`, `jq`
4. `git`, `gh`, `lazygit`
5. `fzf`, `zoxide`
6. `make`, `just`

---

## Kit Mínimo Diário

```text
rg      procurar no projeto
fd      achar arquivos
bat     ler arquivos
eza     listar pastas
curl    testar HTTP/API
jq      ler JSON
git     versionamento
gh      GitHub no terminal
fzf     seleção interativa
zoxide  navegação rápida
```

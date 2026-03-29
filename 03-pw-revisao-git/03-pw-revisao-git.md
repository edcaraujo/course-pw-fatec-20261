---
marp: true

author: "Eduardo Cruz Araujo"
title: "Programação Web"
description: "Disciplina de Programação Web."

theme: "default"
class: "invert"

footer: "Eduardo Cruz Araujo | Fatec | 2026.1 | Programação Web | Revisão: Git"

paginate: "true"

---

# Programação Web :mortar_board:
## Revisão: Git

---

Revisão: Git
## Introdução

---

> **Git** é o Sistema de Controle de Versão mais popular do mundo.

---

> **Linus Torvalds**, o criador do kernel Linux, desenvolveu o Git para gerenciar o desenvolvimento do kernel Linux

---

## Por que Git?

- **Trabalho em Equipe:** Permite que múltiplos desenvolvedores trabalhem no mesmo projeto sem sobrescrever o trabalho um do outro.
- **Histórico Completo:** Cada alteração é registrada. Você pode voltar no tempo para corrigir um bug ou entender uma decisão.
- **Segurança:** Se você estragar tudo, pode facilmente reverter para uma versão estável.
- **Ramificações (Branches):** Permite desenvolver novas funcionalidades de forma isolada, sem afetar a versão principal do projeto.

---

## Estágios

Todo o seu trabalho local em Git reside em três "árvores" ou estágios.

1.  **Working Directory (Área de Trabalho):** Onde você cria e edita seus arquivos. É a sua pasta de projeto.
2.  **Staging Area (Área de Preparação):** Um "rascunho" do seu próximo *commit*. Você adiciona aqui as mudanças que quer salvar.
3.  **Repository (Repositório - `.git`):** Onde o Git armazena permanentemente o histórico de todas as versões (commits).

---

## Estágios

```
Working Directory --> Staging Area --> Repository
     (git add)       (git commit)
```

---

Revisão: Git
## Hello 'Git' World!

---

## Configuração

```bash
# Configura seu nome de usuário
git config --global user.name "Seu Nome"

# Configura seu e-mail
git config --global user.email "seu.email@exemplo.com"
```

O `--global` faz com que essa configuração seja válida para todos os seus projetos.

---

## Versionamento

**Inicialize um repositório** em uma pasta existente ou nova.
```bash
git init
```

---

## Versionamento

**Adicione arquivos** à *Staging Area*.
```bash
# Adiciona um arquivo específico
git add nome_do_arquivo.js

# Adiciona todos os arquivos modificados/novos
git add .
```

---

## Versionamento

**Salve as mudanças** no repositório com um *commit*.
```bash
git commit -m "Mensagem clara e descritiva do que foi feito"
```

---

## Verificações

Como saber o que está acontecendo?

```bash
# Mostra o status do Working Directory e da Staging Area
# (quais arquivos foram modificados, quais estão em staging, etc)
git status

# Mostra o histórico de commits
git log

# Uma versão mais bonita e compacta do log
git log --oneline --graph --decorate
```

---

## Branches

Branches (ramificações) são como universos paralelos do seu projeto. Você pode criar uma nova *branch* para trabalhar em uma funcionalidade sem afetar a linha principal (`main` ou `master`).

---

## Branches

```bash
# Lista todas as branches locais
git branch

# Cria uma nova branch chamada "nova-feature"
git branch nova-feature

# Muda para a branch "nova-feature"
git checkout nova-feature

# Atalho: cria e já muda para a nova branch
git checkout -b outra-feature
```
---

## Remotos (GitHub, GitLab, etc.)

```bash
# Clona um repositório existente da internet para sua máquina
git clone <url_do_repositorio>

# Adiciona um repositório remoto a um projeto local já existente
git remote add origin <url_do_repositorio>

# Envia seus commits para o repositório remoto
# -u define o "upstream" para pushes/pulls futuros
git push -u origin main

# Baixa as atualizações do repositório remoto
git pull
```

---

## Remotos (GitHub, GitLab, etc.)

`git pull` é, na verdade, uma combinação de `git fetch` (baixa as mudanças) + `git merge` (junta com seu trabalho local).

---

## Merge

Depois de terminar sua funcionalidade na *branch*, você vai querer juntá-la (fazer o *merge*) com a *branch* principal.

```bash
# 1. Volte para a branch principal (destino)
git checkout main

# 2. Traga as mudanças da sua branch de feature
git merge nova-feature
```

---

## Merge


**E se houver conflitos?** O Git avisará se a mesma linha de código foi alterada em ambas as branches. Você precisará editar o arquivo manualmente para resolver o conflito e depois fazer um novo *commit*.

---


## Rebase

Enquanto `merge` cria um "commit de junção", o `rebase` move seus commits para o topo da branch principal, criando um histórico linear e limpo.

**Cuidado:** **NUNCA** use `rebase` em branches públicas/compartilhadas (`main`, `develop`). Isso reescreve o histórico e pode causar um caos imenso para seus colegas. Use apenas em suas branches locais de feature.

---

## Rebase

```bash
git rebase main
```

---

## Stash

Precisa mudar de branch, mas seu trabalho atual não está pronto para um commit? O `git stash` guarda suas modificações não "commitadas" temporariamente em uma "pilha".

```bash
# Salva as mudanças atuais no stash
git stash

# Aplica as últimas mudanças do stash e as remove da pilha
git stash pop

# Lista o que está no stash
git stash list

# Aplica uma mudança específica sem remover da pilha
git stash apply stash@{2}
```

---

## Reset

- **`git reset <commit>`**: **Move o ponteiro** da sua branch para um commit anterior, "esquecendo" os commits que vieram depois.
    - `reset --soft`: Mantém as mudanças na Staging Area.
    - `reset --mixed` (padrão): Mantém as mudanças no Working Directory.
    - `reset --hard`: **Descarta todas as mudanças**. CUIDADO!

---

##  Revert

- **`git revert <commit>`**: **Cria um novo commit** que é o exato oposto do commit que você quer desfazer.
    - Não reescreve o histórico, apenas adiciona um novo registro.
    - **É a forma segura** de desfazer algo em uma branch pública (`main`, `develop`).

---

## Cherry-pick

O comando `git cherry-pick` permite que você aplique um commit específico de uma branch em outra.

*É como "copiar e colar" um commit.*

**Quando usar?**
Imagine que você corrigiu um bug urgente na branch `main`, mas essa correção também é necessária na branch `develop`. Em vez de fazer um merge completo, você pode "pinçar" apenas o commit da correção.

---

## Cherry-pick

```bash
# 1. Mude para a branch que vai receber o commit
git checkout develop

# 2. Aplique o commit desejado usando seu hash
git cherry-pick <hash_do_commit_da_correcao>
```

**Importante:** O `cherry-pick` cria um *novo* commit na branch de destino com as mesmas alterações. O hash do commit será diferente.

---

## Reflog

O `reflog` é a sua rede de segurança definitiva. Ele registra (quase) todas as movimentações do `HEAD` na sua máquina local.

### Quando usar?
- Quando você "perde" um commit (ex: após um `reset --hard`).
- Quando você quer restaurar um estado anterior do seu repositório que não está mais no histórico visível da branch.

---

## Tagging

Tags são usadas para marcar pontos específicos no histórico como importantes, geralmente para marcar versões de lançamento (`v1.0.0`, `v2.0-beta`).

- **Annotated Tags (Tags Anotadas):** Recomendado. São objetos completos no Git, contêm o nome do autor da tag, e-mail, data e uma mensagem.
- **Lightweight Tags (Tags Leves):** Apenas um ponteiro para um commit.

---

## Tagging

```bash
# Cria uma tag anotada
git tag -a v1.0 -m "Lançamento da versão 1.0"

# Cria uma tag leve
git tag v1.0-leve

# Envia as tags para o repositório remoto
git push origin --tags
```

---

## Blame (Quem Foi?)

O comando `git blame` mostra, para cada linha de um arquivo, qual foi o último commit que a modificou e quem foi o autor.

É extremamente útil para entender o contexto de uma linha de código: por que ela existe? Quem a escreveu?

```bash
# Exibe o "blame" para um arquivo específico
git blame caminho/para/o/arquivo.js

# -L limita a um intervalo de linhas
git blame -L 10,20 caminho/para/o/arquivo.js
```
Apesar do nome "culpa", a intenção é mais investigativa do que acusatória.

---

## Submodules (Submódulos)

Submódulos permitem que você mantenha um repositório Git como um subdiretório de outro repositório Git.

Isso é útil quando você quer usar um projeto externo dentro do seu projeto, mas quer manter os históricos de ambos separados.

```bash
# Adiciona um novo submódulo
git submodule add <url_do_repositorio_externo> caminho/para/a_pasta

# Para clonar um projeto com submódulos
git clone --recurse-submodules <url_do_projeto_principal>

# Para inicializar e atualizar os submódulos após clonar
git submodule update --init --recursive
```

---

## Archive (Arquivamento)

O comando `git archive` cria um arquivo compactado (`.zip` ou `.tar.gz`) de uma branch, commit ou tag específica do seu repositório.

É uma ótima maneira de criar um pacote de distribuição do seu código-fonte sem incluir todo o histórico do Git (a pasta `.git`).

```bash
# Cria um .zip da branch main
git archive --format=zip --output=meu_projeto.zip main

# Cria um .tar.gz de uma tag específica
git archive --format=tar.gz --output=versao-1.0.tar.gz v1.0
```

---

## GC (Garbage Collection)

O Git acumula muitos "objetos soltos" (commits que não são mais referenciados, etc.) durante o uso normal. O `git gc` (Garbage Collector - Coletor de Lixo) limpa esses objetos desnecessários e otimiza o repositório local.

Geralmente, o Git executa esse comando automaticamente quando necessário, mas você pode executá-lo manualmente.

```bash
# Executa o coletor de lixo
git gc

# Opção mais agressiva
git gc --aggressive
```
**É um comando de manutenção.**

---

## Reflog

```bash
# Mostra o histórico de movimentações do HEAD
git reflog

# Exemplo: para restaurar um commit perdido
git reset --hard HEAD@{5}
```
**É um registro local, não é compartilhado no push.**

---

## Bisect 

O `git bisect` é uma ferramenta poderosa para encontrar qual commit introduziu um bug no projeto. Ele faz uma busca binária no seu histórico de commits.

Você informa um commit "ruim" (com o bug) e um commit "bom" (sem o bug), e o `bisect` te guiará, perguntando a cada passo se o bug está presente, até isolar o commit culpado.

---

```bash
# Inicia o processo
git bisect start

# Informa o commit com bug (ex: o mais recente)
git bisect bad HEAD

# Informa o último commit bom conhecido
git bisect good <hash_do_commit_bom>

# O Git fará checkout de um commit no meio. Teste e informe:
git bisect good # se não tiver o bug
git bisect bad  # se tiver o bug

# Ao final, o Git apontará o commit culpado. Saia do bisect:
git bisect reset
```

---

Revisão: Git
## Estratégias de Branching

---

Uma "estratégia de branching" é um conjunto de regras e convenções que uma equipe de desenvolvimento segue para usar branches no Git.

Escolher uma boa estratégia ajuda a:
- Organizar o desenvolvimento de novas features.
- Facilitar a correção de bugs.
- Manter uma versão estável (produção) do código.
- Gerenciar diferentes versões do software simultaneamente.

---

## Feature Branching

- **Conceito:** Cada nova funcionalidade (`feature`) é desenvolvida em sua própria branch, separada da principal (`main`).
- **Fluxo:**
    1. Crie uma nova branch a partir da `main` (ex: `feature/login-social`).
    2. Desenvolva, faça commits.
    3. Abra um *Pull Request* (ou *Merge Request*) quando a feature estiver pronta.
    4. Após a revisão e aprovação, faça o *merge* da branch de feature de volta para a `main`.
- **Vantagem:** Simples e eficaz para isolar trabalhos. É a base da maioria das outras estratégias.

---

## Git Flow

- **Conceito:** Uma estratégia mais rígida com branches de longa duração e papéis bem definidos. Popularizada por Vincent Driessen.
- **Branches principais:**
    - **`main` (ou `master`):** Código de produção. Só recebe merges da `develop` e de `hotfix`. Marcada com tags de versão.
    - **`develop`:** Branch de integração para as features. É a "verdade" do próximo lançamento.

---

## Git Flow

- **Branches de suporte:**
    - **`feature/*`:** Saem da `develop` e voltam para a `develop`.
    - **`release/*`:** Saem da `develop` para preparar um novo lançamento (testes finais, etc.). Voltam para `develop` e `main`.
    - **`hotfix/*`:** Saem da `main` para corrigir bugs urgentes em produção. Voltam para `develop` e `main`.

---

## GitLab Flow

- **Conceito:** Uma simplificação do GitFlow, mais adequada para integração e entrega contínuas (CI/CD).
- **Fluxo:**
    - A branch **`main`** é o ponto de partida e destino final.
    - O trabalho é feito em **`feature-branches`**.
    - **Ambientes:** Utiliza branches para representar ambientes. Por exemplo, ao fazer merge na `main`, o deploy é feito para *staging*. Ao fazer merge da `main` para uma branch `production`, o deploy é feito para produção.
- **Vantagem:** Mais simples que o GitFlow e integra-se bem com pipelines de CI/CD e múltiplos ambientes.

---

## GitHub Flow

- **Conceito:** Uma estratégia ainda mais simples, popularizada pelo GitHub.
- **Regras:**
    1. Qualquer coisa na branch `main` é "deployable" (pode ir para produção).
    2. Para trabalhar em algo novo, crie uma branch descritiva a partir da `main`.
    3. Faça commits nessa branch e envie regularmente para o remoto.
    4. Quando precisar de feedback ou ajuda, ou quando a feature estiver pronta, abra um *Pull Request*.
    5. Depois que o Pull Request for revisado e aprovado, ele é mesclado na `main`.
    6. Uma vez na `main`, o código deve ser imediatamente implantado em produção.

---

## GitHub Flow

- **Vantagem:** Muito simples, rápido e focado em entrega contínua.

---

## Trunk-Based Development (TBD)

- **Conceito:** Os desenvolvedores colaboram em uma única branch chamada "trunk" (`main` ou `master`).
- **Fluxo:**
    - Desenvolvedores fazem commits pequenos e frequentes diretamente no `trunk`.
    - Se branches são usadas, elas são de vida muito curta (no máximo algumas horas/dias) e são integradas rapidamente.
    - Depende fortemente de *feature flags* (ou *feature toggles*) para gerenciar funcionalidades incompletas sem quebrar o build.

---

## Trunk-Based Development (TBD)

- **Vantagem:** Evita a complexidade de gerenciar muitos merges e branches, promovendo uma integração verdadeiramente contínua. Exige uma suíte de testes automatizados muito robusta.

---

Revisão: Git
## Extra

---

## O Arquivo `.gitignore`

Nem tudo deve ir para o repositório. Arquivos de configuração de IDE, dependências (`node_modules`), arquivos de build e senhas **NÃO** devem ser versionados.

Crie um arquivo chamado `.gitignore` na raiz do seu projeto e liste os arquivos e pastas a serem ignorados.

---

## O Arquivo `.gitignore`

```.gitignore
# Ignorar dependências do Node.js
node_modules/

# Ignorar arquivos de log
*.log

# Ignorar arquivos de ambiente (que podem conter senhas)
.env
```

Existem templates prontos para a maioria das linguagens em github.com/github/gitignore.

---

## Conventional Commits

Um padrão para escrever mensagens de commit claras e que podem ser lidas por máquinas. Ajuda a automatizar a geração de changelogs e o versionamento.

**Formato:** `<tipo>(escopo opcional): <descrição>`

- **`feat`**: Uma nova funcionalidade (feature).
- **`fix`**: Uma correção de bug.
- **`docs`**: Mudanças na documentação.

---

## Conventional Commits

- **`style`**: Mudanças de formatação, sem alterar a lógica (ponto e vírgula, etc).
- **`refactor`**: Refatoração de código, sem adicionar features ou corrigir bugs.
- **`test`**: Adição ou correção de testes.
- **`chore`**: Atualização de tarefas de build, pacotes, etc.

---

# Obrigado :metal:

---

## Eduardo Cruz Araujo

- E-mail: [eduardo.araujo28@fatec.sp.gov.br](eduardo.araujo28@fatec.sp.gov.br)
- Linkedin: [edcaraujo](https://www.instagram.com/)
- Github: [edcaraujo](https://github.com/edcaraujo)
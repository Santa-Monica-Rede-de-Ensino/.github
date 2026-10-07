# Guia GitHub do time

Como a equipe de sistemas da Santa Mônica trabalha junto no GitHub, de graça.
Base: GitHub Flow (doc oficial do GitHub) e Conventional Commits.
Nomes dos botões conferidos em outubro de 2026.

---

## Resumo: uma tarefa do início ao fim

Primeira vez? Faça antes o [passo 0](#0-prepare-o-pc-uma-vez-só). Palavra estranha? [Palavras](#palavras). Clique no passo para ver
o exemplo completo.

| # | Faça | Onde | Como |
|---|---|---|---|
| 1 | [Anote a tarefa](#1-anote-a-tarefa-issue) | site | **Issues** > **New issue** > **Create**.<br>O GitHub dá o número: #12 |
| 2 | [Crie sua branch](#2-crie-sua-branch) | terminal | `git switch main`<br>`git pull`<br>`git switch -c feat/12-cadastro-alunos` |
| 3 | [Edite os arquivos e salve](#3-edite-e-salve-commit) | editor, depois terminal | `git add alunos.js`<br>`git commit -m "feat(alunos): adiciona cadastro"` |
| 4 | [Envie para o GitHub](#4-envie-push) | terminal | `git push -u origin feat/12-cadastro-alunos` |
| 5 | [Peça revisão](#5-peça-revisão-pull-request) | site | **Compare & pull request**.<br>No texto, escreva `Closes #12` |
| 6 | [Junte na main, depois do OK](#6-junte-squash-and-merge) | site | **Squash and merge** > **Confirm** |
| 7 | [Limpe o PC](#7-limpe-o-pc) | terminal | `git switch main`<br>`git pull`<br>`git branch -D feat/12-cadastro-alunos` |

Troque `12`, `cadastro-alunos`, `alunos` e o nome do arquivo pelos seus. Outros tipos além de `feat`:
[Nomes](#nomes-e-números).

---

## Palavras

| Palavra | O que é |
|---|---|
| **Repo** | A pasta do projeto, com todo o histórico. |
| **Commit** | Um ponto salvo na história: "aqui eu mudei isto". |
| **Stage** | A sacola do próximo commit. `git add` põe arquivo na sacola. |
| **Branch** | Uma cópia paralela para trabalhar sem mexer na main. |
| **main** | A branch principal. O código que funciona. |
| **Push** | Mandar seus commits do PC para o GitHub. |
| **Pull** | Trazer do GitHub o que os colegas mandaram. |
| **Issue** | Uma tarefa escrita no GitHub (#12, #13...). |
| **Pull Request (PR)** | O pedido: "revisem minha branch e juntem na main". |
| **Review** | Um colega lê o PR e aprova ou pede ajuste. |
| **Merge** | Juntar uma branch em outra. |
| **Squash** | Merge que transforma todos os commits da branch em 1 só. |
| **Conflito** | Duas pessoas mudaram a mesma linha. O git pergunta qual fica. |

---

## Passo a passo, com exemplo

**Cenário:** sistema **Escola Fácil**, na organização `Santa-Monica-Rede-de-Ensino`. Time: Dev A,
Dev B e Dev C. Repo privado, plano grátis.

### 0. Prepare o PC (uma vez só)

**Dev A, no site:**

1. Na organização, **New repository**: `escola-facil`, privado, com README e `.gitignore`.
   Na descrição (*About*), comece pelo nome do sistema: "Escola Fácil – cadastro de alunos". É
   esse nome que aparece no Trello.
2. Settings > General > Pull Requests: deixa só **Allow squash merging** e marca
   **Automatically delete head branches** (a branch some sozinha depois do merge).

Quem é da organização já enxerga o repo. Pessoa nova: o dono da organização convida em **People**
> **Invite member**.

📷 [convidar para a organização](https://docs.github.com/pt/organizations/managing-membership-in-your-organization/inviting-users-to-join-your-organization) ·
[squash](https://docs.github.com/pt/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests) ·
[apagar branch sozinha](https://docs.github.com/pt/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-the-automatic-deletion-of-branches)

**Todos, no PC:**

1. Instalam o Git: [git-scm.com](https://git-scm.com). No Windows, o terminal é o **Git Bash**.
2. Dizem ao Git quem são:
   ```bash
   git config --global user.name "Seu Nome"
   git config --global user.email "seu@email.com"
   ```
   Nos repos da escola, use o e-mail da escola, já confirmado na sua conta do GitHub
   (*Settings > Emails*): `git config user.email "voce@smrede.com.br"` dentro do repo.
3. Quem é novo aceita o convite da organização (e-mail ou sino do GitHub). Sem isso: "Repository
   not found".
4. Copiam a URL do repo (botão verde **Code** > **HTTPS**) e baixam:
   ```bash
   git clone https://github.com/Santa-Monica-Rede-de-Ensino/escola-facil.git
   cd escola-facil   # todo comando roda aqui dentro
   ```

No primeiro `git push`, o navegador pede login: entre com a conta do GitHub.

---

### 1. Anote a tarefa (issue)

No site: **Issues** > **New issue**. Escreva o título e o texto (modelo abaixo).

Na lateral direita:

- **Assignees** (quem faz a tarefa): clique e escolha você.
- **Labels** (etiqueta do tipo): `enhancement` se é coisa nova, `bug` se é erro.

Clique **Create**. O GitHub dá o número: #12.

Texto da issue:

```markdown
Título: Cadastro de alunos

## Objetivo
Permitir que a secretaria cadastre alunos.

## Critérios de aceite
- [ ] Formulário com nome, nascimento, matrícula e turma
- [ ] Matrícula não pode repetir

## Fora do escopo
- Edição e exclusão de aluno (outra issue)
```

- Critério de aceite: como saber que acabou.
- Fora do escopo: impede a tarefa de crescer sem fim.

Bug usa outro texto: **Como reproduzir** (passos), **Esperado** e **Atual**.

📷 [criar uma issue](https://docs.github.com/pt/issues/tracking-your-work-with-issues/using-issues/creating-an-issue)

### 2. Crie sua branch

```bash
git switch main                        # branch nova sempre nasce da main
git pull                               # traz o que os colegas juntaram
git switch -c feat/12-cadastro-alunos  # cria a branch e entra nela
```

Sem o `pull`, você começa de código velho e ganha conflito depois.

### 3. Edite e salve (commit)

Edite os arquivos no seu editor (VS Code, por exemplo). Depois:

```bash
git status                                         # o que mudou?
git add alunos.html alunos.js                      # só esses arquivos
git commit -m "feat(alunos): adiciona cadastro"    # salva um ponto
```

- Repita quantas vezes precisar. Um assunto por commit.
- `add` arquivo por arquivo evita subir senha ou lixo.

### 4. Envie (push)

```bash
git push -u origin feat/12-cadastro-alunos   # 1ª vez. Depois, só: git push
```

Envie todo dia, mesmo sem terminar: é backup, e o time vê o progresso.

### 5. Peça revisão (pull request)

No site: faixa amarela **Compare & pull request**. Não apareceu? **Pull requests** >
**New pull request** > sua branch em **compare**. Na lateral direita, **Reviewers** (quem revisa): escolha Dev B.

```markdown
Título: feat(alunos): adiciona cadastro de alunos

## O que foi feito
- Formulário de cadastro
- Validação de matrícula duplicada

## Como testar
1. Ir em Alunos > Novo
2. Salvar matrícula repetida: deve dar erro

## Como testei
Cadastrei a matrícula 2024001 duas vezes. Na segunda apareceu "Matrícula já existe".

Closes #12
```

- **Como testei**: o que você rodou e viu. Prova, não promessa. Não testou? "não verificado".
- `Closes #12` fecha a issue sozinho quando o PR entra.

Pediu ajuste? Corrija na mesma branch, `commit` e `git push`. O PR atualiza sozinho.

**Se você revisa** (aqui, Dev B):

1. Abra o PR > aba **Files changed**.
2. Confira: faz o que a issue pede? "Como testei" tem prova? Subiu senha ou arquivo estranho?
3. Dúvida numa linha: clique no **+** azul ao lado dela e comente.
4. **Review changes** > **Approve** (está ok) ou **Request changes** (precisa ajustar) >
   **Submit review**.

📷 [criar PR](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) ·
[revisar](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request)

### 6. Junte (squash and merge)

- Quem clica: você, o autor, **depois** do Approve. Projeto só seu: junta direto.
- No fim do PR: **Squash and merge** > **Confirm squash and merge**.
- Aparece **Merge pull request**? Clique na setinha ao lado e escolha Squash.
- A issue #12 fecha sozinha. A branch some do GitHub sozinha.

📷 [fazer o merge](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request)

### 7. Limpe o PC

```bash
git switch main
git pull                                # sua main agora tem o cadastro
git branch -D feat/12-cadastro-alunos   # apaga a branch do PC. Seguro: ela já está na main
```

Próxima tarefa: volte ao passo 1.

### Conflito (vai acontecer)

Dev B e Dev C mexeram no mesmo arquivo de menu. B juntou primeiro. O PR de C mostra
"This branch has conflicts". Dev C:

```bash
git switch main
git pull                     # pega o código do B
git switch feat/14-frequencia
git merge main               # traz o código do B. O git avisa: CONFLICT
```

No arquivo aparece:

```
<<<<<<< HEAD
Frequência
=======
Notas
>>>>>>> main
```

Em cima (`HEAD`), a sua versão. Embaixo, a da main. Deixe o certo (aqui, os dois), apague as
marcações e:

```bash
git add menu.html
git commit -m "fix(menu): resolve conflito com notas"
git push                     # o PR fica verde de novo
```

Quem resolve é quem chegou depois. A main nunca é mexida direto.

📷 [sobre conflitos](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)

---

## Por que não fazer tudo direto na main?

Sexta, 17h. Dev B manda um bug direto na main. Dev A e Dev C dão `pull`: agora ninguém entra
no sistema. Os três param para achar o erro. A apresentação para o cliente é segunda.

Com branch e PR, o bug ficaria na branch do B. O colega veria no review. A main continuaria
funcionando.

- Custa mais passos: uma tarefa de 1 minuto leva 5.
- Compensa quando algo dá errado. Com 3 pessoas, sempre dá.
- Projeto só seu, de estudo? Direto na main é aceitável. Mas treinar o fluxo te prepara para time.

---

## Nomes e números

**Número:** quem dá é o GitHub, na issue. Issue e PR dividem a contagem: issue #12, PR #13.
A branch copia o número da **issue**.

**Commit:** `tipo(escopo): descrição`

- **tipo**: o que a mudança é (tabela).
- **escopo**: a parte do sistema (`alunos`, `notas`). Opcional.
- **descrição**: verbo, minúscula, sem ponto: "adiciona", "corrige", "remove".

| Tipo | Quando | Exemplo |
|---|---|---|
| `feat` | coisa nova | `feat(alunos): adiciona cadastro` |
| `fix` | correção | `fix(notas): bloqueia nota acima de 10` |
| `docs` | documentação | `docs: atualiza README` |
| `refactor` | reorganiza sem mudar o que faz | `refactor(auth): simplifica login` |

Estes 4 cobrem quase tudo. Exceção, só quando nenhum deles descreve a mudança: `test` (só testes),
`ci` (só automação do GitHub), `chore` (só manutenção: dependência, configuração) e `revert` (desfaz
um commit).

**Branch:** tipo + número da issue + 2 ou 3 palavras: `feat/12-cadastro-alunos`,
`fix/15-nota-acima-de-10`. Em empresa, siga o padrão do time.

**PR:** título igual a um commit. Ele vira a mensagem na main depois do squash.

---

## Regras do time

1. Ninguém commita direto na main. Única exceção: `git revert` de um commit que caiu na main
   por engano ([Deu errado](#deu-errado-e-agora)), avisando o time.
2. Toda tarefa vira issue, com responsável.
3. Todo PR tem aprovação de **outra** pessoa.
4. Uma branch = uma tarefa pequena (até 1 dia).
5. `git pull` na main antes de criar branch.
6. `git status` antes de `git add`. Arquivo por arquivo.
7. `.gitignore` desde o 1º commit (`.env`, `node_modules`, `venv`).
8. Senha e chave nunca vão para o repo. Vazou? Troque a senha na hora: apagar o arquivo
   não tira ela do histórico.
9. Merge sempre com **Squash and merge**.

Revisão em rodízio: A revisa B, B revisa C, C revisa A.

Repo privado no plano grátis: o GitHub **não trava** a main nem obriga aprovação. Quem
garante as regras é o combinado entre vocês.

---

## Deu errado, e agora?

Primeiro, `git status`: mostra onde você está e o que mudou.

**Commitei na main, sem push:**

```bash
git switch -c feat/12-login     # cria a branch certa. O commit vai junto
git branch -f main origin/main  # volta a main do PC a ser igual à do GitHub
```

**Commitei na main e dei push:**

```bash
git revert --no-edit HEAD   # commit novo que desfaz o último
git push
```

Única vez que se mexe direto na main. Avise o time e refaça a mudança numa branch.

**Mexi na branch errada, sem commit:** `git switch -c feat/13-cadastro`. O que você mexeu vai junto.

**Quero desfazer o último commit, sem push:** `git reset --soft HEAD~1`. As mudanças voltam
para a sacola. Já deu push? Use `git revert`, nunca `reset`.

---

## Extras (quando se sentir confortável)

- **GitHub CLI (`gh`)**: issue e PR pelo terminal (`gh issue list`, `gh pr create`).
- **GitHub Actions**: roda os testes sozinho em todo PR e mostra ✅ ou ❌. No plano grátis
  privado ele avisa, mas não impede o merge.
- **Template de PR**: `.github/pull_request_template.md` abre o PR já com o modelo do passo 5.
- **CONTRIBUTING.md**: as [Regras do time](#regras-do-time) viram esse arquivo.
- **Versão (SemVer)**: `v1.4.0`. `fix` sobe o último número, `feat` o do meio, `!` o primeiro.

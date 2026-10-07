# Como contribuir

Vale para todos os repositórios da Santa Mônica. Repositório com `CONTRIBUTING.md` próprio
acrescenta o que é dele (ambiente, testes).

## Uma tarefa do início ao fim

| # | Faça | Como |
|---|---|---|
| 1 | Anote a tarefa | **Issues** > **New issue** > modelo *Tarefa* ou *Bug*. Escolha o responsável. O GitHub dá o número: #12 |
| 2 | Crie a branch a partir da main | `git switch main` · `git pull` · `git switch -c feat/12-cadastro-alunos` |
| 3 | Edite e salve | `git status` · `git add alunos.js` (arquivo por arquivo) · `git commit -m "feat(alunos): adiciona cadastro"` |
| 4 | Envie | `git push -u origin feat/12-cadastro-alunos` (todo dia, mesmo sem terminar) |
| 5 | Peça revisão | **Compare & pull request**. O modelo já vem com `Closes #12`. Escolha o revisor |
| 6 | Junte, depois do Approve | **Squash and merge** > **Confirm**. A issue fecha e a branch some sozinhas |
| 7 | Limpe o PC | `git switch main` · `git pull` · `git branch -D feat/12-cadastro-alunos` |

Quem revisa: **Files changed** > **Review changes** > **Approve** ou **Request changes** >
**Submit review**. Comentar não conta como aprovação.

## Nomes

- **Branch:** `tipo/N-descricao`, com o número da **issue**: `feat/12-cadastro-alunos`, `fix/15-nota-acima-de-10`.
- **Commit e título do PR:** `tipo(escopo): descricao`, verbo na 3ª pessoa, minúscula, sem ponto:
  `fix(notas): bloqueia nota acima de 10`.
- **Tipos:** `feat` (novo), `fix` (correção), `docs`, `refactor`, `test`, `chore`.

## Regras do time

1. Ninguém commita direto na `main`. Única exceção: `git revert` de um commit que caiu na `main`
   por engano, avisando o time.
2. Toda tarefa vira issue, com responsável.
3. Todo PR tem aprovação de outra pessoa.
4. Uma branch = uma tarefa pequena (até 1 dia).
5. `git pull` na `main` antes de criar branch.
6. `git status` antes de `git add`. Arquivo por arquivo.
7. `.gitignore` desde o 1º commit (`.env`, `node_modules`, `venv`).
8. Senha, token e chave nunca vão para o repositório. Vazou? Troque na hora: apagar o arquivo não
   tira o valor do histórico.
9. Merge sempre com **Squash and merge**.
10. Autoria só de pessoas: sem linha `Co-Authored-By` ou "Generated with" de ferramenta ou
    assistente de IA. No squash, apague essas linhas da mensagem antes de confirmar.

## Trello

O quadro "Desenvolvimento de Sistemas" acompanha o GitHub sozinho (de 15 em 15 min, dias úteis,
7h às 18h). Para o cartão andar, basta seguir os nomes acima:

- a branch tem o número da issue (`feat/12-...`);
- o PR tem `Closes #12`.

Repositório novo: escreva a descrição (*About*) começando pelo nome do sistema, por exemplo
"Matrícula Online – rematrícula pelo site". A etiqueta aparece sozinha no quadro.

# Como contribuir

Vale para todos os repositórios da Santa Mônica. Repositório com `CONTRIBUTING.md` próprio
acrescenta o que é dele (ambiente, testes).

**Passo a passo, com exemplo:** [guia GitHub do time](docs/guia-github.md). Resumo: issue →
branch → commits → PR com `Closes #N` → revisão de outra pessoa → **Squash and merge**.

## Nomes

- **Branch:** `tipo/N-descricao`, com o número da **issue**: `feat/12-cadastro-alunos`.
- **Commit e título do PR:** `tipo(escopo): descricao`, verbo na 3ª pessoa, minúscula, sem ponto:
  `fix(notas): bloqueia nota acima de 10`.
- **Tipos:** `feat` (novo), `fix` (correção), `docs`, `refactor`. Exceção, só quando nenhum
  deles descreve: `test` (só testes), `ci` (só automação do GitHub), `chore` (só manutenção) e
  `revert`. Na dúvida, `feat` ou `fix`.

## Regras do time

1. Ninguém commita direto na `main`. Única exceção: `git revert` de um commit que caiu na `main`
   por engano, avisando o time.
2. Toda tarefa vira issue, com responsável.
3. Todo PR tem aprovação de outra pessoa (**Review changes** > **Approve**; comentar não conta).
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
7h às 18h). O cartão anda se a branch tiver o número da issue (`feat/12-...`) e o PR tiver
`Closes #12`. Cartão com etiqueta de sistema vira issue; issue nova vira cartão.

Repositório novo: a descrição (*About*) começa pelo nome do sistema, por exemplo
"Matrícula Online – rematrícula pelo site". A etiqueta aparece sozinha no quadro.

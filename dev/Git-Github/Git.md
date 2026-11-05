# Comandos
Pegar um commit específico e adicionar na minha branch atual utilizar o `cherry-pick`. Esse comando também joga o commit no seu histórico. Ao rodar o `git status` ele está lá.
```bash
git cherry-pich <ID DO COMMIT>
```

Voltar para o branch anterior o que estava:
```bash
git checkout -
```

Inclui partes específicas que foram alteradas
```bash
git add -p
```
Abre opções para adicionar tais pedaços alterados, tais alterações são jogadas para o `stage` para depois realizar o commit. 
- **y**:  sim
- **n**: não
- **q**: não adicione e saia do menu
- **a**: adiciona todos
- **d**: não adicione, mas não sai do menu
- **j**: próxima alteração
- **g**: alterações anterior
- **s**: divide em parte menores
- **e**: editar manualmente

Ao selecionar a opção y, ele vai pular para a próxima alteração, daí pode sair do menu e pode verificar que uma parte do código está em staged e outra não. Agora só fazer o commit e rodar o comando novamente e fazer a mesma coisa.

# Boas práticas

Não realizar commit na branch master/main, para não alterar o histórico da branch principal. Caso seja realizado fazer um `git revert`. 

Quando altera o histórico da branch master ao realizar um push para o remoto ele vai rejeitar informando que o histórico está errado. Por isso não é interessante realizar git reset direto na branch master/main. Para fazer o push para o remoto, deve-se utilizar o `push --force`.

```bash
git push origin <master / main> --force
```


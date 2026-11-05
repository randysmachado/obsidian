
## Diferença entre `parse` e `safeParse`
- `parse`: joga o erro na tela e quebra a aplicação, ideal utilizar um` try / catch` para pegar o erro
- `safeParse`: não joga o erro na tela, retorna objeto com `success`, `error` etc. Os dados retornados corretamente fica dentro de `data`, por exemplo: `result.data`. 

## Alterar mensagens:
Referência: [b7web](https://alunos.b7web.com.br/curso/node/intro-node-zod-mensagens-de-erro)

- Erro -  `required_error`
```javascript
 age: z.number({
    required_error: 'Idade é obrigatória'
  })
```
- Tipo inválido (o dado é uma `string` e o usuário enviou um `number`) - `invalid_type_error`
```javascript
age: z.number({
  invalid_type_error: 'A idade de ser um número'
})
```
Mensagem de validação
```javascript
age: z.number().gte(18, 'Precisa ser maior de idade') // esse
```


## Validar resposta de uma API
Utilizar o `z.promise()`

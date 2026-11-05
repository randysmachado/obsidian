É necessário 3 arquivos para criação de um novo theme: `style.css`, `index.php` e `function.php`

No `index.php` é preciso adicionar os scripts:
```php
<?php wp_head(); ?>  
    <p>Api</p>  
<?php wp_footer(); ?>
```

E no `style.css`
```css
/**  
    Theme Name: Api 
*/
```


# Custom post type
Nesta API está sendo utilizado custom post types.


# Criando API
No WordPress a forma de criar uma api é necessário criar uma função de callback que será chamada ao acessar uma rota.
Após criar a função é necessário registra-lá na REST API do WordPress


# Funcões úteis
`username_exists` -Função para validar se usuário já está cadastrado
`wp_create_user()` - Função para criar usuário

# Inativar produto
Como o wordpress tem os status do post, verificar uma forma de inativar o produto e não aparecer no front nem deletar do backend, ver isso com os 'post_status', 'draft', 'publish'


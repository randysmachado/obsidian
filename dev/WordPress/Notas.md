
# Arquivos do tema
`single.php` - Abre a página do post algo mais dinâmico
`page.php` - Abriria a página com o conteúdo estático

# Enqueue scripts
- `get_template_directory_uri()` - retorna a URL até a pasta do tema, exemplo: `https://meusite.com/wp-content/themes/theme-name`. Caso necessite utilizar um arquivo de estilo que se encontra em outra pasta ou com outro nome utilizar essa função.
- `get_template_directory()` - retorna o caminho absoluto (path) da pasta do tema, por exemplo: `C:\Users\randy\Local Sites\wp-devs\app\public\wp-content\themes\theme-name` 
- `get_stylesheet_uri()` - retorna a URL absoluta do arquivo de estilo `style.css` do tema, por exemplo:  `https://meusite.com/wp-content/themes/theme-name/style.css`
- `get_theme_file_uri` - 


```php
wp_get_theme()->get('Version');
```

`wp_get_post_parent_id()` verifica se o post tem um pai.
`get_the_ID()` retorna o ID do post
```php
wp_get_post_parent_id( get_the_ID() )
```

`get_post_type_archive_link( 'post_type' )` - retorna o link para página de arquivo (archive) de acordo com o post type inserido no parâmetro.

`get_the_category_list()` - retorna a lista de categorias de um post. Geralmente retorna um link referente a categoria.

# Ler mais sobre
Como registar um novo campo na API, utilizar o hook `rest_api_init` e a função `register_rest_field`. Ex:

```php
function university_custom_rest() {
    register_rest_field( 'post', 'authorName', array(
        'get_callback' => function() {return get_the_author();}
    ) );
}
add_action( 'rest_api_init', 'university_custom_rest' );
```

Como criar um nonce com `wp_create_nonce`. Olhar aula 92 curso Wordpress ou na seção My Notes do curso.

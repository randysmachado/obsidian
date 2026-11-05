`style.css`
T`heme URI `e `Theme Author` devem ser diferentes caso necessite disponibilizar o tema para comercialização

Lista de tags disponíveis para utilizar no `style.css` 
https://make.wordpress.org/themes/handbook/review/required/theme-tags/

Tags que precisam ser adicionadas no WordPress

# Tag que precisam ser adicionadas no wordpress

`language_attributes()` - na tag `html` no lugar do atributo `lang` 
`bloginfo( 'charset' )` - no atributo charset da meta
`body_class()` - tag body
`wp_body_open()` - abaixo da tag body

# Comentários no início dos arquivos
Se o tema for disponibilizado é necessário adicionar comentários no início dos arquivos assim como são feitos nos temas oficiais do WordPress.
Documentação: https://developer.wordpress.org/coding-standards/inline-documentation-standards/php/
```php
<?php

	/**
	 * The main template file
	 *
	 * This is the most generic template file in a WordPress theme
	 * and one of the two required files for a theme (the other being style.css).
	 * It is used to display a page when nothing more specific matches a query.
	 * E.g., it puts together the home page when no home.php file exists.
	 *
	 * @link https://developer.wordpress.org/themes/basics/template-hierarchy/
	 *
	 * @package Nome do tema
	 */
	
	get_header();
?>
```


`get_template_directory_uri()` - retorna a url até a pasta do tema algo como: 
http://localhost/folder-name/wp-content/themes/theme-name. Exemplo: quando há mais de um arquivo css no tema e precisa utilizar o caminho de onde esse arquivo se encontra.

`get_template_directory()` - retorna o caminho absoluto da pasta onde está o tema instalado, 
algo como: `C:\Users\randy\Local Sites\wp-woo\app\public\wp-content\themes\theme-name`

`get_stylesheet_uri()` - retorna a url absoluta do arquivo de estilo principal do tema `style.css`

Quando estive desenvolvendo utilizar `filemtime( get_template_directory() . '/style.css' )` no lugar da versão do style.css por causa do cache do navegador.


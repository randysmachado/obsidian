# Como incluir folha de estilo do jeito certo no WordPress
	https://www.youtube.com/watch?v=TITI2cAm68E
	Ver este vídeo pois é a nova forma de adicionar fonts
- Explicar passo a passo como incluir as folhas de estilo
- Explicar cada argumento que vai na função `wp_enqueue_style()`
- Explicar as funções `get_template_diretory()`, `get_template_directory_uri()`, `get_stylesheet_uri()`. Essas aqui podem gerar um post somente para explicar o que cada uma faz e linkar a postagem juntamente no post, ótimo para SEO.
- Explicar eventuais problemas com cache do navegador, com relação a carregamento de folhas de estilo.  Explicar que o cache é do navegador e não do WordPress. (fazer isso somente como desenvolvimento pois desenvolver com cache é horrível), a função filemtime() gera o unix timestamp
- Adicionar um estilo no `style.css` para refletir no site como exemplo e triar um print.
- Tirar um print do código fonte do script carregado no `head` como exemplo para o post


# Como carregar fontes do Google wordpress
Gerar outro post e linkar o post acima para melhorar o SEO.
- Mostrar isso com a função wp_enqueue_scripts() acima. 

# Desativar scripts desnecessários
- Emoji
- Blocos do Gutemberg caso não sejam utilizados
- etc. (Pegar esses scripts em algum tema que utilizei)

# Falar sobre @wordpress/scripts
	https://www.youtube.com/watch?v=qARMFZImty8
	Ver esse vídeo.


# Falar sobre a função bloginfo()

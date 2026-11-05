Estou criando uma aplicação utilizando a API de ofertas e realizando alguns testes eu percebi que o em alguns browsers eu não conseguia mostrar os produtos, então fui vasculhar e percebi que os bloqueadores de anúncios bloqueiam a API de vocês.

Browser que teste foi Brave e Arc que já tem bloqueadores inclusos ocorre o erro: net::ERR_BLOCKED_BY_CLIENT

E depois utilizei o Google Chrome sem bloqueador de anúncios e funcionou normalmente

Utilizando a extensão uBlock Origin no Google Chrome ocorre o bloqueio de chamada da API.

É preciso utilizar alguma reparo na API para que ela não seja bloqueada, como a API utiliza o domínio lomadee este domínio pode estar na black list dos bloqueadores de anúncios.
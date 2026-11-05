Após criar o projeto deve-se inicializar a API pois em versões recentes o Laravel desativou os recursos nativos de API pois nem todos os projetos trabalham com API
```shell
php artisan install:api
```

Logo depois adicionar no model de User o trait `HasApitokens` .
Ao utilizar API no Laravel é criado um arquivo chamado `sanctum.php` na pasta config.
No arquivo bootstrap é adicionar mais uma camada `api: __DIR__.'/../routes/api.php',` e o arquivo de rotas `api.php`

# Bind do Model na rota
No método show por exemplo, é comum buscar um recurso por `id`. Ao invés de fazer desta forma, é possível fazer um bind na rota:

Forma tradicional
```php
public function show(string $id)  
{  
    $post = Post::find($id);  
  
    return response()->json([  
        'data' => $post,  
    ], 200);  
}
```

Fica assim
```php
public function show(Post $post)  
{  
    return response()->json([  
        'data' => $post,  
    ], 200);  
}
```

# Utilizar Re
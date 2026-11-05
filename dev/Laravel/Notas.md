## Instalar versão específica 
Para criar um projeto Laravel com uma versão específica utilizar o seguinte comando:
```bash
composer create-project --prefer-dist laravel/laravel project-name "11.x"
```
Altere o `project-name` pelo nome do projeto. Sobre a versão é possível definir uma versão exata `10.2.1` ou pegar o último lançamento da versão utilizando o `x` para após a versão  `11.x` 


## Invokable Controller
Controller que só tem uma responsabilidade, ou seja, ele não tem os métodos do resource como: `index`, `show`, `store` etc. Tem somente uma função que invoca a classe. **Isso é PHP Moderno**

```php
public function __invoke(LoginRequest $request)
{
	// código
}
```

# Request
A camada de request lida com as requisições, nela é adicionada as validações que vem de uma requisição
```shell
php artisan make:request Auth\UserRequest
```

---

# Resource (API Resources)
A camada resource é para controlar o que é disponibilizado pela API. Por exemplo, quando um usuário realizar um login é no resource que é definido quais dados desse usuário é retornado e disponibilizado.

> [!SUCCESS] 
> É sempre boa pratica criar um resource para retornar os dados no frontend. Pois evita que dados confidenciais sejam expostos e só retorna os dados que são realmente necessários.

```shell
php artisan make:resource UserResource
```

> [!NOTE] Nota
> Obs.: O Resource cria uma estrutura nova com os dados, um deles é criar uma objeto `data:{}` com os dados dentro.

> [!TIP] Dica
> Como o Resource devolve um JSON ele cria uma variável `data`. Com o código abaixo ele remove a variável `data` e retorna os dados diretamente.

> [!WARNING] ATENÇÃO
> Sempre que for possível ao criar um Controller criar também Request e Resource.
#### `::collection()`

Ao chamar o método estático `collection` da resource, o retorno é um `array` com os dados já formatados.

```php
class PostResources extends JsonResource
{
    /**
     * Transform the resource into an array.
     *
     * @return array<string, mixed>
     */
    public function toArray(Request $request): array
    {
        return parent::toArray($request);
    }
}
```

É possível personalizar os dados que serão retornados:

```php
// Feature Resource

class FeatureResource extends JsonResource
{
    public function toArray($request)
    {
        return [
            'id' => $this->id,
            'name' => $this->name,
            'created_at' => $this->created_at->format('d/m/Y'),
        ];
    }
}
```

```php
// View
return FeatureResource::collection(Feature::all());
```

retorno:
```json
{
    "data": [
        { "id": 1, "nome": "Feature A", "criado_em": "20/02/2025" },
        { "id": 2, "nome": "Feature B", "criado_em": "21/02/2025" }
    ]
}
```

Quando se retorna um model e não a collection como no método `store`, é preciso instanciar a classe do Resource
```php
public function store(PostStoreRequest $request)
{
    $inputs = $request->validated();

    $post = Post::create($inputs);

	// instancia o resource
    return new PostResources($post);
}
```



# Exception
Na mensagem retornada na exception não é uma mensagem para o usuário e sim para quem estiver implementando a API.

---

# Events e Listeners
![[Pasted image 20250311083959.png]]
## Event (Acontecimento)
O Event é a ação que acontecerá como por exemplo: Quando o usuário realizar um cadastro.
```shell
php artisan make:event UserRegistered
```

Os dados que são passados dentro do `dispatch` do evento são recebidos na `__construct`  da classe.

```php
// Register controller

$user = User::query()->create($input);  
  
UserRegistered::dispatch($user);

```

```php
// UserRegistered

public function __construct(public User $user)  
{  
    //  
}
```

Essas informações do user são passadas para o listener que ficarão disponíveis no objeto `$event `do método `handle`

## Listeners (Ação)
Ficará ouvindo os events para disparar alguma coisa, que podem ser e-mail, serviço, ações etc. 

```shell
php artisan make:listener SendWelcomeEmail
```

Dentro do listener no método `handle`  que fica a configuração do e-mail/serviço que será enviado.

```php
public function handle(object $event): void  
{  
    Mail::to('test@test.com')->send(new WelcomeMail());  
}
```

Como falado anteriormente o `$event` recebe os dados que são passados no `__contruct` do Event.

```php
public function handle(object $event): void  
{  
    $user = $event->user;  
    
    Mail::to($user->email)->send(new WelcomeMail($user));  
}
```

# Mail
Para enviar e-mail é preciso criar uma classe Mail que é responsável por controlar o template de e-mail.
```shell
php artisan make:mail WelcomeMail
```

Assim como o Event é preciso acessar os dados do usuário, eles podem ser acessados através do `__construct`.

```php
public function __construct(public User $user)  
{  
    //  
}
```

Com isso todos os dados passados no `__construct` estarão disponíveis dentro do template do e-mail.

```php
Welcome, {{ $user->first_name }}!!
```


## Configurar o Event e o Listener
No arquivo `AppServiceProvider.php` dentro da função `boot` adicione os events vinculados aos listeners.

```php
Event::listen(  
    UserRegistered::class,  
    SendWelcomeEmail::class,  
);

// Mais de um Listener
Event::listen(
    UserRegistered::class,
    [SendWelcomeEmail::class, LogUserRegistration::class]
);
```


---

# Filas (Queues)
Link documentação: https://laravel.com/docs/11.x/queues

> [!NOTE] Nota
> No Laravel 11 já tem a migration das filas criada (Job table)
## Filas no banco de dados

```shell
php artisan make:queue-table
```

> [!WARNING] Atenção
> No `.env` é preciso que a variável `QUEUE_CONNECTION` esteja com o valor `database`
> `QUEUE_CONNECTION=database`

Para o listener ir para fila é preciso configurar e dizer que ele deve ir para a fila. Para que isso seja feito é só implementar a classe com `ShouldQueue`.
```php
class SendWelcomeEmail implements ShouldQueue
```
Com isso ao enviar o e-mail ele ficará na fila (verificar na tabela job), mas não será enviado. Para enviar os itens da fila é preciso executar o comando:
```shell
php artisan queue:work
```






























---

# InertiaJS
## Form
Ao criar um `form` é preciso utilizar o hook `useForm` no Inertia.
Link: https://inertiajs.com/forms








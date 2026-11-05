link: https://youtu.be/lqKbDEBa2B0?si=nD_CEi4S4wncpdPP
# Pacotes do Projeto 
- Spatie - lida com permissões


## Spatie
link: https://spatie.be/docs/laravel-permission/v6/installation-laravel
Instalação
```
composer require spatie/laravel-permission
```

```
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
```

Gerar a migration: 
```
 php artisan migrate
```



# Steps
Depois de instalar o Spatie é preciso ir no model `User` e adicionar a Trait HasRoles do Spatie. Este passo a passo tem na documentação do Spatie
```php
use HasFactory, Notifiable, HasRoles;
```
link: https://spatie.be/docs/laravel-permission/v6/installation-laravel
link: https://spatie.be/docs/laravel-permission/v6/basic-usage/basic-usage


Depois criar dois Enum, com permissions (permissões) e outro com as roles (regras/papéis/funções). No comando vai ser criado uma pasta chamada Enum dentro da pasta app e dentro os arquivos. *Olhar cada arquivo e analisar o código*.
```
php artisan make:enum Enum\PermissionsEnum
```

```
php artisan make:enum Enum\RolesEnum
```

## Criar as seeds de cada role e permission
Crias a seeds para associar usuários a cada role e permission.
*Olhar o arquivo para ver o código*

```
php artisan migrate:fresh --seed
```

## Habilitando Verificação por e-mail
No model `User` habilitar a implementação `MustVerifyEmail`
```php
class User extends Authenticatable implements MustVerifyEmail
```
Depois fazer a configuração dos dados de envio de e-mail no arquivo `.env`

## Resources (AuthUserResource, UserResource)
Criado dois `resources`, um para o usuário autenticado `AuthUserResource` e outro para usuário `UserResource`.
Depois de definir os Resources, dentro do `HandleInertiaRequests` é preciso fazer umas modificações, já que foi criado os resources para retornar somente o que é preciso.

> [!TIP]
> Como o Resource devolve um JSON ele cria uma variável `data`. Com o código abaixo ele remove a variável `data` e retorna os dados diretamente.

```php
/**  
 * @var bool Remove o `data` de retorno JSON  
 */
 public static $wrap = false;
```

No componente `AuthenticatedLayout (react)`, é buscado o usuário autenticado na linha abaixo:
```js
const user = usePage().props.auth.user;
```
Essas informações vem do `HandleInertiaRequests`. 
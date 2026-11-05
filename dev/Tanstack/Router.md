Link tutorial: https://youtu.be/WyqxZniJk5w?si=jJnKFEhM7aylDVIY

## Padrões
- Sempre utilizar o componente `Link` do tanstack router.
- 






# Nesting Routes

Alguns detalhes do nested routes.
Suponhamos que há a seguinte estrutura de pastas para settings:

`/settings/`
`/settings/profile.tsx`
`/settings/payment.tsx`

Na estrutura acima será gerado somente duas rotas `/settings/profile` e `settings/payment`. Caso acesse a rota `/settings` retornará Not Found.

Se adicionar um arquivo chamado `index.tsx` dentro de settings ele vai gerar uma página `/settings` e no arquivo que o tanstack gera `/settings/` com uma barra no final, identificando que é uma página.

Ao criar um arquivo chamado `route.tsx` o tanstack vai entender esse arquivo como um
`root layout`, ou seja, as rotas dentro da estrutura `/settings` vão herdar estilos e comportamentos dele. Neste caso para as rotas `/profile` e `/payment` serem mostradas é preciso utilizar o componente do tanstack `<Outlet />`.


`/settings/` (Not found)
`/settings/index.tsx` será uma página de `/settings`
`/settings/route.tsx` Root Layout de Settings (Utilizar o componente `<Outlet />`  )
`/settings/profile.tsx`
`/settings/payment.tsx`


# Parâmetros pela rota e Loader (Path Parameters)
Se há uma rota recebe um parâmetro `id` ao criar a rota é necessário utilizar a convenção `$nome_do_parametro`, exemplo `$id`
Exemplo: `pokemon/$id.tsx`

```typescript
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/pokemon/$id')({
  component: RouteComponent,
})

function RouteComponent() {
  return <div>Hello</div>
}
```

Para acessar o parâmetro da rota utilize o `Route.useParams()` 
```js
const { id } = Route.useParams();
```

# Loader
Caso precise acessar ou fazer alguma outra coisa antes mesmo de obter o `ID`, por exemplo, obter meus dados antes do root carregar. Somente utilizar a função loader:
Ou seja, o loader serve para buscar dados para serem renderizados no componente.

```javascript
import { createFileRoute } from "@tanstack/react-router";

import { getPokemon } from "@/api/pokemon";

export const Route = createFileRoute("/pokemon/$id")({
  component: PokemonPage,
  loader: async ({ params }) => await getPokemon(params.id),
});

function PokemonPage() {
  const { id } = Route.useParams();
  const pokemon = Route.useLoaderData();

  return (
    <div>
      <h2>
        {id} - {pokemon.name}
      </h2>

      <img
        src={pokemon.sprites.front_default}
        className="size-32"
        alt={pokemon.name}
      />

      <p>Height: {pokemon.height}</p>
      <p>Weight: {pokemon.weight}</p>
    </div>
  );
}
```

# Parâmetro de consulta (Query Parameters  and Validation)


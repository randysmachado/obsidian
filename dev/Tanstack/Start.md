

## Dynamic Routes (Rotas Dinâmicas)
Para criar rotas dinâmicas utiliza-se o sinal de `$` e um slug para referenciar o parâmetro, por exemplo: `$id.tsx` onde o `id` será o parâmetro na rota.

Para acessar o atributo da rota, utiliza-se `Route.useParams();`

```jsx
function RouteComponent() {
  const { id } = Route.useParams();

  return <div>Hello "/products/{id}"!</div>;
}
```

### Link
Quando utiliza o componente `<Link />` para acessar uma rota dinâmica é necessário adicionar a propriedade `params` que é o parâmetro do link, pois ele não sabe o que vem no parâmetro.

```jsx
<Link to="/products/$id" params={{ id: '1' }}>
    Product 1
</Link>
```

# Loader
Ao utilizar a função `loader` ao carregar a rota, é necessário acessar os dados de retorno dentro do componente.

```tsx
export const Route = createFileRoute('/products/')({
  component: ProductsPage,
  // Ao acessar a rota fazer o loader
  loader: () => {
    return { products: sampleProducts };
  },
});
```

Para acessar os dados do loader utiliza o hook do TanStack Start `Route.useLoaderData()`, puxando de `Route`;

```tsx
function ProductsPage() {
  const { products } = Route.useLoaderData();
}
```

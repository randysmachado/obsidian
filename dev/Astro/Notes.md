---
tags:
  - Astro
---

# Layout
Quando se cria um layout é utilizado a tag `<slot />` que é responsável a jogar o conteúdo dentro do layout.
É possível adicionar uma propriedade `name` no slot, com isso ao adicionar um componente no layout deve adicionar o name do slot, por exemplo.

```html
<!-- BaseLayout -->
<main>
    <slot name="content" />
</main>
```

```html
<!-- About Page -->
<div slot="content">
    <h1>About Page</h1>
    <p>This is the About page of the website.</p>
</div>
```

```html
<!-- Home Page -->
<div slot="content">
    <h1>Home Page</h1>
    <p>This is the Home page of the website.</p>
</div>
```

No exemplo acima somente o conteúdo do About Page apareceria renderizado no `BaseLayout`. Assim é possível dar dinamicidade ao mostrar conteúdos, como estilos diferentes, funções diferente etc.

# Scope
No astro os estilos, funções etc são salvas no escopo do componente ou arquivo. Então um estilo em um link `a` CSS não afeta outros estilos na mesma tag.
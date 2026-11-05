

Propriedades `class:list` e `define:vars` na tag `style`. Deixar claro que deve-se utilizar com cautela para não virar bagunça.

```html
---
const { classList, background, color } = Astro.props;
---

<button class:list={["btn", classList]}>
  <slot />
</button>

<style define:vars={{ background, color }}>
  .btn {
    padding: 0.5em 1em;
    border: none;
    background-color: var(--background);
    color: var(--color);
    border-radius: 4px;
    cursor: pointer;
    font-size: 1em;
  }

  .btn:hover {
    background-color: #005fa3;
  }
</style>
```
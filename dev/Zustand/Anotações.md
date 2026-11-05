## Básico

No zustand você precisa criar como se fosse uma variável com valores iniciais e funções também conhecida como ações (actions) para manipular essas variáveis. Bem parecido com State em React.

```typescript
interface BearState {
  blackBears: number;

  increaseBlackBears: (by: number) => void;
}

export const useBearStore = create<BearState>()((set) => ({
  // variavel do estado
  blackBears: 10,

  // Funções ou Ações para manipular as variáveis do estado
  increaseBlackBears: (by: number) =>
    set((state) => ({ blackBears: state.blackBears + by })),
}));
```

Uma recomendação é não utilizar a desestruturação dos estado e ações e sim isolar cada um em uma variável.

```javascript
// ✅ Bom
const blackBears = useBearStore((state) => state.blackBears);
const increaseBlackBears = useBearStore((state) => state.increaseBlackBears);

// ❌ Ruim
const { increaseBlackBears, blackBears } = useBearStore((state) => state);
```
Ao realizar uma desestruturação componentes que não deveriam ser renderizados sofrerão renderização, devido a utilização do mesmo estado, mesmo estando em componentes separados. E na maioria das vezes não queremos isso. Então a própria documentação do Zustand não recomenda desestruturar.


## Objetos Aninhados (Array) / useShallow
### Shallow
Faz uma comparação superficial de igual entre objetos e arrays, ao invés de comparar tudo profundamente.

Quando se use um seletor do hook useStore, por padrão ele compara o novo valor retornado com o anterior utilizando a igualdade de referência `(===)` .
Ao selecionar um objeto ou array, mesmo que só parte dele mude, a referência é diferente, então o componente vai rerenderizar. 

O que o `shallow` faz?
- Ele compara cada propriedade do objeto (ou cada elemento do array) uma vez, e só considera "diferente" se algum valor interno mudou.
- Se todas as chaves/itens ainda tiverem o mesmo valor (comparados com `===`), ele considera tudo igual e pula a rerenderização.

Em resumo: sempre que você selecionar múltiplos campos (ou um objeto) de uma só vez e não quiser que seu componente atualize "por engano" só porque a referência do array/objeto mudou, passe `shallow` como segundo argumento.

Exemplo: 

```typescript
interface Bear {
  id: number;
  name: string;
}

interface BearState {
  bears: Bear[];

  doNothing: () => void;
}

export const useBearStore = create<BearState>()((set) => ({
  bears: [{ id: 1, name: "Urso 1" }],

  doNothing: () => set((state) => ({ bears: [...state.bears] })),
}));
```

Componente sem shallow:
```javascript
export const BearsDisplay = () => {
  const bears = useBearStore((state) => state.bears);
  const doNothing = useBearStore((state) => state.doNothing);

  return (
    <WhiteCard centered>
      <h2>Ursos</h2>
      <button onClick={doNothing}>Do Nothing</button>

      <pre>{JSON.stringify(bears, null, 2)}</pre>
    </WhiteCard>
  );
};
```
Toda vez que clicar no botão "Do Nothing" o componente vai renderizar.

Componente com shallow:
```javascript
export const BearsDisplay = () => {
  // ❗ Usando o useShallow 
  const bears = useBearStore(useShallow((state) => state.bears));
  const doNothing = useBearStore((state) => state.doNothing);

  return (
    <WhiteCard centered>
      <h2>Ursos</h2>
      <button onClick={doNothing}>Do Nothing</button>

      <pre>{JSON.stringify(bears, null, 2)}</pre>
    </WhiteCard>
  );
};
```
O componente não renderiza

## Propriedades computadas
Para poder pegar o total de Ursos, o exemplo que está sendo usado, podemos criar uma função `get` do JavaScript e a função `get` do Zustand e mostrar o valor em outro componente. Lembrando que o nome da função deve ser o mesmo nome que foi definido da interface.

`bearStore.ts`
```typescript
// bearStore.ts

import { create } from "zustand";

interface Bear {
  id: number;
  name: string;
}

interface BearState {
  blackBears: number;
  polarBears: number;
  pandaBears: number;

  bears: Bear[];

  computed: {
    totalBears: number;
  };
}

export const useBearStore = create<BearState>()((set, get) => ({
  // variavel do estado
  blackBears: 10,
  polarBears: 5,
  pandaBears: 1,

  bears: [{ id: 1, name: "Urso 1" }],

  computed: {
    // função get do JavaScript
    get totalBears() {
      return (
        get().blackBears +
        get().polarBears +
        get().pandaBears +
        get().bears.length
      );
    },
  },
```

Uso:
```typescript
const totalBears = useBearStore((state) => state.computed.totalBears);
```


## Middleware
Para persistir o estado do Zustand no `localStorage` ou `sessionStorage` é preciso utilizar middlewares.  O middleware em questão é o `persist`.

```typescript
interface PersonState {
  firstName: string;
  lastName: string;
}

interface Actions {
  setFirstName: (value: string) => void;
  setLastName: (value: string) => void;
}

type PersonStore = PersonState & Actions;

export const usePersonStore = create<PersonStore>()(
  // ❗Aqui vai o middleware
  persist(
    (set) => ({
      firstName: "",
      lastName: "",

      setFirstName: (value) => set({ firstName: value }),
      setLastName: (value) => set({ lastName: value }),
    }),
    // ❗é necessário passar um segundo argumento que é o nome 
    // a ser salvo no localStorage.
    {
      name: "person-storage",
    }
  )
);
```
Por padrão o estado é salvo no `localStorage`, mas se quiser salvar no `sessionStorage` por exemplo, é preciso adicionar o parâmetro `storage` e indicar onde o estado será salvo.
```typescript
storage: createJSONStorage(() => sessionStorage),
```


## StateCreator Interface
Serve para agrupar o `set` caso o store criado esteja ficando grande e complexo

```typescript
import { type StateCreator, create } from "zustand";
import { persist, createJSONStorage } from "zustand/middleware";

interface PersonState {
  firstName: string;
  lastName: string;
}

interface Actions {
  setFirstName: (value: string) => void;
  setLastName: (value: string) => void;
}

type PersonStore = PersonState & Actions;

// ❗ Aqui é criado a interface StateCreator
const storeAPI: StateCreator<PersonStore> = (set) => ({
  firstName: "",
  lastName: "",

  setFirstName: (value) => set({ firstName: value }),
  setLastName: (value) => set({ lastName: value }),
});

export const usePersonStore = create<PersonStore>()(
  persist(
  // ❗ Aqui a variável que foi criada, que 
  // fica no lugar do set
  storeAPI, {
    name: "person-storage",
    storage: createJSONStorage(() => sessionStorage),
  })
);
```









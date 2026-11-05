Para controlar um formulário utilizar o hook `useForm`. Defina uma variável e assinale ao hook. 

```typescript
const form = useForm({});
```

Define os valores padrão do formulário, aqui o formulário tem dois valores, `username` e `password`. Se tiver outros valores defina aqui.
É possível ter valores assíncronos, leia mais aqui: https://tanstack.com/form/latest/docs/framework/react/guides/async-initial-values

```typescript
const form = useForm({
    defaultValues: {
      username: "",
      password: "",
    },
  });
```

Na tag de formulário no método `onSubmit` é preciso configurar para o tanstack form lide com os dados na submissão do formulário.
```javascript
<form
	onSubmit={(e) => {
	  e.preventDefault();
	  form.handleSubmit(); // tanstack form
	}}
>
```


No `onSubmit` do formulário adicione as seguintes propriedades:

```typescript
<form
  className="flex flex-col gap-4"
  onSubmit={(e) => {
	e.preventDefault();
	e.stopPropagation();
  }}
>
```

## Compartilhar default values entre formulários
Utilizar a função `formOptions`. 
Link: https://tanstack.com/form/latest/docs/framework/react/guides/basic-concepts#form-instance



## Field Meta
`field.state.meta` tem informações sobre o estado dos campos.

## Form 
`form.state` informações, dados, metadados do formulário.

> [!NOTE] Nota
> O Tanstack Form por padrão evita renderização desnecessário no formulário quando algum campo é alterado. Para que haja mais reatividade é necessário utilizar `useStore` ou `<form.Subscribe>`.

https://tanstack.com/form/latest/docs/framework/react/guides/basic-concepts#form-instance

![[Pasted image 20251104094831.png]]

> [!IMPORTANT] Importante
> É importante entender os conceitos de `isDirty`, `isPristine` tanto do `form` quando do `field`


`useStore`: https://tanstack.com/form/latest/docs/framework/react/guides/reactivity#usestore
`form.Subscribe`: https://tanstack.com/form/latest/docs/framework/react/guides/reactivity#**formsubscribe

### useStore
Como foi falado na nota, o tanstack não renderiza o formulário quando há alteração dos campos, para isso precisamos utilizar métodos para deixar mais reativo.
O `isDirty` do `field` tem um estado diferente do `isDirty` do `form`. Então para correlacionar um valor do `field`  com `form` uma das formas é utilizar o `useStore`

```javascript
const firstName = useStore(form.store, (state) => state.values.firstName)
```

O useStore recebe dois argumentos o store do formulário e uma função linkando o valor que campo que você precisa. O segundo parâmetro não é obrigatório, mas se não for passado todo o formulário é renderizado quando houver qualquer alterado em algum campo.


### form.Subscribe
Suponhamos que eu tenha um formulário onde para aparecer outro campo eu precise que outro seja preenchido, por exemplo para aparecer o campo `lastName` o `firstName` deve ser preenchido.
No código abaixo tem o exemplo de como podemos lidar com isso utilizando o `form.Subscribe`.

```javascript
<form.Subscribe selector={(state) => state.values.firstName}>
	  {(firstName) => (
		<>
		  {firstName && (
			<form.Field name="lastName">
			  {(field) => {
				return (
				  <div className="mb-4">
					<input
					  type="text"
					  placeholder="Last Name"
					  className="border border-black p-2 w-full"
					  value={field.state.value}
					  onChange={(e) => field.handleChange(e.target.value)}
					  onBlur={field.handleBlur}
					/>
				  </div>
				);
			  }}
			</form.Field>
		  )}
		</>
	  )}
</form.Subscribe>
```


## Listeners
Se inspecionar os values do form utilizando o store 
```javascript
const values = useStore(form.store, (state) => state.values);

<pre>{JSON.stringify(values, null, 2)}</pre>
```

Ao preencher o `firstName` o campo `lastName` vai aparecer, se você remover os dados do `firstName` o campo `lastName` vai desaparecer, porém você vai observar que o valor atribuído continuará preenchido.

```json
{
  "firstName": "",
  "lastName": "Machado",
  "email": "",
  "password": "",
  "confirmPassword": "",
  "address": {
    "street": "",
    "city": "",
    "state": "",
    "zipCode": ""
  },
  "skills": [],
  "acceptTerms": false
}
```

Para limpar o valor precisamos utilizar os listeners, pois com ele podemos ficar "escutando" o que está acontecendo e fazer alguma ação. A nossa ação acima será a seguinte, se no campo `firstName` não tiver preenchido tempos que limpar o campo `lastName`.

```javascript
<form.Field
  name="firstName"
  // LISTENERS
  listeners={{
	onChange: ({ value }) => {
	  if (!value) {
		form.setFieldValue("lastName", "");
	  }
	},
  }}
>
```
No listener ficará "ouvindo" o `onChange`, e utilizaremos a função `setFieldValue` para limpar o campo `lastName`.
Quando utilizar uma `api` para atualizar dados podemos utilizar os `debounces` para eliminar chamadas na `api` sempre que algo for alterado. Assim ele aguarda meio segundo para aplicar as mudanças.

```javascript
<form.Field
  name="firstName"
  listeners={{
	onChangeDebounceMs: 500, // DEBOUNCE APLICADO.
	onChange: ({ value }) => {
	  if (!value) {
		form.setFieldValue("lastName", "");
	  }
	},
  }}
>
```

Os Listeners também podem ser utilizados definidos dentro do formulário, não se limita somente a campos.
```javascript
const form = useForm({
    listeners: {
      onChange: ({ formApi, fieldApi }) => {
        console.log({ formApi, fieldApi });
      },
    },
});
```

No código acima tem o exemplo do listener ouvindo mudanças em todo o formulário e com as `formApi`, `fieldApi` é possível definir com mais precisão o que é alterado e fazer uma ação.

## Object, Arrays e Boolean
Para alterar um objeto é simples. Utiliza o mesmo componente e no name você referencia o name com a notação de um objeto. Ex:
### Object
```typescript
const defaultValues = {
	address: {
	    street: "",
	    city: "",
	    state: "",
	    zipCode: "",
	},
}

<form.Field name="address.street"> // <- AQUI!!
  {(field) => (
	<div className="mb-4">
	  <input
		type="text"
		className="border border-black p-2 w-full"
		placeholder="Street"
		value={field.state.value}
		onChange={(e) => field.handleChange(e.target.value)}
		onBlur={field.handleBlur}
	  />
	</div>
  )}
</form.Field>
```

### Array
Para trabalhar com `array` é necessário adicionar o `mode="array"`.
O tanstack fornece recursos para lidar com arrays.

Para remover utilizar `field.removeValue(index)` aqui estamos passando o `index` do array.
Para adicionar utilizar `field.pushValue({})`

Também é aplicado o conceito de `subField` que é quando se tem um `field` dentro de outro.

```typescript
const defaultValues = {
skills: [
    {
      name: "HTML",
      id: crypto.randomUUID(),
      level: "beginner",
    },
    {
      name: "CSS",
      id: crypto.randomUUID(),
      level: "beginner",
    },
    {
      name: "JavaScript",
      id: crypto.randomUUID(),
      level: "beginner",
    },
],
}

<form.Field name="skills" mode="array">
  {(field) => {
	return (
	  <div>
		Skills
		<div>
		  {field.state.value.map((skill, index) => (
			<div
			  key={skill.id}
			  className="flex items-center mb-2 gap-2"
			>
			  <span>{skill.name}</span>

			  <form.Field name={`skills[${index}].level`}>
				{(subField) => (
				  <select
					className="border border-black p-1 w-full"
					value={subField.state.value}
					onChange={(e) =>
					  subField.handleChange(e.target.value as any)
					}
					onBlur={subField.handleBlur}
				  >
					<option value="beginner">Beginner</option>
					<option value="intermediate">Intermediate</option>
					<option value="expert">Expert</option>
				  </select>
				)}
			  </form.Field>

			  <Button
				type="button"
				size="sm"
				variant="destructive"
				onClick={() => field.removeValue(index)}
			  >
				X
			  </Button>
			</div>
		  ))}
		</div>
		<Button
		  type="button"
		  size="sm"
		  onClick={() => {
			field.pushValue({
			  id: crypto.randomUUID(),
			  name: `New Skill ${field.state.value.length + 1}`,
			  level: "beginner",
			});
		  }}
		>
		  Add Skill
		</Button>
	  </div>
	);
  }}
</form.Field>
```


### Boolean




















Com a variável que tem o hook atribuído será onde é possível controlar os dados do formulário. Utilizando o Field.
```typescript
<form.Field
	name="username"
	children={(field) => (
	  <div className="flex flex-col gap-2">
		<Label htmlFor="username">Username</Label>
		<Input
		  type="text"
		  id="username"
		  placeholder="your username"
		  value={field.state.value}
		  onChange={(e) => field.handleChange(e.target.value)}
		/>
	  </div>
	)}
/>
```

Utilizando o `form.getMeta()` é possível ter os valores em tempo real, assim é possível proporcionar uma experiencia maior para o usuário.

```html
<div className="relative">
	  <Input
		id="username"
		type="text"
		value={field.state.value}
		onChange={(e) => field.handleChange(e.target.value)}
	  />
	  {field.getMeta().isValidating && (
		<div className="absolute right-2 top-1/2 -translate-y-1/2">
		  <LoaderCircleIcon className="animate-spin" />
		</div>
	  )}
</div>
```

## Validação entre dois campos 
link: https://tanstack.com/form/latest/docs/framework/react/guides/linked-fields

Dentro do `validators` utilizar `onChangeListenTo`.
```javascript
validators={{
  onChangeListenTo: ["password"],
  onChange: ({ value, fieldApi }) => {
	if (value !== fieldApi.form.getFieldValue("password")) {
	  return "Passwords do not match";
	}
  },
}}
```
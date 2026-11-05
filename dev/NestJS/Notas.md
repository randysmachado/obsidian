


## Relacionamento 
Doc: [Relacionamentos](https://docs.nestjs.com/techniques/database#relations)


### Many to many
Adiciona o decorator `@ManyToMany()` 
`@JoinTable()` deve ir acompanhando pois ele define qual é a tabela principal entre o relacionamento.

No exemplo abaixo, há duas entidades que se relacionam, courses e tags
Na entidade tag é necessário criar uma referência da entidade courses. `courses: Couses[]`
E na entidade courses é feito a referência com a entidade tags `tags: Tag[];`

OBS: Com esse relacionamento, vai gerar uma tabela pivô no banco de dados entre as entidades
`courses_tags_tags`.

```typescript
// courses.entity.ts

@JoinTable()
@ManyToMany(() => Tag, (tag) => tag.courses)
tags: Tag[];
```

```typescript
// tags.entity.ts

@ManyToMany(() => Course, (course) => course.tags)
courses: Couses[]
```




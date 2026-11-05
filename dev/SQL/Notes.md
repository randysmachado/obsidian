
# Create Table 

Sem definição de tipos e restrições (constraints)
```sql
CREATE TABLE courses (id, name, lessons);
```

Com definição de tipos e restrições (constraints)
```sql
CREATE TABLE courses(
	id INTEGER NOT NULL,
	name TEXT NOT NULL,
	lessons INTEGER
);
```

# Pragma

Verifica as características da tabela.
```sql
PRAGMA TABLE_INFO('courses'); -- o argumento é uma string
```

# Drop Table

```sql
DROP TABLE courses;
```

# Select simples

```sql
SELECT * FROM courses;
```

# Insert

```sql
INSERT INTO courses (id, name, lessons) VALUES (1, 'HTML', 10)
-- Utilizar aspas simples na string.
```

# Aspas

> [!INFO] NOTA
> 
> Aspas simples `''` são usadas para strings, aspas duplas `""` para identificadores como nomes de colunas ou tabelas. Números são definidos sem aspas.
> 
> Podemos omitir as aspas duplas para nomes de colunas e tabelas, mas é uma boa prática usá-las para evitar conflitos com palavras chaves (keywords).

```sql
INSERT INTO "courses" ("id", "name", "lessons") VALUES (1, 'HTML', 10);
```





















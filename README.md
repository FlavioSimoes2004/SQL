# SQL
## RELATIONAL DATABASE
É uma data base que organiza informação em uma ou mais tabelas.\
Tabela as vezes são referidas como relations(relações).\
Coluna é um set de data de um tipo particular.\

## DATA TYPES
tipos de DATA TYPE:
- INTEGER, um número inteiro positivo ou negativo
- TEXT, uma string
- DATE, data
- REAL, um valor decimal

## STATEMENTS
um statement é um texto que a data base reconhece como comando válido.\
Statement sempre acaba com ';'.
```SQL
CREATE TABLE table_name (
   column_1 data_type, 
   column_2 data_type, 
   column_3 data_type
);
```

### QUEBRANDO COMPONENTES DE UM STATEMENT
No exemplo acima, 'CREATE TABLE' é uma clause. Clause performa tarefas específicas no SQL.\
Por convenção, clauses são escritas com letras maiúsculas.\
Clauses podem também ser referidas como comandos.\
\
'table_name' se refere ao nome da tabela em que o comando está sendo aplicado.\
\
'(column_1 data_type, column_2 data_type, column_3 data_type)' são parâmetros.\
Um parâmetro é uma lista de colunas , data types ou valores que são passados para uma clause como argumentos.\
No código acima, os parâmetros são uma lista de nomes de colunas, e seus data types.

## CREATE
O statement 'CREATE' nos permite criar uma nova tabela no data base.\
Pode usar o 'CREATE' quando quiser para criar uma tabela do zero.\
```SQL
CREATE TABLE celebs (
   id INTEGER, 
   name TEXT, 
   age INTEGER
);
```
O exemplo acima cria uma nova tabela chamada 'celebs'.

## INSERT
Esse statemente insere uma nova linha na tabela.\
Podemos usar o 'INSERT' quando for adicionais mais coisas.
```SQL
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Justin Bieber', 29);
```
O código acima adiciona uma celebridade na tabela celebs.

### QUEBRANDO O CÓDIGO
- INSERT INTO is a clause that adds the specified row or rows.
- celebs is the table the row is added to.
- (id, name, age) is a parameter identifying the columns that data will be inserted into.
- VALUES is a clause that indicates the data being inserted.
- (1, 'Justin Bieber', 29) is a parameter identifying the values being inserted.
  - 1: an integer that will be added to id column
  - 'Justin Bieber': text that will be added to name column
  - 29: an integer that will be added to age column

## SELECT
É usado para buscar dados no data base.\
O 'INSERT' sempre retorna uma nova tabela chamada de 'the result set'.\
No exemplo abaixo, o SELECT retorna todos os dados da coluna de nome 'name' da tabela celebs.
```SQL
SELECT name FROM celebs;
```
\
OU
```SQL
SELECT column1, column2 
FROM table_name;
```
\
OU\
\
Para selecionar todas as colunas de uma tabela, podemos usar o '*' em vez do nome de uma coluna.\
O '*' seleciona todas as colunas, em vez de ter que nomear cada uma individualmente.\
```SQL
SELECT * FROM celebs;
```

### QUEBRANDO O CÓDIGO
- SELECT is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database.
-  name specifies the column to query data from.
-  FROM celebs specifies the name of the table to query data from. In this statement, data is queried from the celebs table.
 
## ALTER
O 'ALTER TABLE' adiciona uma nova coluna na tabela.\
Podemos usar esse comando quando quisermos adicionar uma nova coluna na tabela.\
O código abaixo adiciona uma nova coluna chamada 'twitter_handle'  na tabela celebs.
```SQL
ALTER TABLE celebs
ADD COLUMN twitter_handle TEXT;
```

### QUEBRANDO O CÓDIGO
- ALTER TABLE is a clause that lets you make the specified changes.
- celebs is the name of the table that is being changed.
- ADD COLUMN is a clause that lets you add a new column to a table:
  - twitter_handle is the name of the new column being added
  - TEXT is the data type for the new column
- NULL is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have NULL (∅) values for twitter_handle.

## UPDATE
Edita uma linha na tabela.\
Podemos usá-lo para quando quisermos mudar dados de uma linha.\
O exemplo abaixo atualiza um dado de uma linha com id igual a 4 e muda o valor da coluna 'twitter_handle'.
```SQL
UPDATE celebs 
SET twitter_handle = '@taylorswift13' 
WHERE id = 4; 
```

### QUEBRANDO CÓDIGO
- UPDATE is a clause that edits a row in the table.
- celebs is the name of the table.
- SET is a clause that indicates the column to edit.
  - twitter_handle is the name of the column that is going to be updated
  - @taylorswift13 is the new value that is going to be inserted into the twitter_handle column.
- WHERE is a clause that indicates which row(s) to update with the new column value. Here the row with a 4 in the id column is the row that will have the twitter_handle updated to @taylorswift13.

## DELETE
Deleta um ou mais linhas de uma tabela.\
No exemplo abaixo deleta todas as linhas onde a coluna 'twitter_handle' é NULL.
```SQL
DELETE FROM celebs 
WHERE twitter_handle IS NULL;
```

### QUEBRANDO O CÓDIGO
- DELETE FROM is a clause that lets you delete rows from a table.
- celebs is the name of the table we want to delete rows from.
- WHERE is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL.
- IS NULL is a condition in SQL that returns true when the value is NULL and false otherwise.

## CONSTRAINTS
Constraints that add information about how a column can be used are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction. The statement below sets constraints on the celebs table.
```SQL
CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAULT 'Not Applicable'
);
```

### QUEBRANDO O CÓDIGO
- PRIMARY KEY columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.
- UNIQUE columns have a different value for every row. This is similar to PRIMARY KEY except a table can have many different UNIQUE columns.
- NOT NULL columns must have a value. Attempts to insert a row without a value for a NOT NULL column will result in a constraint violation and the new row will not be inserted.
- DEFAULT columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.

## AS
Renomeia a coluna.\
No exemplo abaixo, a coluna é renomeada para Titles.\
É necessário o uso '' para renomear.
```SQL
SELECT name AS 'Titles'
FROM movies;
```

## DISTINCT
É usado para retornar valores únicos.\
Sem o DISTINCT:
```SQL
SELECT tools 
FROM inventory;
```
OUTPUT
<pre>
<strong>tools</strong>
Hammer
Nails
Nails
Nails
</pre>

Com o distinct:
```SQL
SELECT DISTINCT tools 
FROM inventory;
```
OUTPUT
<pre>
<strong>tools</strong>
Hammer
Nails
</pre>

## WHERE
Podemos restringir os elementos que queremos que retorne nas colunas usando o WHERE, para obter apenas informações que queremos.\
No exemplo abaixo, conseguimos o retorno de apenas filmes com nota maior que 8.
```SQL
SELECT *
FROM movies
WHERE imdb_rating > 8;
```

### COMO FUNCIONA?
- The WHERE clause filters the result set to only include rows where the following condition is true.
- imdb_rating > 8 is the condition. Here, only rows with a value greater than 8 in the imdb_rating column will be returned.

## LIKE
Serve para comparar valores similares.\
Imagine que numa tabela de filmes, há dois filmes com nomes similares: se7ven e seven.\
Como iriámos selecionar filmes que começam com "se" e terminam com "en" e contém exato 1 caractere no meio?
```SQL
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';
```

### COMO FUNCIONA?
- LIKE is a special operator used with the WHERE clause to search for a specific pattern in a column.
- name LIKE 'Se_en' is a condition evaluating the name column for a specific pattern.
- Se_en represents a pattern with a wildcard character.
- The _ means you can substitute any individual character here without breaking the pattern. The names Seven and Se7en both match this pattern.

### MAIS COISAS IMPORTANTES
Pega todos os filmes que começam com a letra A.
```SQL
SELECT * 
FROM movies
WHERE name LIKE 'A%';
```

Pega todos os filmes que terminam com a letra A.
```SQL
SELECT * 
FROM movies
WHERE name LIKE '%A';
```

Para pegar todos os filmes que tem a palavra "man".
```SQL
SELECT * 
FROM movies 
WHERE name LIKE '%man%';
```

Pega todos os filmes que começam com "The ".
```SQL
SELECT * 
FROM movies
WHERE name LIKE 'The %' AND imdb_rating >= 8;
```

## IS
Não é possível usar operadores como '=' ou '!=' para saber se um valor é nulo, então usamos o IS para saber se o valor é igual a NULL.\
```SQL
SELECT name
FROM movies 
WHERE imdb_rating IS NOT NULL;
```
\
Mas também podemos usar o IS para saber se um valor é igual ou diferente.
```SQL
SELECT name FROM movies WHERE imdb_rating IS 7;
```

## BETWEEN
É usado depois do WHERE para selecionar resultados em certos intervalos.
```SQL
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999;
```
\
Quando os valores são textos, o BETWEEN é usado para pegar resultados entre o alcance no alfabeto.
```SQL
SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';
```
Pega valores que começam com a letra A até os que começam com a letra J, porém um filme com nome de "Jaws" não seria selecionado.

## AND
```SQL
SELECT * 
FROM movies
WHERE year BETWEEN 1990 AND 1999
   AND genre = 'romance';
```

## OR
```SQL
SELECT *
FROM movies
WHERE year > 2014
   OR genre = 'action';
```

## ORDER BY
Indica que queremos ordenar os resultados em uma coluna.\
No exemplo abaixo, as colunas vão estar ordenadas em ordem alfabética por que o ORDER BY está ordenando o nome.
```SQL
SELECT *
FROM movies
ORDER BY name;
```

### CRESCENTE E DECRESCENTE
ASC is a keyword used in ORDER BY to sort the results in ascending order (low to high or A-Z).
```SQL
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year ASC;
```

DESC is a keyword used in ORDER BY to sort the results in descending order (high to low or Z-A). 
```SQL
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```

## LIMIT
Para limitar quantos itens a tabela pode ter no máximo.\
No exemplo abaixo, pegamos os top 3 filmes que tem as maiores notas.
```SQL
SELECT * FROM movies ORDER BY imdb_rating DESC LIMIT 3;
```
\
Outro exemplo
```SQL
SELECT *
FROM movies
LIMIT 10;
```

## CASE
Nos permite criar outputs diferentes. Geralmente ele fica depois do SELECT.
```SQL
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END AS 'Review'
FROM movies;
```
\
Outro exemplo:
```SQL
SELECT name,
 CASE
  WHEN genre = 'romance' THEN 'Chill'
  WHEN genre = 'comedy'  THEN 'Chill'
  ELSE 'Intense'
 END AS 'Mood'
FROM movies LIMIT 5;
```
OUTPUT
|name |	Mood|
|:---:|:---:|
|Avatar| 	Intense|
|Jurassic World| 	Intense|
|The Avengers| 	Intense|
|The Dark Knight| 	Intense|
|Star Wars: Episode I - The Phantom Menace| 	Intense|

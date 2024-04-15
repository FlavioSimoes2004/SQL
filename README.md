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

### QUEBRANDO O CÓDIGO
- SELECT is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database.
-  name specifies the column to query data from.
-  FROM celebs specifies the name of the table to query data from. In this statement, data is queried from the celebs table. 
<!-- TESTE -->

Para selecionar todas as colunas de uma tabela, podemos usar o '*' em vez do nome de uma coluna.
```SQL
SELECT * FROM celebs;
```
O '*' seleciona todas as colunas, em vez de ter que nomear cada uma individualmente.

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

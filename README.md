# migrations-lib

> A documentação dessa lib precisa ser revista

Antes fazia parte do `new-singularity`, mas foi movido para um projeto separado, pois não terá atualizações frequentes e poderá ser usado em outros projetos como o `GLSIP`

## migrations-lib/generateMigrations

O método `generateMigrations(folder)` fica observando o diretório enviado e gerando um arquivo no mesmo diretório chamado `migrations.ts`

O método `generateMigrations(folder)` observa os arquivos que seguem o padrão `000-name.ts` ou `1-name.sql`, aonde o número pode ser de qualquer tamanho de número de caracteres, mas sempre será ordenado pelo número

## migrations-lib/better-sqlite3

Possui o método `migrateBetterSQLite3(db, migrations)`, aonde recebe como argumento as migrações geradas no arquivo `migrations.ts`, então faz migrações em um banco de dados `sqlite` usando o `better-sqlite3`

### Utilities para better-sqlite3

Dois métodos simples para reduzir o boilerplate de inserção e update, não são necessários, mas pelo menos reduzem o código para não precisar de um ORM

`insertIntoDB` Método de inserção inspirado no `knex` é chamado da seguinte maneira

```ts
insertIntoDB(db, 'test', { id: 1, name: 'Test' });

// Retornando um valor
const { id } = insertIntoDB(db, 'test', { id: 1, name: 'Test' }, 'id');
```

`updateDB` Método de update inspirado no `knex` é chamado da seguinte maneira

```ts
updateDB(db, 'test', { name: 'Test updated' }, { id: 1 }); // Segundo objeto é where
```

## Características do projeto de migrações

As migrações são sempre para `latest` sem a possibilidade de `down`, pois se você fez uma migração errada em produção você está ferrado de qualquer jeito

O ideal é fazer testes automatizados para garantir que as migrações não ferrem tudo, e evitar refatorar as coisas

## Roadmap

No futuro, poderemos suportar outros bancos de dados além do `sqlite`

### Prisma Notes

### What are ORM?
ORM stands for Object-Relational Mapping, a programming technique used in software development to convert data between incompatible type systems in object-oriented programming languages. This technique creates a "virtual object database" that can be used from within the programming language.
ORMs are used to abstract the complexities of the underlying database into simpler, more easily managed objects within the code
In easier words, ORMs let you easily interact with your database without worrying too much about the underlying syntax (SQL language for eg)

### Why ORMs?
- Simpler syntax (converts objects to SQL queries under the hood)

- Abstraction that lets you flip the database you are using. Unified API irrespective of the DB

- Type safety/Auto completion
  
-  Automatic migrations
In case of a simple Postgres app, it’s very hard to keep track of all the commands that were ran that led to the current schema of the table.
As your app grows, you will have a lot of these CREATE  and ALTER  commands.
ORMs (or more specifically Prisma) maintains all of these for you.

### What is Prisma?
Prisma unlocks a new level of Developer Experience when working with Databases thanks to its intutive 
Data Model
Automated Migrations
Type Safety
Auto Completions

- 1. Data model
In a single file, define your schema. What it looks like, what tables you have, what field each table has, how are rows related to each other.
- 2. Automated migrations
Prisma generates and runs database migrations based on changes to the Prisma schema. 
- 3. Type Safety
Prisma generates a type-safe database client based on the Prisma schema.
- 4. Auto-Completion
  Enables Auto completion while writing code (shows DB tables, columns etc)



### Installing prisma in a fresh app
Let’s create a simple TODO app
 
- Initialize an empty Node.js project
```
npm init -y
```
- Add dependencies
```
npm install prisma typescript ts-node @types/node --save-dev
```
- Initialize typescript
```
npx tsc --init
Change `rootDit` to `src`
Change `outDir` to `dist`
```
- Initialize a fresh prisma project
```
npx prisma init
```
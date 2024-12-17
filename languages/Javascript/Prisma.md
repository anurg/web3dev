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

Next steps:
- 1. Set the DATABASE_URL in the .env file to point to your existing database. If your database has no tables yet, read https://pris.ly/d/getting-started
- 2. Set the provider of the datasource block in schema.prisma to match your database: postgresql, mysql, sqlite, sqlserver, mongodb or cockroachdb.
- 3. Run prisma db pull to turn your database schema into a Prisma schema.
```
npx prisma db pull
```
- 4. Run prisma generate to generate the Prisma Client. You can then start querying your database.
```
npx prisma generate
```

### Selecting your database
Prisma lets you chose between a few databases (MySQL, Postgres, Mongo)
You can update prisma/schema.prisma  to setup what database you want to use. 

### Defining your data model
Prisma expects you to define the shape of your data in the schema.prisma  file
If your final app will have a Users table, it would look like this in the schema.prisma  file
```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  authorId  Int?
  User      User?   @relation(fields: [authorId], references: [id])
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  Post  Post[]
}

```

### Generate migrations
You have created a single schema file. You haven’t yet run the CREATE TABLE  commands. To run those and create migration files , run 
```
npx prisma migrate dev --name Initialize the schema
```

### Generating the prisma client
- What is a client?
Client represents all the functions that convert 
```
User.create({email: "harkirat@gmail.com"})
```
into
```
INSERT INTO users VALUES ...
```
Once you’ve created the prisma/schema.prisma , you can generate these clients  that you can use in your Node.js app

### How to generate the client?
```
npx prisma generate
```
This generates a new client  for you.

### Start Prisma Studio
To view Data in the Database, you can use prisma studio
```
npx prisma studio
```

### Write a function that let’s you insert data in the Users  table.
```
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

interface User {
    id:number;
    email:string;
    name:string;
}
async function insertUser(user:User) {
    await prisma.user.create({
        data:{
            id:user.id,
            email:user.email,
            name:user.name
        }
    })
}
const u1:User = {
    id:1,
    email:"anurg@yahoo.com",
    name:"Anurag"
}
const u2:User = {
    id:2,
    email:"test@yahoo.com",
    name:"Test"
}
insertUser(u1)
insertUser(u2)
```
### Write a function that let’s you update data in the Users  table.
```
async function updateUser(user:User, newEmail:string) {
    const res = await prisma.user.update({
        where:{
            id:user.id
        },
        data:{
            email:newEmail
        }
    })
    console.log(res)
}
updateUser(u1,"anurg@yahoo.com")
```

### Write a function that let’s you fetch the details of a user given their email
```
async function getUser(userId:number) {
    const res = await prisma.user.findUnique({
        where:{
            id:userId
        }
    })
    console.log(res?.email)
}
getUser(1)
getUser(2)
```

### Relationships.
Prisma let’s you define relationships  to relate tables with each other.
1. Types of relationships
- One to One
- One to Many
- Many to One
- Many to Many
 

 For the TODO app, there is a one to many  relationship
 ```
model User {
  id         Int      @id @default(autoincrement())
  username   String   @unique
  password   String
  firstName  String
  lastName   String
  todos      Todo[]
}

model Todo {
  id          Int     @id @default(autoincrement())
  title       String
  description String
  done        Boolean @default(false)
  userId      Int
  user        User    @relation(fields: [userId], references: [id])
}
 ```

-  Update the database  and the prisma client 
```
npx prisma migrate dev --name relationship
npx prisma generate
```
### Write a function to create Post for a User
```
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

async function createPost(title:string,content:string,published:boolean,authorId:number) {
    await prisma.post.create({
        data:{
            title,
            content,
            published,
            authorId
        }
    })
}

createPost("Hello World","Hello World, Prisma Here", true,1)
```
### Write a function to get all the todos for a user.
```
async function getPosts(authorId:number) {
   const posts = await prisma.post.findMany({
        where:{
            authorId
        }
    })
    console.log(posts)
}
 getPosts(1);

```

### getTodosAndUserDetails (Does/should it use joins?)
- Write a function that gives you the todo details of a user along with the user details
```
async function getPostsWithAuthor(authorId:number) {
   const posts= await prisma.post.findMany({
        where:{
            authorId:authorId
        },
        select: {
            author:true,
            title:true,
            content:true,
            published:true,
            
        }
    })
    console.log(posts)
 }

 console.log(getPostsWithAuthor(1))
```
### Select only Name from User table and Post Id in descending order
```
 async function getPostsWithAuthor(authorId:number) {
   const posts= await prisma.post.findMany({
        where:{
            authorId:authorId
        },
        select: {
            author:{
                select:{
                    name:true
                }
            },
            title:true,
            content:true,
            published:true,
            id:true
        },
        orderBy:{
            id:'desc'
        }
    })
    console.log(posts)
 }

 console.log(getPostsWithAuthor(1))
```

### Expressify it - Assignment for this week
    Try creating a todo application that let’s a user signup, put todos and fetch todos. 
Use 
- Typescript as the language
- Prisma as the ORM
- Postgres as the database
- Zod as validation library


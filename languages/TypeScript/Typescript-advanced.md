### Advanced Typescript

### Pick
- Pick allows you to create a new type by selecting a set of properties (Keys) from an existing type (Type).
Imagine you have a User model with several properties, but for a user profile display, you only need a subset of these properties.
```
interface User {
    Id:number;
    name:string;
    email:string;
    createdOn:Date;
}
type UserProfile = Pick<User, 'Id'|'name'>

const displayUserProfile = function(user:UserProfile) {
    console.log(`User Id: ${user.Id} User Name: ${user.name}`)
}

const u1:User = {
    Id:1,
    name:"Anurag",
    email:"anurg@yahoo.com",
    createdOn:new Date()

}
// const u2:UserProfile = u1;
displayUserProfile(u1)
```
### Partial
Partial makes all properties of a type optional, creating a type with the same properties, but each marked as optional.
Specifically useful when you want to do updates
```
interface User {
    id: string;
    name: string;
    age: string;
    email: string;
    password: string;
};

type UpdateProps = Pick<User, 'name' | 'age' | 'email'>

type UpdatePropsOptional = Partial<UpdateProps>

function updateUser(updatedProps: UpdatePropsOptional) {
    // hit the database tp update the user
}
updateUser({})
```

### Readonly
When you have a configuration object that should not be altered after initialization, making it Readonly ensures its properties cannot be changed.

This is compile time checking, not runtime (unlike const)
```
interface Config {
    readonly endpoint:string;
    readonly apikey:string;
}

const config:Readonly<Config> = {
    endpoint: 'https://api.example.com',
    apikey: 'abcdef123456',
}

// config.apikey = "newKey" //Cannot assign to 'apikey' because it is a read-only property.
```
### Record and Map
### Record
Record let’s you give a cleaner type to objects
You can type objects like follows - 
```
interface User {
    id:string;
    name:string
}
type Users = {[key:string]:User}
const users:Users = {
    'abc123':{id:'abc123',name:"Anurag"},
    'xyz123':{id:'xyz123',name:"Zebra"}
}
```
or use Record
```
interface User {
    id:string;
    name:string
}
type Users = Record<string,User>
const users:Users = {
    'abc123':{id:'abc123',name:"Anurag"},
    'xyz123':{id:'xyz123',name:"Zebra"}
}
console.log(users['abc123'])
```
### Map
maps gives you an even fancier way to deal with objects. Very similar to Maps in C++
```
const usersMap = new Map<string,User>()

//Add users to the map using .set
usersMap.set('abc123',{id:'abc123', name:"Anurag"})
usersMap.set('xyz123',{id:'xyz123', name:"Zebra"})

console.log(usersMap.get('xyz123'))
usersMap.forEach(x=>console.log(x.name))
```

### Exclude
In a function that can accept several types of inputs but you want to exclude specific types from being passed to it.
```
type MyEvent = 'click'|'scroll'|'mousemove'
type ExcludeEvent = Exclude<MyEvent,'scroll'>

const handleEvent = (event:ExcludeEvent)=>{
    console.log(`Handling event ${event}`)
}
handleEvent('click');
handleEvent('mousemove')
handleEvent('scroll') //Argument of type '"scroll"' is not assignable to parameter of type 'ExcludeEvent'.
```

### Type inference in zod
When using zod, we’re done runtime validation. 
For example, the following code makes sure that the user is sending the right inputs to update their profile information
More details - https://zod.dev/?id=type-inference 
```
import { z } from 'zod';
import express from "express";

const app = express();

// Define the schema for profile update
const userProfileSchema = z.object({
  name: z.string().min(1, { message: "Name cannot be empty" }),
  email: z.string().email({ message: "Invalid email format" }),
  age: z.number().min(18, { message: "You must be at least 18 years old" }).optional(),
});

app.put("/user", (req, res) => {
  const { success } = userProfileSchema.safeParse(req.body);
  const updateBody = req.body; // how to assign a type to updateBody?

  if (!success) {
    res.status(411).json({});
    return
  }
  // update database here
  res.json({
    message: "User updated"
  })
});

app.listen(3000);
```
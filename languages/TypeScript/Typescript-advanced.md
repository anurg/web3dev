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

```
or use Record
```

```
### Map
maps gives you an even fancier way to deal with objects. Very similar to Maps in C++
```

```

### Exclude
In a function that can accept several types of inputs but you want to exclude specific types from being passed to it.
```

```
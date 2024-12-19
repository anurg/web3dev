### Nextjs temp file

### Server Actions and Mutations
Server Actions are asynchronous functions that are executed on the server. They can be called in Server and Client Components to handle form submissions and data mutations in Next.js applications.

A Server Action can be defined with the React "use server" directive. You can place the directive at the top of an async function to mark the function as a Server Action, or at the top of a separate file to mark all exports of that file as Server Actions.

### Client Components
To call a Server Action in a Client Component, create a new file and add the "use server" directive at the top of it. All exported functions within the file will be marked as Server Actions that can be reused in both Client and Server Components:
file: app/actions.ts
```
'use server'
 
export async function create() {}
```

file:app/ui/button.tsx
```
'use client'
 
import { create } from '@/app/actions'
 
export function Button() {
  return <button onClick={() => create()}>Create</button>
}
```
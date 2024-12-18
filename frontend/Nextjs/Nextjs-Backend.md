### Nextjs Backend
- Next.js is a full stack framework
- This means the same process can handle frontend and backend code.

### Why?
- Single codebase for all your codebase
- No cors issues, single domain name for your FE and BE
- Ease of deployment, deploy a single codebase

### Recap of Data fetching in React

- Example- User card website
Build a website that let’s a user see their name and email from the given endpoint.
https://week-13-offline.kirattechnologies.workers.dev/api/v1/user/details 
![Nextjs-datafetch](../../images/nextjs-datafetch.webp)

```
"use client"

import axios from "axios"
import { useEffect, useState } from "react"

export default function User() {
    const [loading,setLoading] = useState(true)
    const [data,setData] = useState({})
    useEffect(()=>{
        setLoading(true)
        axios.get("https://week-13-offline.kirattechnologies.workers.dev/api/v1/user/details ").then(
            (response)=>{
                
                setData(response.data)
                
            }
        )
        setLoading(false)
    },[])

    if (loading) {
        return <div>
            Loading...
        </div>
    }
  
    return (
        <div>
            User Page
            <div>
                {data?.name}     
            </div>
            <div> 
                {data?.email}
            </div>
            
        </div>
    )
}
```

- Data fetching happens on the client in React
![Waterfalling](../../images/waterfalling_react.webp)
```
import axios from "axios"

export default async function User() {
     const response = await  axios.get("https://week-13-offline.kirattechnologies.workers.dev/api/v1/user/details ")
     const data = response.data
    return (
        <div>
            User Page
            <div>
                {data?.name}     
            </div>
            <div> 
                {data?.email}
            </div>
        </div>
    )
}
```

### Loaders in Next
What if the getUserDetails call takes 5s to finish (lets say the backend is slow). You should show the user a loader during this time.

- loading.tsx file
Just like page.tsx and layout.tsx , you can define a skeleton.tsx file that will render until all the async operations finish
- Create a loading.tsx file in the root folder
- Add a custom loader inside

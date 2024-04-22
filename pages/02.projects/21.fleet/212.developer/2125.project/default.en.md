# Project Structure

```graphql
Project Root
├───prisma
│   ├───seeders
│   │   └───**.seed.ts
│   └───schema.prisma
├───src
│   ├───killbil
│   │   └───**killbill files
│   ├───lib
│   │   ├───actions
│   │   ├───components
│   │   ├───context
│   │   ├───features
│   │   ├───helpers
│   │   ├───images
│   │   ├───mocks
│   │   ├───shared
│   │   ├───store
│   │   ├───zod
│   │   └───**other lib files
│   ├───routes
│   │   ├───(authenticated)
│   │   │   ├───admin
│   │   │   ├───api
│   │   │   ├───clients
│   │   │   ├───contracts
│   │   │   ├───costs
│   │   │   ├───dashboard
│   │   │   ├───**[module folder]
│   │   │   │   ├─── +page.server.ts
│   │   │   │   └─── +page.svelte
│   │   │   ├─── +layout.server.ts
│   │   │   └─── +layout.svelte
│   │   ├───(unauthenticated)
│   │   └───**other routes files
│   └───**other lib files
└───**config files
```

#### [Client Side Structure](./client/)
#### [Api Endpoints Structure](./api/)
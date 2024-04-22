# Api Folder Structure

```graphql
Api root
└───tenants
    └───[[tenantId]]
        ├───client
        │   └───[[clientId]]
        │       └───+server.ts
        └───+server.ts
```
The double square brackets `[[objectId]]` are used to denote optional parameters.

## Documentation for the +server.ts File

### Imports

- **zod**: Used for defining data validation schemas.
- **zod**: Adapter for `sveltekit-superforms` to work with Zod.
- **RequestHandler**: SvelteKit type for handling HTTP requests.
- **superValidate**: Function from `sveltekit-superforms` for form validation.
- **actionResult**: Function from `sveltekit-superforms` for handling action results.
- **actionCreate, actionUpdate, actionDelete, actionList**: Actions defined in `$lib/actions/**` for interacting with objects in the database.

### Validation Schema

The `objectSchema` schema defines the expected structure of object data. It uses Zod to specify validation rules:

- `form_field`: data type

### Request Handlers

#### GET

This request handler retrieves a list of objects using the `actionList` function and returns the list as a JSON response.

#### POST

This request handler validates the received form data against the `objectSchema` using `superValidate`. If validation fails, it returns an action result with a 400 status  i.e(`return actionResult('failure', { form }, { status: 400 })`). 

If validation is successful, it checks if an existing object is being updated or a new one is being created always making use of the global prisma instance located on `locals.currentInstance.currentPrismaClient`.

```jsx
if (params.objectId) {
    await actionUpdate(prismaInstance, {**property});
} else {
	await actionCreate(prismaInstance, {**property});
}
```
Then, it calls `actionUpdate` or `actionCreate` with the form data and returns an action result with a 200 status i.e(`return actionResult('success', { form }, { status: 200 })`).


#### DELETE

This request handler attempts to delete a object using the `actionDelete` function with the provided `objectId`. If deletion is successful, it returns a response with a 204 status i.e(`return new Response(null, { status: 204 })`). If an error occurs, it returns a response with an error message and a 400 status i.e(`return new Response('Deletion failed', { status: 400 })`).

# Routes Folder Structure
```graphql
routes
├───(authenticated)
│   ├───admin
│   ├───api
│   ├───clients
│   ├───contracts
│   ├───costs
│   ├───dashboard
│   ├───**[module folder]
│   │   ├─── +page.server.ts
│   │   └─── +page.svelte
│   ├─── +layout.server.ts
│   └─── +layout.svelte
├───(unauthenticated)
└───**other routes files
```

## Documentation for the +page.server.ts file
In this file, any direct handling of prisma should be avoided. Ideally, only the validation scheme is started and sent to the +page.svelte as data.

### Imports

- **z**: Imported from `zod` to define validation schemas.
- **zod**: Imported from `sveltekit-superforms/adapters` to adapt Zod schemas for use with `sveltekit-superforms`.
- **superValidate**: Imported from `sveltekit-superforms/server` for server-side form validation.
- **PageServerLoad**: Imported as a type from `./$types.js` to ensure the `load` function satisfies the expected type signature.

### Validation Schema

The `objectSchema` schema defines the expected structure of form data. It uses Zod to specify validation rules:

- `form_field`: data type

### Load Function

The `load` function is an asynchronous function that initializes the form using the `superValidate` function with the `objectSchema` schema. It returns an object containing the form data i.e(`return { form: form }`), which is expected to satisfy the `PageServerLoad` type.

In the case of more than one form, the same structure must be made but declaring each form as independent.


## Documentation for the +page.svelte file
In this file, any attemp of use prisma will cause an error.

### Imports

- **Flowbite Svelte Components**: Imported for UI components such as `Card`, `GradientButton`, `Table`, `Modal`, and `Alert`.
- **Flowbite Svelte Icons**: Imported for icons like `TrashBinSolid` or `FileEditSolid`.
- **PageData Type**: Imported as a type for the `data` prop.
- **onMount**: Imported from Svelte for running code after the component mounts.
- **getContext**: Imported from Svelte for accessing context values.
- **axios**: Imported for making HTTP requests.

### Reactive Declarations

- **data**: A prop of type `PageData` passed to the component.

### Lifecycle Hooks

- **onMount**: Used to load data from the api when the component mounts.

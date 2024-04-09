# Project Authentication Documentation

## Auth.js Integration

This project utilizes the authentication library [Auth.js](https://authjs.dev/) to handle user authentication. Auth.js provides a secure and flexible authentication solution for web applications.

### Authentication Providers

#### 1. Google Authentication

We currently support [Google](https://authjs.dev/reference/core/providers/google) authentication as one of our authentication providers. Users can log in using their Google accounts. To enable Google authentication, developers must whitelist their Gmail accounts in the Google app configuration. Additionally, ensure that your Gmail account is included in the seeding data.

#### 2. EmailProvider Authentication

[EmailProvider](https://authjs.dev/getting-started/providers/email-tutorial?frameworks=sveltekit) authentication is also supported in the project. Users can log in using their email addresses associated with supported email providers. Make sure to include your email in the seeding data for testing purposes.

#### 3. Future Support - Email/Password

In the future, we plan to support authentication using email and password. Developers should stay updated on project releases for information on when this feature will be available.

### Access Request for New Developers

To gain access to the project, new developers must follow these steps:

1. **Whitelist Gmail Account:**
   - Add your Gmail account to the whitelist in the Google app configuration.

2. **Include Email in Seeding Data:**
   - Include your email address in the seeding data for testing purposes.

By completing these steps, new developers ensure smooth access to the authentication system during development and testing phases.

### Example Seeding Data:

```json
{
    "email": "developer_email@gmail.com", 
    "userRole": Role.ADMIN, 
    "companyId": admin_company.id
}
```

### Note:
- Keep your credentials secure and do not share them with unauthorized individuals.
- Stay informed about updates to Auth.js and other authentication providers integrated into the project.

For any questions or issues related to authentication, please contact the project's support team.

Thank you for contributing to the project!

## Decorator
Yes, you can use TypeScript decorators to achieve this kind of functionality. Decorators in TypeScript allow you to add metadata or modify the behavior of classes, methods, or properties at design time.

Here's how you can create a decorator to handle authentication:

```typescript
import { Response } from 'some-response-library'; // Import the response library you are using

// Define a decorator function that checks if the user is authenticated
export function loginRequired(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    descriptor.value = async function (...args: any[]) {
        const locals = args[0].locals; // Assuming locals is passed as the first argument
        const session = await locals.getSession();
        
        if (!session?.user) {
            return new Response('Forbidden', { status: 403 });
        }

        return originalMethod.apply(this, args);
    };

    return descriptor;
}
```

Now, you can use `@loginRequired` decorator on your methods that require authentication:

```typescript
import { RequestHandler } from 'some-request-handler-library'; // Import the request handler library you are using

export const DELETE: RequestHandler = async ({ locals, params }) => {
    const instance = locals.inventoryActionObject.currentPrismaClient;

    if (params.vehicleId) {
        await deleteTracker(instance, {
            id: parseInt(params.vehicleId)
        });
        return new Response("Deleted", { status: 200 });
    } else {
        return new Response("Invalid Request", { status: 400 });
    }
}

// Apply the decorator to your function
export const securedDELETE: RequestHandler = loginRequired(DELETE);
```

In this setup, the `securedDELETE` function will now first check if the user is authenticated before executing the actual logic defined in the `DELETE` function. You can apply the `@loginRequired` decorator to any other functions that need authentication in your codebase.

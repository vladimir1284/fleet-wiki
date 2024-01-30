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
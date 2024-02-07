# User Model

Represents a user in the system.

Fields:

- `id`: Unique identifier for the user.
- `name`: Name of the user.
- `email`: Email address of the user, must be unique.
- `emailVerified`: Datetime when the user's email was verified.
- `image`: URL to the user's profile picture.

Relationships:

- `accounts`: One-to-many relationship with the `Account` model, representing the user's linked accounts.
- `sessions`: One-to-many relationship with the `Session` model, representing the user's active sessions.
- `tenantUsers`: One-to-many relationship with the `TenantUser` model, representing the user's tenants.

---

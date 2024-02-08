# Tenants and Users

## User Model

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

## Tenant Model

Represents a tenant in the system.

Fields:

- `id`: Unique identifier for the tenant.
- `name`: Name of the tenant.
- `email`: Email address of the tenant.
- `isAdmin`: Flag indicating whether the tenant is an admin.

Relationships:

- `clients`: One-to-many relationship with the `Client` model, representing the tenant's clients.
- `tenantUsers`: One-to-many relationship with the `TenantUser` model, representing the tenant's users.
---

## TenantUser Model

Represents the association between a user and a tenant with a specific role.

Fields:

- `id`: Unique identifier for the tenant user record.
- `role`: Role of the user within the tenant (e.g., STAFF, ADMIN, OWNER).
- `tenantId`: Associated tenant ID.
- `userId`: Associated user ID.

Relationships:

- `tenant`: One-to-one relationship with the `Tenant` model, indicating the tenant of the user.
- `user`: One-to-one relationship with the `User` model, indicating the user of the tenant.


### Role Enum

Defines the possible roles a user can have within a tenant.

Values:

- `STAFF`: Indicates a staff member role.
- `ADMIN`: Indicates an administrator role.
- `OWNER`: Indicates an owner role.

---

<iframe width="100%" height="640" src='https://dbdiagram.io/e/65c4fcc4ac844320aebff1bd/65c4fdf5ac844320aec00c0d'> </iframe>
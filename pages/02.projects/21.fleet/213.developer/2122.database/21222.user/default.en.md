# Tenant and User Models Explanation

In a system with a multi-tenant architecture, the concepts of **tenant** and **user** play crucial roles in managing access to data and resources. Below is an explanation of the tenant and user models, with a focus on a special tenant called **admin**.

<iframe width="100%" height="640" src='https://dbdiagram.io/e/65c4fcc4ac844320aebff1bd/65c4fdf5ac844320aec00c0d'> </iframe>


## User Model

A **User** is an individual entity with a unique identity (an email) within the system. Each user must be associated with at least one tenant, referred to as a **TenantUser**. Furthermore, a user can have multiple **TenantUser** associations, with one of them designated as the default.

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


A **tenant** represents a distinct and isolated environment within the system, typically associated with a specific organization, group, or entity. In the described scenario, there is a special tenant known as **admin**. The admin tenant holds a unique position, granting its users unrestricted access to all data in the database. Other tenants are subject to more restrictive access policies.

## Fields

- `id`: A unique identifier for each `Tenant`. It's an auto-incrementing integer.
- `name`: The name of the tenant.
- `email`: The email address of the tenant. It's optional and not unique.
- `isAdmin`: A boolean flag indicating whether the tenant is an admin. It defaults to `false`.
- `clients`: A one-to-many relationship with the `Client` model, indicating the clients associated with this tenant.
- `tenantUsers`: A one-to-many relationship with the `TenantUser` model, indicating the users associated with this tenant.
- `parts`: A one-to-many relationship with the `Part` model, indicating the parts associated with this tenant.
- `categories`: A one-to-many relationship with the `Category` model, indicating the categories associated with this tenant.
- `locations`: A one-to-many relationship with the `Location` model, indicating the locations associated with this tenant.
- `vendors`: A one-to-many relationship with the `Vendor` model, indicating the vendors associated with this tenant.
- `customForms`: A one-to-many relationship with the `CustomForm` model, indicating the custom forms associated with this tenant.
- `inspections`: A one-to-many relationship with the `Inspection` model, indicating the inspections associated with this tenant.

## Relationships

- `clients`: A one-to-many relationship with the `Client` model, indicating the clients associated with this tenant.
- `tenantUsers`: A one-to-many relationship with the `TenantUser` model, indicating the users associated with this tenant.
- `parts`: A one-to-many relationship with the `Part` model, indicating the parts associated with this tenant.
- `categories`: A one-to-many relationship with the `Category` model, indicating the categories associated with this tenant.
- `locations`: A one-to-many relationship with the `Location` model, indicating the locations associated with this tenant.
- `vendors`: A one-to-many relationship with the `Vendor` model, indicating the vendors associated with this tenant.
- `customForms`: A one-to-many relationship with the `CustomForm` model, indicating the custom forms associated with this tenant.
- `inspections`: A one-to-many relationship with the `Inspection` model, indicating the inspections associated with this tenant.


## Special Annotations

- The `isAdmin` field is a boolean with a default value of `false`.

### Special Tenant: Admin

- **Access Privileges:** Users belonging to the **admin** tenant have elevated privileges, allowing them to access all data within the system without restrictions.

---

## TenantUser Model


- **Definition:** A link between a user and a specific tenant, defining the user's access privileges within that tenant.

- **Minimum Requirement:** Every user must have at least one associated tenantUser to establish their connection to a specific tenant.

- **Default TenantUser:** If a user has multiple tenantUser associations, one of them must be marked as the default. The default tenantUser is the primary association used for access control by default.

Fields:


- `id`: A unique identifier for each `TenantUser`. It's an auto-incrementing integer.
- `role`: Defines the user's role within the tenant. It can be `STAFF`, `ADMIN`, or `OWNER`, as defined by the `Role` enum.
- `tenantId`: The identifier of the tenant the user belongs to. It's a foreign key referencing the `Tenant` model.
- `tenant`: A relation to the `Tenant` model, indicating which tenant the user is associated with.
- `userId`: The identifier of the user. It's a foreign key referencing the `User` model.
- `user`: A relation to the `User` model, indicating which user is associated with this tenant user entry.
- `is_default`: A boolean flag indicating whether this tenant user is the default for the tenant.
Relationships:

- `tenant`: One-to-one relationship with the `Tenant` model, indicating the tenant of the user.
- `user`: One-to-one relationship with the `User` model, indicating the user of the tenant.


## Relationships

- `createdParts`: A one-to-many relationship with the `Part` model, indicating which parts were created by this tenant user.
- `updatedParts`: A one-to-many relationship with the `Part` model, indicating which parts were last updated by this tenant user.
- `deletedParts`: A one-to-many relationship with the `Part` model, indicating which parts were deleted by this tenant user.
- `customFieldResponses`: A one-to-many relationship with the `CustomFieldResponse` model, indicating the responses provided by this tenant user to custom fields.
- `inspections`: A one-to-many relationship with the `Inspection` model, indicating the inspections conducted by this tenant user.


## Special Annotations

- The `role` field uses the `Role` enum, which is defined in the schema.
- The `tenantId` and `userId` fields are foreign keys, establishing relationships with the `Tenant` and `User` models.
- The `is_default` field is a boolean with a default value of `false`.


### Role Enum

Defines the possible roles a user can have within a tenant.

Values:

- `STAFF`: Indicates a staff member role.
- `ADMIN`: Indicates an administrator role.
- `OWNER`: Indicates an owner role.


### Admin Tenant

- **Access Level:** Users from the **admin** tenant enjoy unrestricted access to all data in the database.

### Other Tenants

- **Access Requirement:** Users outside the **admin** tenant must have an active **TenantUser** after logging in to access authenticated routes.

- **Persisting TenantUser Election:** The system should persist the user's chosen **TenantUser**, especially in the session model. This ensures that the user's access preferences are maintained across different interactions and sessions.

By implementing these tenant and user models, the system can achieve a flexible and secure access control mechanism, allowing for granular control over data access based on tenants and users' roles within those tenants.

---
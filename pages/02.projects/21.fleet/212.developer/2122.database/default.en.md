# Database documentation

## PostgreSQL: A Powerful Relational Database Management System

In our project, we have chosen PostgreSQL as the relational database management system (RDBMS) for its robustness, extensibility, and support for advanced features. PostgreSQL is known for its adherence to SQL standards, ACID compliance, and scalability, making it an ideal choice for our [SaaS](https://en.wikipedia.org/wiki/Software_as_a_service) product.

### Multi-Tenant Data Isolation with PostgreSQL Row Level Security

To ensure proper data isolation in our SaaS product, we will implement Multi-Tenant Data Isolation using PostgreSQL Row Level Security (RLS). This approach allows us to control access to rows in database tables based on the characteristics of the user executing a query. 

!!! For a more in-depth understanding of this implementation, we recommend reading [**Multi-Tenant Data Isolation with PostgreSQL Row Level Security on AWS** Blog](https://aws.amazon.com/es/blogs/database/multi-tenant-data-isolation-with-postgresql-row-level-security/).

## Prisma: An Advanced Database Access Toolkit

[Prisma](https://www.prisma.io/) serves as our Object-Relational Mapping (ORM) tool, simplifying database interactions and providing a type-safe and auto-generated query API. Its versatility and ease of use make it an excellent choice for our project.

### Integrating Prisma Client with PostgreSQL Row Level Security

For seamless integration of Prisma Client with PostgreSQL Row Level Security, developers should refer to the guide available at the repository [Prisma Client Extension - Row Level Security](https://github.com/prisma/prisma-client-extensions/tree/main/row-level-security). It's important to note that while Prisma automates SQL migrations, modifications are required for supporting Row Level Security functionality.

For instance, for the following migration code:
```sql
-- CreateTable
CREATE TABLE "Client" (
    "id" TEXT NOT NULL,
    "name" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "phoneNumber" TEXT NOT NULL,
    "avatar" TEXT,
    "companyId" TEXT NOT NULL,

    CONSTRAINT "Client_pkey" PRIMARY KEY ("id")
);
```
We need to write the following sentences:
```sql
ALTER TABLE "Client" ENABLE ROW LEVEL SECURITY;
CREATE POLICY tenant_isolation_policy ON "Client" USING ("companyId" = current_setting('app.current_company_id', TRUE)::text);
CREATE POLICY bypass_rls_policy ON "Client" USING (current_setting('app.bypass_rls', TRUE)::text = 'on');

```
For the isolation and bypass policies.


## Superforms: Powerful Form Validation

In our project, we utilize Superforms for efficient form validation. Superforms leverages Zod schemas, which are automatically generated from the Prisma schema using the `zod-prisma-types` library. This integration ensures that our forms are validated against the expected data structure, enhancing data integrity.

- [Superforms Documentation](https://superforms.rocks/get-started)
- [zod-prisma-types on GitHub](https://github.com/chrishoermann/zod-prisma-types)

## Model Documentation

! Developers are responsible for documenting the models added by them into the database. 

We encourage the use of visual diagrams illustrating the relationships and structures of the database tables they create. This documentation ensures clarity and understanding of the database schema, facilitating collaboration and maintenance.
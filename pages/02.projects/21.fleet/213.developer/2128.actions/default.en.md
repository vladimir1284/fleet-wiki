# Creating an Action File in SvelteKit with Prisma

This document provides a step-by-step guide on how to create an action file in a SvelteKit application using Prisma for database operations. Prisma is a powerful ORM (Object-Relational Mapping) tool that simplifies database access and manipulation in Node.js and TypeScript applications.


## Step 1: Define Your Model

In the `schema.prisma` file, define your `Object` model to match the structure of your database table.

## Step 2: Create the Action File

Create a new file in your SvelteKit project, for example, `src/lib/actions/**object.ts`. This file will contain the functions for listing, creating, updating, and deleting.

## Step 3: Import Prisma Client
`import type { PrismaClient } from '@prisma/client';`


## Step 4: Define Action Types
```
type createObjectType = { **property: **type;}; 
type updateObjectType = createObjectType & { id: number };
```
#### Note: id property must be number type


## Step 5: Implement CRUD Operations

```
export const listObjects = async (instance: PrismaClient) => {
    const objects = await instance.object.findMany(); 
    return objects; 
};

export const createObject = async ( instance: PrismaClient, { **property }: createObjectType ) => { 
    const object = await instance.object.create(
            { data: { 
                **property
                } 
            }); 
    return object; 
};

export const updateObject = async ( instance: PrismaClient, { **property }: updateObjectType ) => {
    const object = await instance.object.update(
        { where: { 
            id 
        }, 
        data: { **property } 
        }
    ); 
    return object; 
};

export const deleteObject = async (instance: PrismaClient, { id }:{ id: number }) => { 
    await instance.object.delete(
        { where: { 
            id 
            } 
            }); 
    };
```

## Step 6: Use the Action File in Api Endpoints

In your SvelteKit endpoints (e.g., `src/routes/api/tenant/[[tenantId]]clients/+server.ts`), import and use the action functions to perform CRUD operations.



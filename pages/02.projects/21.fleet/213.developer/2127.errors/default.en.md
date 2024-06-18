# Common Errors in SvelteKit Applications

This document outlines common errors that developers might encounter while working with SvelteKit applications.

## Error Objects

SvelteKit distinguishes between expected and unexpected errors, both of which are represented as simple `{ message: string }` objects by default. You can add additional properties, like a `code` or a tracking `id`, as shown in the examples below. When using TypeScript, this requires you to redefine the `Error` type as described in type safety.

## Expected and Unexpected Errors

- **Expected Errors**: Created with the `error` helper from `@sveltejs/kit`. These errors indicate that the developer knows what they are doing and is handling the error intentionally.
  
## "document is not defined" Error

One of the most common errors in SvelteKit is the `document is not defined` error. This occurs when you try to access the `document` object inside a `script` tag or import a function that uses the `document` object. To fix this error, use the `browser` module from SvelteKit to check if you are in the browser or the server, or use the `onMount` lifecycle function from `svelte` to run code that uses the `document` object.

## "window is not defined" Error

Similar to the "document is not defined" error, the "window is not defined" error occurs when trying to access the `window` object in a server-side context.

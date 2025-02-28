---
title: mockResolve hook
description: Reference documentation for the mockResolve hook
---

The `mockResolve` hook, as the name indicates,
can be used to mock the response of an Operation.
During development, the real server might not be available,
or you don't want to make a real request, e.g. a write operation to a database.

In this case, you can use the `mockResolve` hook to mock the response of an Operation.
The actual resolver will be skipped in this case.

Similar to all other hooks,
the `customResolve` hook is called with the following parameters:

- `user`: The user object when the user is authenticated
- `clientRequest`: The original client request object, including Headers
- `log`: The logger object
- `operations`: The operations client, used to call other (internal) operations
- `internalClient`: The internal client object, _deprecated_
- `response`: The response object (only for postResolve hooks)
- `input`: The input object (only for Operation hooks)

With the `operations` client,
you're able to securely call into all defined Operations,
e.g. to talk to a database or another service to enrich a response or manipulate the inputs of an Operation.

```typescript
// wundergraph.server.ts
export default configureWunderGraphServer(() => ({
  hooks: {
    queries: {
      Dragons: {
        mockResolve: async (hook) => {
          return {
            data: {
              dragons: [
                {
                  name: 'Dragon 1',
                },
              ],
            },
          };
        },
      },
    },
  },
}));
```

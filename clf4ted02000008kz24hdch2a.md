---
title: "How to create and use path alias in TypeScript imports with Vite"
datePublished: Sun Mar 12 2023 03:07:04 GMT+0000 (Coordinated Universal Time)
cuid: clf4ted02000008kz24hdch2a
slug: how-to-create-and-use-path-alias-in-typescript-imports-with-vite
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678591488108/9ed4041d-9d57-4d63-81c9-8ec90d18ab70.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678591500601/765a9673-2084-4688-aa24-18f9729f1871.png
tags: javascript, reactjs, typescript, vite

---

Path aliases are a powerful tool for simplifying imports in your TypeScript projects. Instead of writing out long file paths, you can use a short alias to reference a specific directory or module. In this tutorial, I'll show you how to set up a simple path alias for `@` that points to the `src` directory using the Vite build tool.

### Step 1: Set Up Path Alias in tsconfig.json

The first step is to set up your path alias in your `tsconfig.json` file. Open that file and add a `paths` property to the `compilerOptions` object. For example:

```json
"compilerOptions": {
  "baseUrl": ".",
  "paths": {
    "@/*": ["src/*"]
  }
}
```

This sets up a path alias for `@` that points to the `src` directory. The `baseUrl` property specifies the base directory for resolving non-relative module names.

### Step 2: Set Up Path Alias in Vite Config

Next, we need to tell Vite how to resolve our path alias. Open your Vite configuration file (`vite.config.ts` or `vite.config.js`) and add a `resolve.alias` property to the object. For example:

```javascript
import { defineConfig } from 'vite';
import path from 'path';

export default defineConfig({
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  }
});
```

This maps the `@` path alias to the `src` directory using the `path.resolve` method to get the full file path.

### Step 3: Use Path Alias in TypeScript Imports

With our path alias set up, we can now use it in our TypeScript imports. For example:

```typescript
import React from 'react';
import { Button } from '@/components/Button';

function MyComponent() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  );
}

export default MyComponent;
```

This imports the `Button` component from the `src/components/Button.tsx` file using the `@` path alias. Note that we don't need to write out the full file path to this module – we can use our path alias instead.

### Conclusion

By creating a simple path alias for `@` that points to the `src` directory, we can simplify our imports and make our TypeScript code more readable. This is just a basic example of what's possible with path aliases – you can create as many aliases as you need, and use wildcard characters to match any file or folder names that come after the path alias.
<p align="center">
  <a href="https://cmmv.io/" target="blank"><img src="https://raw.githubusercontent.com/cmmvio/docs.cmmv.io/main/public/assets/logo_CMMV2_icon.png" width="300" alt="CMMV Logo" /></a>
</p>
<p align="center">Contract-Model-Model-View (CMMV) <br/> Building scalable and modular applications using contracts.</p>
<p align="center">
    <a href="https://www.npmjs.com/package/@cmmv/tsconfig"><img src="https://img.shields.io/npm/v/@cmmv/tsconfig.svg" alt="NPM Version" /></a>
    <a href="https://github.com/cmmvio/cmmv-tsconfig/blob/main/LICENSE"><img src="https://img.shields.io/npm/l/@cmmv/tsconfig.svg" alt="Package License" /></a>
</p>

<p align="center">
  <a href="https://cmmv.io">Documentation</a> &bull;
  <a href="https://github.com/cmmvio/cmmv-tsconfig/issues">Report Issue</a>
</p>

# @cmmv/tsconfig

Base TypeScript configurations for CMMV projects.

## Installation

```bash
npm install --save-dev @cmmv/tsconfig
# or
yarn add -D @cmmv/tsconfig
# or
pnpm add -D @cmmv/tsconfig
```

## Usage

This package provides eleven base TypeScript configurations:

-   `tsconfig.base.json` - Base configuration for all projects
-   `tsconfig.node.json` - Configuration for Node.js/backend projects using CommonJS
-   `tsconfig.node-esm.json` - Configuration for Node.js/backend projects using ES Modules
-   `tsconfig.web.json` - Configuration for web/frontend projects
-   `tsconfig.build-cjs.json` - Configuration for building libraries in CommonJS format
-   `tsconfig.build-esm.json` - Configuration for building libraries in ESM format
-   `tsconfig.spec.json` - Configuration for test files
-   `tsconfig.vue.json` - Base configuration for Vue.js projects
-   `tsconfig.vue-app.json` - Configuration for Vue.js application source files
-   `tsconfig.vue-node.json` - Configuration for Vue.js build tools
-   `tsconfig.vue-vitest.json` - Configuration for Vue.js testing with Vitest

### Base Configuration

Extend the base configuration in your `tsconfig.json`:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.base.json",
    "compilerOptions": {
        // Override or add additional options here
    }
}
```

### Node.js Configuration (CommonJS)

For Node.js projects using CommonJS:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.node.json",
    "compilerOptions": {
        // Override or add additional options here
    }
}
```

### Node.js Configuration (ES Modules)

For Node.js projects using ES Modules:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.node-esm.json",
    "compilerOptions": {
        // Override or add additional options here
    }
}
```

For Node.js ESM projects, you should also add `"type": "module"` to your package.json.

### Web Configuration

For web projects (React, Vue, etc.):

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.web.json",
    "compilerOptions": {
        // Override or add additional options here
    }
}
```

### Test Configuration

For test files (spec and test files):

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.spec.json",
    "compilerOptions": {
        // Override or add additional options here
    }
}
```

This configuration automatically includes all `*.spec.ts` and `*.test.ts` files while excluding node_modules, dist, and generated files.

### Vue.js Configuration

For Vue.js projects, this package provides a set of configuration files to support application development, build tools, and testing.

#### Vue Base Configuration

Create a `tsconfig.json` file that extends the Vue base configuration:

```json
{
  "extends": "@cmmv/tsconfig/tsconfig.vue.json"
}
```

The Vue base configuration automatically references the app, node, and test configurations needed for a complete Vue project.

#### Vue App Configuration

For Vue application source files, use:

```json
{
  "extends": "@cmmv/tsconfig/tsconfig.vue-app.json",
  "compilerOptions": {
    // Override or add additional options here
  }
}
```

#### Vue Build Tools Configuration

For build tools configuration (Vite, etc.):

```json
{
  "extends": "@cmmv/tsconfig/tsconfig.vue-node.json",
  "compilerOptions": {
    // Override or add additional options here
  }
}
```

#### Vue Testing Configuration

For Vitest testing configuration:

```json
{
  "extends": "@cmmv/tsconfig/tsconfig.vue-vitest.json",
  "compilerOptions": {
    // Override or add additional options here
  }
}
```

### Dual Package Builds (CJS & ESM)

For libraries that need to support both CommonJS and ESM formats, you can use the build configurations:

#### Setup Main tsconfig.json

First, create your base `tsconfig.json`:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.base.json",
    "compilerOptions": {
        // Your base configuration
    },
    "include": ["src/**/*.ts", "src/**/*.tsx"],
    "exclude": ["node_modules", "dist"]
}
```

#### Setup CommonJS Build

Create `tsconfig.cjs.json`:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.build-cjs.json",
    "include": ["src/**/*.ts", "src/**/*.tsx"]
}
```

#### Setup ESM Build

Create `tsconfig.esm.json`:

```json
{
    "extends": "@cmmv/tsconfig/tsconfig.build-esm.json",
    "include": ["src/**/*.ts", "src/**/*.tsx"]
}
```

#### Configure package.json

Update your `package.json` to support both module formats:

```json
{
    "name": "your-package",
    "version": "1.0.0",
    "main": "dist/cjs/index.js",
    "module": "dist/esm/index.js",
    "types": "dist/types/index.d.ts",
    "exports": {
        ".": {
            "import": "./dist/esm/index.js",
            "require": "./dist/cjs/index.js"
        }
    },
    "scripts": {
        "build": "cmmv build"
    }
}
```

This setup allows your package consumers to use either:

-   CommonJS (`require('your-package')`)
-   ES Modules (`import { something } from 'your-package'`)
-   TypeScript with full type definitions

## Features

### Base Configuration

-   CommonJS module system
-   Node.js module resolution
-   ES Next target
-   TypeScript decorators enabled
-   Path aliases for common project directories
-   Reasonable defaults for CMMV projects

### Node.js Configuration

-   Everything from base, plus:
-   ES2022 target
-   Stricter type checking
-   Optimized for Node.js backend development

### Node.js ESM Configuration

-   Support for ECMAScript Modules (ESM)
-   Uses "NodeNext" module system
-   Preserves decorator metadata
-   Optimized for modern Node.js development
-   Full support for top-level await and dynamic imports
-   Compatible with packages requiring ESM

### Build Configurations

#### CommonJS Build Configuration

-   Optimized for library distribution in CommonJS format
-   ES2018 target for broad compatibility
-   Generates types in a separate directory
-   Preserves source maps for debugging
-   Strips internal comments for cleaner output
-   Compatible with Node.js versions 10+

#### ESM Build Configuration

-   Produces modern ESM output with ESNext features
-   ES2020 target for better tree-shaking
-   Bundler-friendly module resolution
-   Generates compatible type definitions
-   Preserves source maps
-   Optimized for modern bundlers

### Web Configuration

-   Modern ES target
-   ESNext module system with bundler resolution
-   DOM and DOM.Iterable library types
-   JSX support
-   Path aliases for web component frameworks
-   Stricter type checking
-   Vue, React, and other framework support

## Path Aliases

The configurations include path aliases to make imports cleaner:

```typescript
// Instead of
import something from "../../models/something";

// You can use
import something from "@models/something";
```

### Base Path Aliases

-   `@models/*` - `src/models/*`
-   `@services/*` - `src/services/*`
-   `@controllers/*` - `src/controllers/*`
-   `@entities/*` - `src/entities/*`
-   And more (see tsconfig files for complete list)

### Web Path Aliases

-   `@components/*` - `src/components/*`
-   `@pages/*` - `src/pages/*`
-   `@hooks/*` - `src/hooks/*`
-   `@stores/*` - `src/stores/*`
-   `@assets/*` - `src/assets/*`
-   And more (see `tsconfig.web.json` for complete list)

## License

MIT

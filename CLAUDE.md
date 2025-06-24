# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- `npm run build` - Clean and compile TypeScript to dist/
- `npm run clean` - Remove dist/ directory  
- `npm run lint` - Run TSLint on source and test files
- `npm run lint:fix` - Auto-fix linting issues
- `npm test` - Run full test suite with coverage (includes pretest: build + lint)
- `npm run start` - Watch mode compilation
- `npm run tsc` - TypeScript compilation only

Test files are in `test/` with Jest configuration at `test/jest.config.js`. Coverage reports go to `reports/coverage/` with 80% threshold requirements.

## Architecture Overview

This is a TypeScript IoC (Inversion of Control) container library using decorator-based dependency injection. The architecture follows these key patterns:

### Core Components

- **Container**: Main public API (`src/typescript-ioc.ts`, `src/container/container.ts`)
- **IoCContainer**: Internal container implementation with binding management
- **Decorators**: Annotation-based DI (`@Inject`, `@Singleton`, `@Factory`, etc.)
- **Scopes**: Instance lifecycle management (Singleton, Request, Local)
- **Namespaces**: Environment-based configuration isolation

### Key Architecture Details

- Uses `reflect-metadata` for runtime type reflection
- Supports constructor and property injection
- Implements custom scoping with `Scope` abstract class
- Namespace system allows multiple configurations (test/prod environments)
- Snapshot system for temporary configuration changes (useful for testing)
- Build context pattern for request-scoped instances

### File Structure

- `src/typescript-ioc.ts` - Main export and public Container class
- `src/container/` - Core container implementation
- `src/decorators.ts` - All DI decorators (@Inject, @Singleton, etc.)
- `src/scopes.ts` - Scope implementations
- `src/model.ts` - Type definitions and interfaces
- `test/` - Unit and integration tests with Jest

### TypeScript Configuration

Requires `experimentalDecorators: true`, `emitDecoratorMetadata: true`, and `target: "es6"` minimum in tsconfig.json.
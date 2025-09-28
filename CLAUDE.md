# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a TypeScript type definitions library for the Polymarket API (`@nivalis/polymarket-api-types`). It provides comprehensive type definitions for all Polymarket API entities including events, markets, teams, users, trades, and more. The package exports only TypeScript types with no runtime code.

## Essential Commands

### Package Management
```bash
# Install dependencies (preferred)
pnpm install

# Alternative
bun install
```

### Development Commands
```bash
# Lint and format check
pnpm run lint

# Auto-fix linting and formatting issues
pnpm run lint:fix

# Type check declarations
pnpm run ts
```

### Task Completion Checklist
When completing any work:
1. Run `pnpm run lint:fix` to format and fix issues
2. Run `pnpm run ts` to verify TypeScript declarations
3. Use conventional commit format (enforced by commitlint)

## Code Architecture

### Type System Pattern
The project uses a sophisticated TypeScript pattern with:
- **Tagged types** for type safety: `Datetime`, `Integer`, `Float`, `Uri`
- **Maybe pattern** for optional properties: `Maybe<T> = (T | null) | Marker`
- **NormalizeMaybes utility** that converts Maybe types to proper TypeScript optionals

Example pattern:
```typescript
export type SomeType = NormalizeMaybes<{
  required: string;
  optional: Maybe<string>;
  timestamp: Datetime;
  count: Integer;
}>;
```

### File Structure
- `index.d.ts` - Single file containing all type definitions
- Type utilities first (Tagged, Maybe, NormalizeMaybes)
- Core entity types in logical order
- All exports use `export type` syntax

### TypeScript Configuration
- Strict mode enabled with ESNext target
- Declaration-only output (`emitDeclarationOnly: true`)
- Extends @nivalis/biome-config for consistent formatting

## Development Notes

- **No build step required** - declaration files only
- **No tests** - type-only package
- **Git hooks** automatically run biome check and commitlint
- **ESM module** with `./index.d.ts` as only export
- Uses **hex string types** `0x${string}` for blockchain addresses
- **Array syntax**: Always use `Array<Type>` instead of `Type[]`
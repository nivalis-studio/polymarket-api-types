# @nivalis/polymarket-api-types

[![npm version](https://badge.fury.io/js/@nivalis%2Fpolymarket-api-types.svg)](https://badge.fury.io/js/@nivalis%2Fpolymarket-api-types)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

TypeScript type definitions for the Polymarket API, providing comprehensive type safety for prediction market interactions.

## Features

- 🎯 **Complete Type Coverage** - All Polymarket API entities typed
- 🔒 **Type Safety** - Branded types for enhanced compile-time safety
- 🚀 **Zero Runtime** - Pure TypeScript declarations, no runtime overhead
- 📦 **Lightweight** - Only type definitions, no dependencies
- 🔧 **Developer Friendly** - Intelligent optional property handling

## Installation

```bash
npm install @nivalis/polymarket-api-types
```

Or with your preferred package manager:

```bash
pnpm add @nivalis/polymarket-api-types
bun add @nivalis/polymarket-api-types
yarn add @nivalis/polymarket-api-types
```

## Usage

```typescript
import type { Event, Market, Trade, Profile } from '@nivalis/polymarket-api-types';

// Use types for API responses
const event: Event = {
  id: "event-123",
  title: "Will Bitcoin reach $100k by 2024?",
  slug: "bitcoin-100k-2024",
  createdAt: "2024-01-01T00:00:00Z" as Datetime,
  updatedAt: "2024-01-01T00:00:00Z" as Datetime,
  // ... other properties
};

const market: Market = {
  id: "market-456",
  question: "Yes or No?",
  slug: "bitcoin-100k-yes-no",
  conditionId: "0x1234567890abcdef",
  createdAt: "2024-01-01T00:00:00Z" as Datetime,
  updatedAt: "2024-01-01T00:00:00Z" as Datetime,
  // ... other properties
};

// Type-safe trading data
const trade: Trade = {
  conditionId: "0x1234567890abcdef",
  eventSlug: "bitcoin-100k-2024",
  proxyWallet: "0xabcdef1234567890",
  transactionHash: "0x9876543210fedcba",
  side: "BUY",
  price: 0.65,
  size: 100,
  timestamp: 1704067200,
  // ... other properties
};
```

## Type System

This library uses an advanced TypeScript pattern for enhanced type safety:

### Branded Types

```typescript
type Datetime = Tagged<string, 'DateTime'>;
type Integer = Tagged<number, 'Int'>;
type Float = Tagged<number, 'Float'>;
type Uri = Tagged<string, 'Uri'>;
```

### Smart Optional Properties

The library uses a `Maybe<T>` pattern that gets normalized to proper TypeScript optional properties:

```typescript
// Internal definition
type RawEvent = {
  id: string;
  title: string;
  description: Maybe<string>; // Optional
  featured: Maybe<boolean>;   // Optional
};

// Exported as
export type Event = NormalizeMaybes<RawEvent>;
// Results in: { id: string; title: string; description?: string; featured?: boolean; }
```

### Blockchain Types

Ethereum addresses and transaction hashes use template literal types:

```typescript
type Address = `0x${string}`;
type TransactionHash = `0x${string}`;
```

## Available Types

### Core Entities
- `Event` - Prediction market events
- `Market` - Individual markets within events  
- `Trade` - Trading transactions
- `Activity` - User activity feed items
- `Profile` - User profiles
- `Position` - User positions

### Supporting Types
- `Category` - Market categories
- `Collection` - Event collections
- `Series` - Event series
- `Team` - Sports teams
- `Sport` - Sports metadata
- `Tag` - Content tags
- `Comment` - User comments
- `Reaction` - Comment reactions
- `Chat` - Chat channels
- `Template` - Event templates

### Utility Types
- `ImageOptimized` - Optimized image metadata
- `EventCreator` - Event creator information
- `ClobReward` - CLOB reward data

## Development

This is a pure TypeScript declarations package. To contribute:

```bash
# Install dependencies
pnpm install

# Lint and format
pnpm run lint:fix

# Type check
pnpm run ts
```

## License

MIT © [Nivalis](https://github.com/nivalis-studio)

# Queries

E-commerce data utilities project providing TypeScript query functions for a SQLite database.

## Description

This project exposes a set of query modules over an e-commerce SQLite schema (customers, products, orders, inventory, promotions, reviews, shipping, and analytics). Schema definitions live in `src/schema.ts` and query modules in `src/queries/`.

## Getting Started

### Prerequisites

- Node.js 18+
- npm

### Setup

```bash
npm run setup
```

This installs dependencies and runs the project's init script.

### Configuration

Copy `.env.example` to `.env` and fill in the values:

```bash
cp .env.example .env
```

### Running

```bash
npm run sdk
```

## Project Structure

- `src/main.ts` — entry point
- `src/schema.ts` — database schema definitions
- `src/queries/` — query modules (customers, products, orders, analytics, inventory, promotions, reviews, shipping)
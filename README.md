# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.


# Supabase Database

## Database Schema 

## Users Table
- `id`: UUID (Primary Key, default gen_random_uuid())
- `username`: VARCHAR(50), UNIQUE, NOT NULL
- `email`: VARCHAR(255), UNIQUE, NOT NULL
- `password_hash`: VARCHAR(255), NOT NULL
- `first_name`: VARCHAR(100)
- `last_name`: VARCHAR(100)
- `created_at`: TIMESTAMP WITH TIME ZONE, DEFAULT NOW()

## Posts Table
- `id`: UUID (Primary Key, default gen_random_uuid())
- `author_id`: UUID, REFERENCES Users(id) ON DELETE CASCADE
- `title`: VARCHAR(255), NOT NULL
- `content`: TEXT, NOT NULL
- `created_at`: TIMESTAMP WITH TIME ZONE, DEFAULT NOW()

# Crucial Indexes for  performance
- Index foreign key lookups (e.g., user profile post list)
- `CREATE INDEX idx_posts_user_id ON posts (user_id);`

- Index timeline/feed ordering
- `CREATE INDEX idx_posts_created_at_desc ON posts (created_at DESC);`
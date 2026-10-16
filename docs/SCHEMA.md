# Database Schema

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

# Authentication RLS (For Agents (DO NOT ASSUME THIS AUTHENTICATION) ) Not Yet Enabled:
- Users can only update their own profiles.
- Posts are tied to users via user_id
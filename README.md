# Deno SQLite driver for Hono Sessions

## Usage
```ts
import { Hono } from "https://deno.land/x/hono/mod.ts";
import { Session, sessionMiddleware } from "https://deno.land/x/hono_sessions/mod.ts";
import { SqliteStore } from 'http://deno.land/x/hono_sessions_deno_sqlite_driver/mod.ts'
import { DB } from 'https://deno.land/x/sqlite/mod.ts'

const app = new Hono<{
  Variables: {
    session: Session,
    session_key_rotation: boolean
  }
}>()

const sqlite = new DB('./database.sqlite')

const store = new SqliteStore(sqlite, 'optional_custom_sessions_table_name') // Defaults to 'sessions'

app.use('*', sessionMiddleware({
  store
}))

// ...

Deno.serve(app.fetch)
```
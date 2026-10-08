# Smart Notes

A notes workspace for creating, organizing, and searching notes. Guest notes stay on the current device; signing in keeps notes private to that account and syncs them across devices.

**Live app:** [https://nakul-pishari-4205.github.io/smart-notes-app/](https://nakul-pishari-4205.github.io/smart-notes-app/)

Open `index.html` directly or visit the live app. Guest mode works locally without an account. Account sign-in and cloud sync require the one-time setup below.

## Set up account sync

1. Create a Supabase project.
2. In the Supabase SQL Editor, run all of [`supabase-schema.sql`](supabase-schema.sql). It creates the notes table, user-scoped row-level security policies, and the Realtime publication entry.
3. In Supabase **Authentication → URL Configuration**, set the Site URL to `https://nakul-pishari-4205.github.io/smart-notes-app/` and add that same URL (and any local development URLs you use) to the redirect allow list.
4. In **Authentication → Sign In / Providers**, enable Google, Azure (Microsoft), and Apple. Create OAuth apps with each provider and enter their client IDs/secrets in Supabase. Use the callback URL shown by Supabase in each provider's OAuth settings. Provider setup requires developer accounts with Google, Microsoft, and Apple.
5. Copy the Supabase project URL and its **publishable key** (or legacy `anon` key) from the Supabase project's API settings into `url` and `anonKey` in [`supabase-config.js`](supabase-config.js).
6. Publish the updated `supabase-config.js` with the website and sign in from the HTTPS live app.

The browser key is intentionally public. Do not put a Supabase `service_role` key or any OAuth client secret in this repository. Row-level security in `supabase-schema.sql` is what prevents users from reading or changing one another's notes. Local notes from guest mode are not automatically uploaded; after signing into a new, empty account, use **Import device notes** if you want to copy them into that account.

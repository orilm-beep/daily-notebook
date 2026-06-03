# Daily Notebook 📒

A clean, fast, installable daily to-do app with project tracking, cloud sync, and hourly inspiration.

- ✏️ Add your tasks each morning
- ✅ Tick them off with a satisfying check
- 📁 Tag tasks to a project — completed ones collect under that project
- ☁️ Optional cloud sync (Supabase) so your iPhone and laptop share one list
- 💬 A motivational quote that refreshes every hour
- 📱 Installable on iPhone/Android (Add to Home Screen) and works offline

## Use it
Open the published URL, then on iPhone: **Share → Add to Home Screen**.

## Turn on sync across devices (free)
1. Create a free project at [supabase.com](https://supabase.com) → **New project**.
2. In **SQL Editor**, run:

   ```sql
   create table if not exists tasks (
     id text primary key,
     text text,
     project text,
     done boolean default false,
     created_at timestamptz,
     completed_at timestamptz,
     updated_at timestamptz,
     deleted boolean default false
   );
   alter table tasks enable row level security;
   create policy "personal access" on tasks
     for all to anon using (true) with check (true);
   ```

3. In **Project Settings → API**, copy the **Project URL** and **anon public** key.
4. In the app, click **Connect sync** (top right) and paste both. Repeat on each device.

Your keys are stored only in each device's browser — they are **not** committed to this repo.

## Tech
Single static page — `index.html` (app), `sw.js` (offline), `manifest.webmanifest` (PWA), `icon-*.png`. No build step.

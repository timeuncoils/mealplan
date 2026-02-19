# Daily Meal Checklist

A beautiful dark-themed meal tracking app — hosted on GitHub Pages with Supabase as the database.

## Setup Guide

### Step 1: Create a Supabase Project

1. Go to [supabase.com](https://supabase.com) and create a free account
2. Click **New Project**, give it a name, set a database password, choose a region
3. Wait for the project to finish setting up (~2 minutes)

### Step 2: Run the Database Schema

1. In your Supabase dashboard, go to **SQL Editor** (left sidebar)
2. Click **New query**
3. Paste the entire contents of `supabase_schema.sql` into the editor
4. Click **Run** — this creates the tables, enables security policies, and inserts sample meal data
5. Verify: Go to **Table Editor** → you should see `meal_plans` (with 5 rows) and `meal_history` (empty)

### Step 3: Get Your API Credentials

1. In Supabase dashboard, go to **Settings** → **API**
2. Copy these two values:
   - **Project URL** — looks like `https://abcdefgh.supabase.co`
   - **anon / public key** — a long string starting with `eyJ...`

### Step 4: Update index.html

Open `index.html` and find these two lines near the top of the `<script>` block:

```js
const SUPABASE_URL  = 'https://YOUR_PROJECT_ID.supabase.co';
const SUPABASE_ANON = 'YOUR_ANON_KEY_HERE';
```

Replace them with your actual values from Step 3.

### Step 5: Push to GitHub & Enable Pages

1. Create a **public** GitHub repository (e.g., `meal-checklist`)
2. Push both files:
   ```bash
   git init
   git add index.html
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/meal-checklist.git
   git push -u origin main
   ```
3. Go to your repo **Settings** → **Pages**
4. Under "Source", select **Deploy from a branch**
5. Choose **main** branch, **/ (root)** folder, click **Save**
6. Your site will be live at `https://YOUR_USERNAME.github.io/meal-checklist/`

### Step 6: Customize Your Meal Plan

Edit the meal plan directly in Supabase **Table Editor** → `meal_plans`:

| name | time | items | sort_order |
|------|------|-------|------------|
| Breakfast | 8:00 AM | {Oats with banana, Black coffee, Boiled eggs} | 1 |
| Lunch | 1:00 PM | {Grilled chicken, Brown rice, Salad} | 2 |

- **items** is a Postgres text array — use `{item1, item2, item3}` format
- **sort_order** controls display order

---

## Security Note

The Supabase **anon key** is safe to expose in frontend code — it's designed for this. Row Level Security (RLS) policies in the schema ensure users can only **read** meal plans and **read/insert** history. They cannot delete or modify existing records through the anon key.

If you want additional security (e.g., per-user auth), you can enable Supabase Auth and update the RLS policies accordingly.

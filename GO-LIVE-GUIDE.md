# Banking2Day — Go Live Guide (Cloudflare Pages + GitHub + Supabase)

This takes your site from files → a real, live website with a working admin panel and database.
Total time: about **30–40 minutes**. No coding required — just following steps.

The site has **two parts that work together**:

| Part | What it is | Where it lives |
|------|------------|----------------|
| **Frontend + Admin** | All the pages + the admin screens (files) | **Cloudflare Pages** (free) |
| **Backend** | Database, logins, saved data | **Supabase** (free) |

You will do this in 3 stages:
1. **Supabase** — create the database (the backend)
2. **GitHub** — store the code online
3. **Cloudflare Pages** — publish the site to the world

---

## STAGE 1 — Supabase (the backend / database)  ~10 min

1. Go to **https://supabase.com** → **Start your project** → sign up (free).
2. Click **New project**. Give it a name (e.g. `banking2day`), set a strong **database password**
   (save it somewhere), pick a region near your users, click **Create new project**.
3. Wait ~2 minutes while it sets up.
4. In the left sidebar open **SQL Editor** → **New query**.
5. Open the file **`admin-cms/schema.sql`** from your project, copy **everything**, paste it into the
   query box, and click **Run** (bottom right). You should see **“Success”**. This builds every table
   (products, leads, subscribers, credit checks, settings…) and the security rules.
6. In the left sidebar open **Project Settings** (gear icon) → **API**. Copy these two values:
   - **Project URL** (looks like `https://abcxyz.supabase.co`)
   - **anon public** key (a long string)
7. Open the file **`admin-cms/b2d-cms.js`** in your project and paste them into the top two lines:
   ```js
   const SUPABASE_URL  = "https://abcxyz.supabase.co";   // ← your Project URL
   const SUPABASE_ANON = "eyJhbGciOi...";                // ← your anon public key
   ```
   Save the file.
8. Create your admin login: left sidebar **Authentication** → **Users** → **Add user** →
   enter your email + a password → **Create user** (tick “Auto Confirm” if shown).
   *This is the email/password you’ll use to log into the admin panel.*

✅ Backend is ready. (You can test now: open `admin-cms/admin.html`, sign in — it should load the dashboard.)

---

## STAGE 2 — GitHub (store the code online)  ~5 min

**Easiest way — let me do it for you:**
- In the chat composer, open the **Import menu** → click **Connect GitHub** → authorize.
- Send me a message. I’ll create a repository and push the whole `banking2day-site/` folder for you.
- Skip to Stage 3.

**Or do it yourself:**
1. Create a free account at **https://github.com** if you don’t have one.
2. Click **New repository** → name it `banking2day` → **Private** is fine → **Create repository**.
3. On your computer, download the `banking2day-site/` folder (use the download card I provide).
4. Upload it: on the new repo page click **uploading an existing file**, drag in everything inside
   `banking2day-site/`, then **Commit changes**.

✅ Code is on GitHub.

---

## STAGE 3 — Cloudflare Pages (publish to the world)  ~5 min

1. Sign up / log in at **https://dash.cloudflare.com**.
2. Left sidebar → **Workers & Pages** → **Create** → **Pages** tab → **Connect to Git**.
3. Authorize Cloudflare to see your GitHub, then **select the `banking2day` repo**.
4. On the setup screen:
   - **Project name:** `banking2day` (this becomes your URL)
   - **Production branch:** `main`
   - **Framework preset:** **None**
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
5. Click **Save and Deploy**. Wait ~1 minute.
6. You get a live URL like **`https://banking2day.pages.dev`**. That’s your site, live. 🎉
   - Public site: `https://banking2day.pages.dev/Banking2Day.dc.html`
   - Admin panel: `https://banking2day.pages.dev/admin-cms/admin.html`

> **Tip:** to make the landing page open at the bare URL (`banking2day.pages.dev` with no filename),
> ask me to add an `index.html` that redirects to `Banking2Day.dc.html` — I’ll drop it in before you deploy.

---

## STAGE 4 — Custom domain (optional)  ~5 min

1. Buy a domain (e.g. from Cloudflare Registrar, GoDaddy, Namecheap).
2. In Cloudflare Pages → your project → **Custom domains** → **Set up a domain** → enter `banking2day.com`.
3. Follow the DNS instructions it shows. Within a few minutes your site is on your own domain with free HTTPS.

---

## How updates work after launch

- **Content edits (products, rates, articles, leads, subscribers):** just log into the admin panel —
  changes save to Supabase instantly and show on the site. **No re-deploy needed.**
- **Design / page changes (by me):** I update the files → push to GitHub → Cloudflare auto-rebuilds
  in ~1 minute. Nothing for you to do.

---

## Checklist

- [ ] Supabase project created
- [ ] `schema.sql` run successfully
- [ ] 2 keys pasted into `b2d-cms.js`
- [ ] Admin user created in Supabase Auth
- [ ] Code pushed to GitHub
- [ ] Cloudflare Pages connected + deployed
- [ ] (optional) Custom domain added
- [ ] Tested: admin login works, a form submission appears in the admin

---

## Costs

Everything here runs on **free tiers** that comfortably cover a new site:
- Cloudflare Pages — free (unlimited static hosting + global CDN)
- Supabase — free tier (database, auth, API)
- GitHub — free
- A custom domain is the only paid part (~₹800–1,200/year), and it’s optional.

---

## Before the first deploy — small wiring I should finish

So the **live** site is fully connected (not demo mode), I still need to:
- Point the public forms (credit-score, loan apply, newsletter) at the Supabase save functions
  (`B2D.submitCreditCheck`, `B2D.submitLead`, `B2D.subscribe`) instead of the browser-only demo.
- Add the credit-score + subscribers views to the admin panel (data layer + table are already built).

Tell me **“finish the wiring”** and I’ll complete these, then we deploy.

# Ozair Kamran — Portfolio

## Your folder should look like this

```
/your-folder
  index.html          ← the portfolio (this file)
  pic01.jpg           ← your photo
  OzairKamranResume.pdf ← your resume
```

---

## Deploy on GitHub Pages (free hosting)

### Step 1 — Create the repo
1. Go to https://github.com and sign in
2. Click **New repository**
3. Name it exactly: `itsozair11.github.io`
4. Set it to **Public**, then click **Create repository**

### Step 2 — Upload your files
Option A (drag & drop — easiest):
1. Open the repo you just created
2. Click **Add file → Upload files**
3. Drag in: `index.html`, `pic01.jpg`, `OzairKamranResume.pdf`
4. Click **Commit changes**

Option B (via terminal):
```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/itsozair11/itsozair11.github.io.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages
1. In the repo, go to **Settings → Pages**
2. Under **Branch**, select `main` and click **Save**
3. Wait ~60 seconds, then visit: `https://itsozair11.github.io`

---

## Set up a custom domain (e.g. ozair.com)

### Step 1 — Buy your domain
Go to https://www.namecheap.com (or Squarespace Domains)
and purchase `ozair.com` or `ozairkamran.com` (~$10–15/year).

### Step 2 — Add DNS records
In your registrar's DNS settings, add these records:

| Type  | Host | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| CNAME | www  | itsozair11.github.io   |

### Step 3 — Add the domain in GitHub
1. In your repo → **Settings → Pages → Custom domain**
2. Type `ozair.com` and click **Save**
3. Check **Enforce HTTPS** (may take a few minutes to activate)
4. DNS propagation takes up to 24 hours — after that, `www.ozair.com` is live

---

## Making edits later
Just edit `index.html` in any text editor (VS Code recommended),
then re-upload the file to GitHub. The site updates within seconds.

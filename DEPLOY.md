Deploying this Next.js site (recommended: Vercel)

1) Push your code to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
# create a GitHub repo and add remote, then:
git remote add origin https://github.com/<your-username>/<repo>.git
git branch -M main
git push -u origin main
```

2) Import project to Vercel (recommended)
- Go to https://vercel.com/import and select the GitHub repo.
- Framework: Next.js will be auto-detected.
- Set Environment Variables in Vercel dashboard (Project Settings > Environment Variables):
  - `RESEND_API_KEY` (Secret, server-side)
  - `NEXT_PUBLIC_WS_URL` (Client-side)
  - `NEXT_PUBLIC_GA_ID` (Client-side)
  - `UMAMI_DOMAIN` (Client-side)
  - `UMAMI_SITE_ID` (Client-side)
- Deploy.

3) (Optional) Deploy from your machine with Vercel CLI
```bash
npm i -g vercel
vercel login
cd path/to/project
vercel  # follow prompts to link or create project
# add secrets (recommended):
vercel env add RESEND_API_KEY production
# then deploy:
vercel --prod
```

4) Netlify or other hosts
- You can also use Netlify, Render, or a Docker host. Vercel is recommended for full Next.js support.

Notes
- Do NOT commit real secret keys into the repo. Use Vercel's Environment Variables or `vercel env` to add them as secrets.
- If you want, I can try `vercel --prod` from this environment — you'll need to run `vercel login` interactively to authenticate.

CI / automatic deploy (recommended)
- A GitHub Actions workflow has been added at `.github/workflows/vercel-deploy.yml` to deploy on pushes to `main`.
- Steps you need to finish once:
  1. Push this repository to GitHub (see step 1 above).
  2. Create a Vercel personal token: https://vercel.com/account/tokens
  3. In the GitHub repo, go to Settings > Secrets and variables > Actions and add `VERCEL_TOKEN` (value = your Vercel token).
  4. Push to `main` — the workflow will run and call `vercel --prod` using the token.
- If the workflow fails during install, it now uses `npm ci --legacy-peer-deps` to match your local dependencies.

This lets CI handle the deploy so you don't need to sign in from this machine.

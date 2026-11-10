## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## Local development

Use Node.js 24 and the pnpm version declared in `package.json`. Copy `.env.example` to `.env.local` and configure `POSTGRES_URL` and `AUTH_SECRET`.

```sh
pnpm install --frozen-lockfile
pnpm dev
```

Run `pnpm lint`, `pnpm typecheck` and `pnpm build` before opening a pull request. Auth.js remains on the v5 beta because the application uses its server-side `auth`, `signIn` and `signOut` exports. TypeScript stays on the 6.0 line supported by typescript-eslint, and Node type definitions match the Node 24 runtime.

ESLint stays on the 9.x line supported by Next.js's import, React and accessibility plugins. Next.js and the Vercel CLI use the latest stable releases that satisfy the project's 48-hour minimum release age.

## CI and production deployment

GitHub Actions runs lint, type checking, build and an advisory React Doctor scan on pull requests to `main` and pushes to `main`. A successful push to `main` also deploys to Vercel.

In GitHub, open **Settings → Environments → production** and configure:

| Name | Where to add it | Value |
| --- | --- | --- |
| `VERCEL_TOKEN` | Environment secrets | Access token scoped to the project owner |
| `VERCEL_ORG_ID` | Environment variables or secrets | `orgId` from `.vercel/project.json` |
| `VERCEL_PROJECT_ID` | Environment variables or secrets | `projectId` from `.vercel/project.json` |

Run `pnpm exec vercel link` locally to link the existing project and obtain the IDs. If the link created `.vercel/repo.json`, use `orgId` and `id` from the matching entry in `projects` instead. In Vercel, keep `POSTGRES_URL` and `AUTH_SECRET` assigned to the **Production** environment. Configure the GitHub credentials before merging the workflow, since `vercel.json` turns off Git-triggered production deploys from `main`.

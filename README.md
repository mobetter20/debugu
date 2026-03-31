# debugu

Minimal static site for `debugu.xyz`.

## Files

- `index.html`: the site
- `README.md`: project notes and deployment steps
- `.gitignore`: ignores local macOS metadata

## Local preview

From this folder:

```bash
python3 -m http.server 8788
```

Then open `http://127.0.0.1:8788/`.

## Cloudflare Pages

Recommended: Git integration

1. Push this repo to GitHub.
2. In Cloudflare, go to `Workers & Pages`.
3. Select `Create application` > `Pages` > `Connect to Git`.
4. Choose the `debugu` GitHub repository.
5. Use these settings:
   - Framework preset: `None`
   - Build command: leave blank
   - Build output directory: `.`
   - Production branch: `main`
6. Select `Save and Deploy`.

Optional: Direct Upload with Wrangler

Cloudflare's current Pages Direct Upload docs say to create a project with `npx wrangler pages project create` and deploy with `npx wrangler pages deploy <BUILD_OUTPUT_DIRECTORY>`.

```bash
npm install --save-dev wrangler
npx wrangler login
npx wrangler pages project create
npx wrangler pages deploy .
```

## Custom domain: debugu.xyz

In Cloudflare Pages:

1. Open the `debugu` Pages project.
2. Go to `Custom domains`.
3. Select `Set up a domain`.
4. Enter `debugu.xyz`.

Important:

- For an apex domain like `debugu.xyz`, Cloudflare requires the domain to be added as a Cloudflare zone and its nameservers pointed at Cloudflare. Cloudflare then creates the needed DNS record for Pages.
- Do not add only a manual DNS record first. Cloudflare's docs warn that manually pointing a domain at `*.pages.dev` without first associating it in the Pages dashboard can fail and return `522`.

If you also want `www.debugu.xyz`, add it as a second custom domain after the apex is working.

## Sources

- Cloudflare Pages Direct Upload docs: https://developers.cloudflare.com/pages/get-started/direct-upload/
- Cloudflare Pages Git integration docs: https://developers.cloudflare.com/pages/get-started/git-integration/
- Cloudflare Pages custom domain docs: https://developers.cloudflare.com/pages/configuration/custom-domains/

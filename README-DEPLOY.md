# Cereastra on Cloudflare

This folder is ready to deploy the same way as ekgstudy.com: a GitHub repo that auto-deploys to a Cloudflare Worker serving static files.

## What is in it
- public/index.html is the whole app (10.2 MB, under Cloudflare's 25 MiB per-file limit).
- public/404.html is a small page-not-found page.
- public/robots.txt and public/sitemap.xml are for search engines.
- public/favicon.svg, apple-touch-icon.png, icon-512.png and site.webmanifest are the icons, made from your logo.
- public/og-image.png is the preview picture shown when the link is shared.
- public/_headers holds the security headers and caching rules.
- wrangler.jsonc holds the Worker settings (name "cereastra", serving ./public).

## Steps
1. Create a new GitHub repo, for example goldenburger/cereastra, and upload everything in this folder. Keep the public folder and wrangler.jsonc at the top level.
2. In the Cloudflare dashboard, go to Workers & Pages, choose Create, then Import a repository, and pick the repo. The build command can stay empty. The deploy command is `npx wrangler deploy`.
3. After the first deploy, open the Worker, go to Settings, then Domains & Routes, and add the custom domain cereastra.com. Add www.cereastra.com too.
4. Send www to the main address. In the cereastra.com zone, go to Rules, then Redirect Rules, and redirect www.cereastra.com/* to https://cereastra.com/${1} with a 301.
5. In SSL/TLS, set the mode to Full (strict) and turn on Always Use HTTPS.
6. In Google Search Console, add cereastra.com as a Domain property. Cloudflare can add the verification record for you. Then submit https://cereastra.com/sitemap.xml.
7. Share the link in a message to yourself to check the preview picture appears.

Every later update works like ekgstudy. Replace public/index.html in the repo and it redeploys.

## Before turning on AdSense
1. In AdSense, open Privacy & messaging and create the European regulations message and the U.S. state regulations message.
2. In index.html, change `const ADS_ENABLED=false;` to `true` and add the AdSense script tag AdSense gives you.
3. Add Google's ad domains to the Content-Security-Policy line in public/_headers, or the ads will be blocked. At minimum add https://pagead2.googlesyndication.com, https://*.googlesyndication.com, https://*.doubleclick.net, https://*.google.com and https://fundingchoicesmessages.google.com to script-src, img-src and connect-src, and add a frame-src with the same domains.
4. Have a lawyer review the atlas credits and sources file first.

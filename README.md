# BirdNote website

A minimal static Astro + Tailwind CSS site.

## Develop

```sh
npm ci
npm run dev
```

## Build

```sh
npm run build
npm run preview
```

Routes: `/` and `/privacy-policy` (also served as `/privacy-policy/`).

Deploy `dist/` to a static host. The privacy policy must be publicly accessible without login. This site uses no client JavaScript, external fonts, analytics, or tracking cookies.

The policy reflects the app’s current local preference stores and enabled Android system backups. Recheck it whenever app behavior changes.

## Deploy on a VPS

Install Node.js 22.12 or newer, then clone and build:

```sh
git clone https://github.com/dFuZer/birdnote-landing.git
cd birdnote-landing
npm ci
npm run build
```

Serve the generated `dist/` directory with Nginx or another static web server. No Node.js process is needed in production. For Nginx, adapt this server block to your domain and checkout path:

```nginx
server {
    listen 80;
    server_name your-domain.example;
    root /var/www/birdnote-landing/dist;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Keep the checkout in a location the web server can read, such as `/var/www/birdnote-landing`. Configure HTTPS for your domain before sharing the privacy policy URL. Both `/privacy-policy` and `/privacy-policy/` resolve through the generated directory index.

To update the site, run `git pull --ff-only`, `npm ci`, and `npm run build` in the checkout.

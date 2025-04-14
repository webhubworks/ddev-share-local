# ddev-share-local

Share vite projects locally using nip.io. This currently handles only CraftCMS and Laravel projects.

## Usage

```bash
ddev share-local
```

## Configure Vite
Bind Vite to all interfaces and set the correct origin when currently sharing:

```js
// vite.config.js

const url = new URL(process.env.SHARE_URL ?? process.env.DDEV_PRIMARY_URL)

export default defineConfig({
   // …
    server: {
        host: '0.0.0.0',
        port: 5173,
        strictPort: true,
        origin: `https://${url.host}:5173`,
        hmr: {
            protocol: "wss",
            host: url.host
        },
        cors: {
            origin: /^https?:\/\/(?:[a-zA-Z0-9-]+\.)+(ddev\.site|nip\.io)(?::\d+)?$/,
        },
        allowedHosts: ['.ddev.site', '.nip.io'],
    },
   // …
});
```

## Safari on iPhone
Out-of-the-box there will be CORS errors when opening the nip.io url on Safari on your iPhone. \
To solve this, `cd /etc/ssl/certs/` and `cat master.crt`. Copy its contents into a new e.g. `ddevmaster.crt` and airdrop it to your iPhone. In the iPhone's settings you will have to confirm and install this certificate (profile).

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
        origin: `${url.origin}:5173`,
        hmr: {
            protocol: "wss",
            host: url.host
        }
    },
   // …
});
```

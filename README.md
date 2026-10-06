# 30D Fit Challenge

A fitness habit tracker that turns a 30-day challenge into daily checklists, visible progress, and a simple points system.

Track exercise, meals, and walking or running from a mobile interface. The app runs entirely in the browser, stores progress on your device, and can be added to your home screen on supported browsers.

Built with HTML, CSS, and vanilla JavaScript. No build step, account, or backend is required. The current app interface is in Brazilian Portuguese.

## Features

- **Daily checklists:** a generated 30-day schedule with exercise routines, meal tasks, cardio bonuses, and walking or running entries.
- **Progress dashboard:** overall completion, completed exercise and meal counts, total distance, and a streak of completed days.
- **Calendar view:** see complete, partial, and upcoming days, then inspect each day's tasks.
- **Points system:** earn points for completed exercises, meals, recorded distance, and streak bonuses.
- **Challenge settings:** choose a start date and weekly distance target, or reset the challenge.
- **Local persistence:** save task completion and distance in the browser's `localStorage`.
- **Progressive Web App:** includes a web app manifest, home screen icons, an install prompt, and a service worker with a cache fallback.

## Run locally

You need Git and Python 3, or another static HTTP server.

```sh
git clone https://github.com/schulxf/30d-fit-challenge.git
cd 30d-fit-challenge
python -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000). If your Python installation uses the `python3` command, use `python3 -m http.server 8000` instead.

Serve the repository over HTTP rather than opening `index.html` directly: the manifest, icons, and service worker use paths relative to the site root. Service workers require HTTPS or a supported local development origin such as `localhost`.

## Using the app

1. Open **Config** and set the challenge start date and weekly walking or running target.
2. Use **Hoje** or **Tarefas** to check off daily activities and enter distance in kilometers.
3. Open **Calendário** or **Mês** to review progress across the challenge.
4. Open **Pontos** to see the score breakdown and streak bonuses.
5. Use the install banner or your browser's home screen option when available.

The settings default to today's date and a weekly distance target of 7 km. Future task checkboxes are disabled until their scheduled date.

## Data and offline behavior

Challenge state is stored under the `desafio30d_v3` key in `localStorage`. There is no account system, cloud backup, or synchronization between devices or browser profiles. Clearing site data removes saved progress.

The service worker caches the app shell during installation. Subsequent requests try the network first and fall back to cached resources when the network is unavailable. Visit the app online first to populate the cache. Home screen installation and offline behavior depend on browser support.

Fonts are loaded from Google Fonts; their availability offline depends on whether the browser or service worker has cached them.

## Project structure

| Path | Purpose |
| --- | --- |
| [`index.html`](index.html) | App layout, styles, challenge generation, state, scoring, and interactions |
| [`manifest.json`](manifest.json) | App metadata, standalone display settings, and icon definitions |
| [`sw.js`](sw.js) | App shell caching and network requests with a cache fallback |
| [`icons/`](icons/) | SVG app icons, including a maskable icon |
| [`vercel.json`](vercel.json) | Service worker caching and scope headers for Vercel |

## Deployment

Deploy the repository as a static site at the root of an HTTPS domain. No package installation or compilation is needed.

The included Vercel configuration sets `Cache-Control: no-cache` and `Service-Worker-Allowed: /` for `sw.js`. When deploying elsewhere, use equivalent response headers. Hosting under a subdirectory requires updating the root-relative URLs in the HTML, manifest, and service worker.

When changing cached app assets, update the `CACHE` version in `sw.js` so the service worker can replace the previous cache.

## Contributing

Open an [issue](https://github.com/schulxf/30d-fit-challenge/issues) to report a problem or discuss a feature, or submit a pull request with a focused change.

For interface changes, include screenshots and check the daily checklist, calendar, scoring, settings, and saved progress on a narrow mobile viewport. Changes to caching should also be checked after a fresh online visit and with the browser offline.

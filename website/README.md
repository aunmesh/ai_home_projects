# AI Home Projects

Small, opinionated AI projects for the house we actually live in.
Every project ships with the video, a demo, the diagram and the code.

Live site: https://aihomeprojects.netlify.app

## Repo layout

```
site/                 the website (deployed to Netlify)
experiments/          numbered, timeboxed tests — do these before building
chores-assistant/     project 01 — the code
  capture/            scheduled stills, per room
  detect/             object detection + clutter judgement
  notify/             task list out to phone / email
```

## How deploys work

`site/` is connected to Netlify. Push to `main` and the website updates
automatically. Netlify's package directory is set to `site`, so pushes that
only touch `chores-assistant/` do not trigger a website build.

Any branch other than `main` gets its own preview URL — use one when you
want to see a change before it goes live.

## Working on the site

No build step, no dependencies. Open `site/index.html` in a browser, or:

```bash
cd site && python3 -m http.server 8000
```

Then visit http://localhost:8000

## Project 01 — Home Chores Digital Assistant

A camera looks at each room on a schedule. A local model works out what is
out of place, scores the room, compares it against yesterday, and sends a
short task list.

Hard rule: frames are processed and deleted on the machine that captured
them. What persists is text. Notifications never carry images.

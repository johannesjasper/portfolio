# johannesjasper.de

Personal website — plain HTML and CSS, no build step.

## Structure

```
index.html       — the page
style.css        — all styles
public/
  profile.png    — profile photo
  favicons/      — favicon set
```

## Development

Open `index.html` directly in a browser. No server required.

For live-reload during editing, any static server works:

```bash
# Python (no install needed)
python3 -m http.server 4000
```

Then open http://localhost:4000.

## Deployment

Copy files to the web server:

```bash
rsync -av --delete \
  index.html style.css public/ \
  user@host:~/www/www.johannesjasper.de/
```

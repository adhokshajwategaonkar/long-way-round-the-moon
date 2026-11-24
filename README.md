# The Long Way Round the Moon

A walk through Pink Floyd's *The Dark Side of the Moon*: ten places, one for each song.

Live at https://adhokshajwategaonkar.github.io/long-way-round-the-moon/ . One static `index.html`, no build step, served by GitHub Pages from `main`.

## Sound

The album is not in this repo and must never be committed: it is still under copyright. The public site walks silently, and a visitor can add their own copy from "Add sound" (top right) or by dropping a file anywhere. Nothing is uploaded.

To walk with sound on your own machine, put your copy next to `index.html` as `album.ogg` (or `album.mp3` / `album.m4a`) and run:

```
python3 serve.py
```

then open http://localhost:8791 . The page finds the file and plays it from the first heartbeat. `.gitignore` keeps any audio file out of git. Use `serve.py` rather than `python3 -m http.server`, which cannot seek inside the file, so the music would drift away from the places.

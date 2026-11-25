---
name: album-walk
description: Use when the user wants to turn a music album into a scroll-driven 3D walk-through page (an album 'video' or homage) that plays their own audio file, one landscape per song.
---

# Album walk

Build a single web page that turns an album into a walk: the listener scrolls along one winding path through a landscape per song, drags to look around, and the music is cued so each song's key moment lands where they are standing. Publish it as a static site (GitHub Pages works) or a private artifact, or hand over the HTML file.

This skill records what worked, and what failed, over twelve rounds of feedback on a first project ("The Long Way Round the Moon", Pink Floyd's The Dark Side of the Moon). Follow the rules in section 6 from the start; each one was learned the hard way.

## Files in this skill

- `reference/long-way-round-the-moon.html`: the finished first project, one self-contained page with the whole engine (no audio inside). Read it before building and reuse its engine.
- `reference/session-notes.md`: the history of that project: every version, the feedback behind it, the final design, the cue timings and how it was tested.
- `reference/serve.py`: a tiny local server with HTTP range support, so the page can seek inside a local album file.

## 1. Ground rules

- **Never publish the recordings.** Keep audio out of the repo (`.gitignore` every audio extension). Locally, the page can find `album.ogg|mp3|m4a` next to it when served from localhost by `serve.py`; publicly it walks silently and a visitor can add their own copy (an "Add sound" button, or drop a file anywhere), played from a blob URL and remembered in IndexedDB. Do not make the opening screen ask for a file. If the user asks to host the album, decline briefly; YouTube embeds are not a fix (gaps between songs, ads, mobile autoplay blocks, no analyser). Offer a Spotify sign-in mode or a recorded walkthrough video instead.
- **No lyrics on screen**, not even a line. Build each world from what the song is about, in your own imagery.
- **Do not reproduce the album cover or other artwork.** Invent the visuals.
- **Anecdotes must be true.** Check each one with a web search before using it. Drop anything you cannot confirm.
- If the user points to a reference site, take the idea, not its text or layout.

## 2. What to get from the user

- The album, and the audio: one file for the whole album, or one per track. Check the file actually opens before planning around it.
- Anything that shows their taste (a portfolio, a past project). Use it for the on-screen type and colours.
- How they will view it (laptop, phone) and whether you can see their screen. If you cannot, say what you will not be able to check.

Start building after that. Ask only about choices that are expensive to redo, such as a straight versus winding route.

## 3. Research and writing

For each song gather: what it is about (in your words), two to four verified facts about how it was made, and its musical landmarks (intro, voice entry, solo, peak, ending).

Write as little as possible on screen. The opening screen gets the title, one visual line and the Begin button, nothing explaining the idea.

Write the story notes like this:
- One complete, plain sentence per note. Two to four notes per song.
- No highlighted keywords, no italic emphasis, no half-sentences, no dramatic fragments, no groups of three. That pattern reads as machine-written and the user will notice. The same goes for UI titles: never set a name in plain type with one word in a coloured italic.
- Say the concrete thing: names, dates, amounts.

## 4. Audio analysis

You cannot hear the file, so measure it.
- Convert to mono WAV with ffmpeg. Find track starts (silence detection, plus the published track lengths as a cross-check) and key moments (energy envelope, onsets, spectral changes).
- Record every time in seconds from the start of the user's file. Timings are specific to their copy.
- Per song keep about three cues: entry, the main moment (voice in, solo, peak), and at most one more. More cues than that makes the music jumpy.
- Tell the user plainly that timing has not been judged by ear, and ask them to report cues that land wrong.

## 5. Design one place per song

Make a table before coding. For each song: a place name, terrain shape, light and palette, a few line-drawn objects, one landmark the camera leans toward, something on the path to walk through (a doorway, a gate, a bank of cloud, a column of light), a title design, and a pointer shape.

- Every place needs its own identity. Repeating one treatment across all songs was rejected.
- Open on a calm, uncluttered hero view that is the first place itself: the camera looks at the opening landmark, the title sits over it in the same lettering as the first in-world title, and Begin turns the camera onto the path.
- Richness comes from texture, not more objects: moving film grain (an SVG noise layer shifted in steps), dust at several sizes including a few large soft out-of-focus motes, warm bulbs hung on long threads in one or two places, fog, and pencil hatching inside the line drawings (clip to the shape, jittered parallel lines, 25 to 45% alpha).
- HUD type: a mono for labels (IBM Plex Mono, small, tracked, uppercase, soft shadow, dim) and a grotesk for anything read (Archivo). Avoid a mono at 10px with no shadow over grain; it reads as sharp.
- Give each title its own design made from its place (lamps, engraving, handwriting, a notice board, neon). Use canvas effects so the design survives if a web font fails to load.

## 6. Experience rules (do not break these)

1. **Never stop or slow the walker.** No reading pauses, no "keep scrolling to skip", no full-screen title cards. If something needs more time, lengthen the path.
2. **Titles stand in the world** as fixed objects beside the path, at a fixed angle facing where they are read from, sitting on the ground. Not centred, not turning to face the camera (that reads as an overlay), never on the ground plane.
3. **Story notes are a plaque**, low on one side of the screen (bottom about 17%, inset about 7vw), on the side its group of notes belongs to, so plaques alternate left and right. Three parts: a small tracked mono label in the place's accent colour (`III · Footsteps`; IBM Plex Mono 500, 11px, 0.18em, uppercase), the notes as one paragraph in a clean grotesk (Archivo, 16px, weight 420, line height 1.65, soft text shadow), and a dim mono credit (`On the Run · The runway`). Max width about 370px. Scroll drives it: it fades and rises in as the group approaches, each sentence sharpens out of a blur as you reach it, and it fades up and out after. One plaque at a time; the old one fades before the next fills. On phones, centre it above the bottom scale. Keep an on/off control. Story failed as lines at screen centre, as text walls, as themed objects in the scenery, and as a lone caption.
4. **Music follows position.** Crossing a landmark pulls the song to its moment, unless the song is already within a few seconds of it.
5. **Play the run-up.** Put a quiet lead-in cue before each main landmark that starts the song early by (distance to landmark / current walking speed), clamped to about 4-24 seconds, so the moment arrives as the walker does.
6. **Returning resumes.** Each place remembers where its song was when the walker left, and picks up there.
7. **Keep the camera clear of the ground at any speed.** Target eye height is the larger of (ground under the feet + about 2.3) and (highest ground within about 12 units ahead and 4 to the side + about 1.9); also take the target at `s + velocity × 0.12` when moving fast. Smooth it asymmetrically: rise fast (rate 14), fall slowly (rate 5), and never let it sit more than 0.35 below the target. Symmetric smoothing put the camera 7 units inside a mountain at fast scroll. Test by replaying fast scrolling frame by frame through every place and reporting the lowest clearance.
8. **Nothing stands on the path** that the camera would pass through (beams, pillars, signs), unless walking through it is the point (a door, a gate, a cloud bank).
9. **Titles write themselves in.** Once a title comes out of the distance, reveal it left to right over about 2.4 seconds with a soft edge (a `uRev` uniform in the quad shader against the texture's x).
10. **Rewind is one fast unbroken take** back along the route (under four seconds), not a restart.
11. **Always show what is playing** and where in the song, with a bar the listener can seek.
12. **Controls:** volume, a journey scale along the bottom to jump between places with names on hover, and a pointer shape per place.

## 7. Build

One self-contained HTML file. Keep markup, styles and script in it.

Start from `reference/long-way-round-the-moon.html`. Keep its engine and replace the album-specific parts: the list of places (moves, cues, notes), the palettes and their order along the route, the terrain relief per place, the canvas drawings, the objects placed in each place, the title designs and the pointer shapes. In that file the script is laid out in this order: helpers, the places, the route, terrain, landmarks and light, shaders, drawings, objects and titles, then audio, input and the frame loop.

If the reference cannot be read, build these parts:

- **Rendering:** WebGL 1 written by hand works and needs no downloads. Programs: sky, terrain, ground scatter, textured quads, floating motes. A library from an allowed CDN is fine if you can test it.
- **Route:** each place is a list of moves (forward distance and rise, arc radius and angle, named anchors). Turn these into waypoints, then a smooth sampled curve. Give helpers for position, tangent, a point beside the path, and a fraction along a place. Plan roughly 350 units per song; check the route never passes close to itself.
- **Terrain:** a height grid built once at load from route heights plus a relief function per place; a camera-following mesh draws it. Level the ground under each title and along its sightline.
- **Objects:** draw them on canvas at load as line art and use them as alpha textures on quads. Sort far to near.
- **Light:** a palette per place (sky, horizon, ground, fog, accent, HUD colour). Finish each change of light before the next title becomes readable.
- **Text in the world:** draw to canvas, upload as a two-channel texture so one texture can carry two tints, add a soft blurred backing in the opposite tone. Build textures only when near and delete them when far. Redraw when web fonts finish loading.
- **Audio:** two audio elements on the same blob URL, crossfaded through Web Audio gain nodes, with an analyser for a bass pulse. One `arrive(from, to, force)` function owns every decision about jumping the song.
- **Input:** wheel and keys to walk, pointer drag to look, touch for both. Ease position toward a target.
- **Test handle:** expose a small object on `window` to teleport, walk at a set speed, read state and measure clearance.

Artifact constraints: load each web font family with its own link tag, so one bad request cannot break the rest. Wrap storage in try/catch. No alerts, no downloads. Images and media only from data or blob URLs.

Known traps:
- WebGL 1 mipmaps need power-of-two textures; otherwise text and drawings render as solid rectangles.
- A uniform declared in both shaders must have the same precision in each.
- A looping rule near the end of a song can fire just before the next place begins; give the last cue of a place a few seconds of slack.
- Additive (glowing) text washes out on a bright sky. Limit how far away it appears.
- Objects close to the path fill the screen as you pass. Keep them back or small.

## 8. Test

- Prefer a real browser with the real fonts and audio (for example the Claude desktop app's browser pane against `serve.py`). Otherwise run headless Chrome with software WebGL (`--use-gl=angle --use-angle=swiftshader --enable-unsafe-swiftshader`) through Playwright, and feed it the real audio file.
- For every place capture the title from far and near, each landmark, each walk-through element, and the caption. Lay the captures out as contact sheets and look at them before publishing.
- Walk each place at a steady speed and log where the music is at every cue.
- Check there are no page errors, that rewind and far jumps work, and the clearance numbers.
- Say what you could not verify: timing by ear, real fonts if the test browser is offline, frame rate on the user's machine, touch, the live pointer.

## 9. Publish and iterate

- Publish as a static site (GitHub Pages from `main`, with `.nojekyll`) or a private artifact, and update the same one for each revision.
- Keep the session notes and this skill in the project (`docs/`, `skill/`) and update both after every round, then rebuild the skill zip.
- Keep a copy of every version's source before a large change; the user may ask for an earlier treatment back.
- Expect several rounds. After each one, lead with what changed, then list what you could not check and one or two things you want their eye on. Keep replies short.
- When feedback contradicts an earlier round, the newest message wins, but keep the rules in section 6 unless the user explicitly overturns one.

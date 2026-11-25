# The Long Way Round the Moon: session notes

A record of how this project was made, what was decided and why, and what state it is in now.
Started 25 November 2026. Updated after every round of changes; the newest round is at the end of section 3.

## 1. What it is

A single web page that turns Pink Floyd's *The Dark Side of the Moon* into a walk.
You scroll to move along one winding path through ten landscapes, one per song. Dragging looks around in 360°.
The album plays from your own file, and the music is cued so that each song's key moment lands where you are standing.

- **Where it lives now:** a public GitHub repo, github.com/adhokshajwategaonkar/long-way-round-the-moon, served by GitHub Pages at https://adhokshajwategaonkar.github.io/long-way-round-the-moon/ . On Adho's Mac the folder is `Documents/Documents - Ankit’s MacBook Air/long-way-round-the-moon`.
- **Where it started:** a private Claude artifact (https://claude.ai/artifact/CpSw4Dxd8Kx2whCNpiYQiD), versions v1 to v9. That artifact is no longer the current copy.
- **These notes and the album-walk skill** live in the repo under `docs/` and `skill/`, and are refreshed after every round.
- **Who it is for:** a personal homage by Adho, shown on his portfolio.
- **Starting point:** the reference was "East Is Up" (https://vrarora.vercel.app/labs/east-is-up/), a scroll-driven walking museum of Twenty One Pilots lore. The first session could not open it and worked from screen recordings. In v12 it was opened and studied directly (see section 3).

## 2. Fixed rules (these held through every version)

- **The album is never published.** It is not in the repo (`.gitignore` blocks audio files). On the public site the walk is silent unless a visitor adds their own copy ("Add sound" or drop a file). On Adho's Mac, `album.ogg` sits next to `index.html` and plays automatically when served by `serve.py` on localhost. Adho asked several times to publish the file; it was declined each time (it is the full commercial album, and the archive.org copy has no licence). The YouTube embed route was examined and rejected (gaps between songs, ads, mobile autoplay limits, no audio analysis). A Spotify sign-in mode and a recorded walkthrough video were offered as alternatives.
- **No lyrics on screen.** Each world is built from what its song is about, but no lyric text is shown.
- **No album cover artwork.** The prism image is not reproduced anywhere.
- **Do not copy the reference's text or layout.** Use it for the idea only.
- **Working conditions:** v1 to v9 were made from the Claude phone app with an offline, software-rendered test browser. From v10 the work is done in Claude Code on Adho's Mac, with a real browser, real fonts and the real audio file.

## 3. How it got here, version by version

Each round below is Adho's feedback followed by what changed.

### v1: first build
- **Asked for:** scroll to walk, drag to look around at any time while the music keeps going; use his one Ogg file of the album.
- **Built:** ten "rooms" on a straight path, hand-written WebGL (no library, because nothing could be downloaded in the workspace), two audio elements crossfading, a bass pulse driving the visuals.

### v2: a winding route and a story
- **Feedback:** crossfades are fine, but songs must start at their high point when you arrive. The straight path is bland. Build each place from what its song is about. Add a real anecdote for each song. Remove clutter.
- **Changed:** the route became one winding line with climbs and turns. Each place got its own terrain. Verified anecdotes were added in a side panel. The album was analysed to find where each moment falls in the file.

### v3: character, controls, and resuming
- **Feedback:** high points still not synced. More variety in the land. The side panel does not work. Finish the remaining places. Coming back to a place should resume its song where you left it. Add a volume slider, a timeline to jump between places with names on hover, colour and glow per mood, and a camera that tilts toward landmarks.
- **Changed:** all ten places finished; per-place song memory; volume; the journey scale along the bottom; palettes and lighting per place; camera lean toward landmarks. Text was tried on the ground and in a different decorative font per place.

### v4: richer visuals, reading pauses
- **Feedback:** "Walk me back" restarted the journey when it should rewind along the route. Text was illegible and badly placed; never put text on the ground. Story lines scrolled past before the matching music arrived. The opening was cluttered. Visuals were dry. Show which song is playing and where you are in it. The entry into Time was abrupt.
- **Changed:** a calm opening (an eclipse over still water). Richer terrain shading, ground scatter, water, clouds. A song display with a seekable bar. One clean type system drawn from Adho's own portfolio (Geist, Geist Mono, Instrument Serif, one orange accent). Story shown as a column of lines while the walk paused ("stay a moment"), with a full-screen title card for each song.
- **Verdict:** "visuals look pretty", but the pauses and title cards broke the experience.

### v5: nothing stops the walk
- **Feedback:** the user must never have to stop scrolling. Titles and story must be part of the environment you pass, not separate screens. Rewind must be much faster. Take us through some elements. Change the pointer per place.
- **Changed:** holds and title cards removed. The route was lengthened by about 40% to give reading room. Titles and story lines became camera-facing type standing in the path. Music cues gained a "lead-in" so the run-up plays while you approach. Rewind cut to under four seconds. The house, three doors, light columns and cloud banks were put on the path. Ten pointer shapes.
- **Verdict:** lines arriving one by one at the centre "really looks bad"; camera-facing titles felt like an overlay.

### v6: walls of text beside the path
- **Feedback:** bring back v4's story format and positioning, without pausing. Titles and all text should be in the environment, not on screen.
- **Changed:** each anecdote became a block (label, hairline, lines appearing as you approach) standing at the side of the path at a fixed angle. Titles became letters standing on the ground. The terrain is levelled under each one so it does not sink into a slope. Reflections on the opening water.
- **Verdict:** "great".

### v7: a design for each place, plainer writing
- **Feedback:** story text too big, keep it off-centre. Every title should be designed for its own place, not one repeated font. The writing style (a plain half-sentence with a few italic keywords) reads like a language model wrote it.
- **Changed:** ten title designs (see section 5). Ten themed story objects (receipts, runway boards, stones, signs and so on). All anecdotes rewritten as plain single sentences with no highlighted words.
- **Verdict:** the themed story objects were still too big and distracting, and did not blend with the scenery.

### v8: story as an optional caption; higher camera
- **Feedback:** find a subtle way to show the story on screen so the viewer can read it if they want and otherwise enjoy the road. No need to theme it. Separately: the camera rides too close to the ground, especially on the Great Gig slope.
- **Changed:** story objects removed from the world. One small caption in the bottom-left corner, with a "Notes on/off" control. The camera now keeps a set clearance above any ground nearby or just ahead; I measured every place before and after.
- **Verdict:** caption too far out of view and barely visible.

### v9: current
- **Feedback:** keep or increase the size, and bring the text to centre-left where it can be read without leaving the main scene.
- **Changed:** the caption now sits left of centre, just under the horizon, at 17–21px with a soft shade behind it.

### v10: a live site, a new opening (Claude Code, 25 Nov)
- **Asked for:** make it live with its own GitHub repo. Stop asking visitors to drop the album. Redesign the opening screen, which was a serif headline on the left and a "drop the album" circle on the right.
- **Changed:** published to GitHub Pages. The opening became the walk's first place: the eclipse over the water, the title in thin lowercase like the first title in the land, a heartbeat line, one Begin button and the ten places along the bottom. The album plays automatically on localhost via `serve.py`, which adds HTTP range support so the music can seek (Python's own server cannot, and the music drifted away from the places).

### v11: less copy, one typeface, camera and beams
- **Feedback:** write less ("no need for ten places, one for each song", no "each song is a landscape"). The HUD fonts look sharp. Plain words with one orange italic keyword reads like a language model. Going fast up or down a mountain puts the camera inside it. In Any Colour You Like the camera goes through the beams.
- **Changed:** the gate is title, heartbeat, Begin. HUD in one typeface, no italic keywords. Eye height now rises fast and falls slowly, looks ahead by speed, and never sits more than 0.35 below its target; measured at fast scroll speeds it went from up to 7 units underground to at least 1.76 above. The colour beams moved to alternate sides of the path, at least 4.9 units clear.

### v12: the reference's text and richness
- **Feedback:** the text in the reference looks and appears beautifully, and its visuals feel richer. Compare and improve.
- **What the reference does** (studied live in the browser): story sits in a plaque low on one side, alternating left and right: a small tracked mono label in the accent colour (IBM Plex Mono 500, 11px, 0.18em), a clean grotesk body (Archivo, 15 to 16px, weight 420, line height 1.6, soft shadow), and sometimes a dim mono credit line. Plaques fade and rise by scroll, not by timer. Titles are huge tracked capitals that write in letter by letter. The scene has moving film grain, fog, warm bulbs on long threads, lots of drifting dust, and pencil-hatched drawings.
- **Changed:** story notes became plaques: one per group of notes, on the side the group belongs to, label `I · The voices`, sentences that sharpen from a blur one by one as you reach them, credit `Speak to Me · The far side`. Labels in IBM Plex Mono, reading text in Archivo (the HUD too). Every in-world title now writes itself in from left to right once it comes out of the distance. Film grain now moves. Dust doubled, with some large soft out-of-focus motes. Warm bulbs on threads over the first water and along the causeway. Pencil hatching inside the house, doors, shed, towers, signs and arch.
- **What went wrong before:** v1 to v9 never saw the reference running, never saw real fonts, and treated "story" as a caption problem. The reference's answer is typographic: a tight three-part plaque with a mono label, set low and to the side, revealed by scroll.

## 4. What the feedback taught (design rules that came out of this)

1. **Never stop or slow the walker.** No holds, no interstitial screens. If text needs more time, lengthen the path.
2. **Music follows position.** Each place has a few landmarks tied to moments in the song. Arriving pulls the song to that moment unless it is already close.
3. **Give the run-up, not just the peak.** A quiet cue before each landmark starts the song a few seconds early, judged by walking speed, so the moment arrives as you do.
4. **Returning resumes.** Each place remembers where its song was when you left.
5. **Titles belong in the world; story belongs near the eye.** Titles work as designed objects standing beside the path, and write themselves in as they come into view. Story text failed as centred lines, as big walls, as themed objects and as a lone caption. It works as a plaque low on one side (mono label, grotesk body, mono credit), revealed by scroll, sentence by sentence, with an off switch.
6. **No text on the ground**, and no text that turns to face the camera (it reads as an overlay).
7. **Write plainly.** One complete sentence per note. No keyword emphasis, no dramatic fragments.
8. **Each place gets its own identity**: terrain, light, objects, title design, pointer.
9. **Keep the camera clear of the ground** on slopes.
10. **Rewind is a fast unbroken take**, not a restart.
11. **Write less.** No explanatory copy on the opening screen. No keyword emphasis anywhere.
12. **Nothing stands on the path that the camera would pass through**, except things meant to be walked through (doors, gates, cloud).
13. **Texture makes it rich:** moving grain, dust at several sizes, warm points of light, hatching in drawings.

## 5. The current design

### The ten places

| # | Song | Place | What you see | Title design |
|---|---|---|---|---|
| I | Speak to Me | The far side | still water, an eclipse in reverse | thin lowercase with a heartbeat trace, mirrored in the water |
| II | Breathe | First morning | meadow, a hare, rabbit holes, birds | handwritten, with a pencil stroke |
| III | On the Run | The runway | chasing lamps, control tower, a fireball you walk into | amber runway lamps |
| IV | Time | The sundial | ticking clocks, a huge dial with a moving shadow, a lit house you walk through | cut capitals under dial ticks |
| V | The Great Gig in the Sky | The summit | a climb through cloud banks to an arch, rising lights | light italics hanging in the air |
| VI | Money | The gold cut | terraces, coins, a coin gate | fat gold capitals with engraving lines |
| VII | Us and Them | The causeway | a raised path between a blue side and a red side | "US" in blue on the left, "THEM" in red on the right |
| VIII | Any Colour You Like | The dunes | columns of coloured light that turn blue as you reach them | neon that cycles colour, then turns blue |
| IX | Brain Damage | The lawn | park signs, a seated figure, a rising moon, three doors in the path | typed on a crooked notice board |
| X | Eclipse | The hill | a procession of earlier objects, the moon crossing the sun | dark capitals with light round the edges |

### On-screen controls
- **Opening screen:** the eclipse over the water, the title, a heartbeat line, Begin, and the ten places along the bottom (click one to start there).
- **Top left:** the song now playing (Archivo), with a bar you can drag to seek, and a mono label and time.
- **Top right:** volume (or "Add sound" when there is no album), and "Notes on/off".
- **Low on the left or right:** the story plaque.
- **Bottom:** the journey scale. Click a place to go there; hover for its name.
- **End of the route:** "Walk me back" rewinds the whole route in under four seconds.

### The story notes (current wording)

- **Speak to Me:** The album came out on 1 March 1973. / It stayed on the American chart for 741 weeks. That is about fourteen years. / It has sold more than 45 million copies. / The first thing you hear on it is a heartbeat.
- **Breathe:** Rick Wright played jazz before he played in this band. / There is a chord in this song that he took from Miles Davis. / He heard it on Kind of Blue and worked it out at home.
- **On the Run:** On stage in 1972 this was a guitar jam called The Travel Sequence. / In the studio they fed eight notes into a synthesiser and sped them up. / The running feet are Peter James, the assistant engineer, doing laps of the studio.
- **Time:** Alan Parsons recorded each of these clocks by itself in an antique shop. / He made the tape to show off a new sound system, not for the band. / He mentioned it during the sessions and they used it.
- **The Great Gig in the Sky:** Clare Torry was a session singer, booked for a Sunday evening. / They told her there were no words. / She was paid thirty pounds and went home thinking they would not use it. / In 2005 her name was added to the writing credit.
- **Money:** Roger Waters made the opening loop in his garden shed. / He threw coins into a bowl his wife used for mixing clay, and tore up paper. / The loop is seven pieces of tape joined end to end. / The song counts in seven until the guitar solo, which is in four.
- **Us and Them:** Rick Wright wrote this in 1969 for the film Zabriskie Point. / Back then it was called The Violent Sequence. / The director said it was beautiful but too sad, and left it out.
- **Any Colour You Like:** The title comes from Chris Adamson, one of the road crew. / Ask him for a guitar and he would say: any colour you like, they are all blue. / Roger Waters heard it as being offered a choice when there is none.
- **Brain Damage:** This one is about Syd Barrett, who started the band and had to leave it. / The lawn is real. It is behind King's College in Cambridge. / There is a sign on it telling you to keep off the grass.
- **Eclipse:** The band wrote questions on cards and asked whoever was around the studio. / Gerry O'Driscoll, the doorman, got the one about the dark side of the moon. / He said there was no dark side. It is all dark.

These facts were checked by web search earlier in the session; the source links are not reproduced here.

## 6. How it is built

One self-contained HTML page, about 126 KB. No libraries.

- **Rendering:** hand-written WebGL 1. Five shader programs: sky (gradient, sun, stars, clouds), terrain (faceted shading, contour lines, water, fog), ground scatter (pebbles, grass, flowers), textured quads (every drawn object and title), and floating motes.
- **Route:** each place is a list of moves (forward, arc, named anchor). These become waypoints, then a smooth sampled curve about 3,730 units long.
- **Terrain:** a height grid built once at load from the route's heights plus a relief function per place, then levelled under each title. A camera-following mesh draws it.
- **Objects:** line drawings made on canvas at load and used as textures, placed along the route by distance and side.
- **Titles:** drawn to canvas with a two-channel mask (so one texture can carry two colours), stood beside the path facing where you read them from, built only when near and released when far.
- **Light:** a palette per place (sky, ground, fog, accent, HUD colour), blended along the route so each place has its own light by the time its title is readable.
- **Camera:** follows the route, leans part-way toward landmarks and titles, and keeps a clearance above nearby ground.
- **Audio:** two audio elements crossfaded through Web Audio gains; an analyser gives a bass pulse and a level. On localhost the page looks for `album.ogg`, `album.mp3` or `album.m4a` next to it; otherwise a visitor's own file is stored in IndexedDB.
- **Type:** IBM Plex Mono for labels, Archivo for reading text, Jost for the opening title. In-world titles keep their own per-place designs.
- **Serving:** `serve.py` (Python, adds range requests) on port 8791 locally; GitHub Pages publicly.
- **Cues:** a sorted list of landmarks, each with a position and a time in the file. Crossing one calls a single `arrive` function that decides whether to resume, jump, or leave the song alone.

### Timings in Adho's file (seconds)

Song starts: 0, 70, 241, 466, 874, 1153, 1538, 2005, 2213, 2440; the file ends at 2545 with the tail cut.

Key moments used as cues: heartbeat 3 · voices 32 · scream into first chord 66.5–69 · Breathe voice 144.5, second verse 194 · On the Run sequence 286, crash 411.5 · ticking 432, alarms 468, Time verse 599, reprise 825 · Gig piano 875, voice 939.5, peak 990, hush 1024 · till 1153, riff 1165.5, guitar solo 1340 · Us and Them organ 1540, voice 1630, first chorus 1687 · Any Colour swirl 2038, guitar 2087 · Brain Damage voice 2226, chorus 2284 · Eclipse 2442, peak 2500, final heartbeat 2526.

These are specific to this rip; another copy of the album will differ by a second or more.

### Source layout (in the cloud workspace used for this session)

`moonwalk/src/head.html` (markup and CSS), `a_places.js` (the ten places, cues, notes), `b_light.js` (landmarks, palettes, sky), `c_shaders.js`, `d_world.js` (objects, titles, pointers), `e_run.js` (audio, input, frame loop), and `build.py`, which stitches them with engine blocks from an earlier build into `index.html`.

That workspace is temporary. The published artifact is the durable copy: its HTML contains the whole program.

## 7. How it was tested

- v10 onward: the Claude desktop app's browser pane against `serve.py` on localhost, with the real fonts and the real album, plus the live Pages URL after each push.
- A camera test that replays fast scrolling frame by frame through every place and reports the lowest clearance (v11: at least 1.76 units).
- v1 to v9: headless Chrome with software WebGL, driven by Playwright, fed the real album file.
- A test handle (`window.__lw`) to jump along the route, walk at a set speed, read state, and measure ground clearance.
- Contact sheets of screenshots for every place, viewed after each change.

**Still not verified from my side:** how the timing sounds by ear, frame rate on Adho's own laptop, and touch gestures on a real phone.

## 8. Open items

- Each place makes four or five music jumps, because the walk is far shorter than the songs. Not yet judged by ear.
- Sound for public visitors: undecided between a Spotify sign-in mode and a recorded walkthrough video.
- In The Great Gig in the Sky, light text has the weakest contrast against the pink hills.
- Phone portrait layout received only a quick check.

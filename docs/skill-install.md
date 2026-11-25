# Installing the album-walk skill on another account

You have one file to carry over: `album-walk.zip`. Do not unzip it.

## What is inside

```
album-walk/
  SKILL.md                                  the instructions Claude follows
  reference/long-way-round-the-moon.html    the finished Dark Side of the Moon page, with the whole engine
  reference/session-notes.md                how that project was made, version by version
  reference/serve.py                        a local server that lets the page seek inside a local album file
```

The zip contains no music. Each copy of the page plays an album file that stays on the computer that opens it.

## Add it as a skill

These steps are from Anthropic's help pages ("Use skills in Claude" and "How to create custom skills"); the labels may change over time.

1. Sign in to Claude with the other account, on the web or in the desktop app.
2. Go to **Customize > Skills**.
3. Click the **+** button, then **+ Create skill**.
4. Choose **Upload a skill** and pick `album-walk.zip`.
5. The skill appears in the skills list. Make sure it is switched on.

On a Team or Enterprise plan, skills and code execution have to be allowed by the organization's owner first (Organization settings > Plugins & skills).

Help pages:
- https://support.claude.com/en/articles/12512180-use-skills-in-claude
- https://support.claude.com/en/articles/12512198-how-to-create-custom-skills

## If the upload does not work

Attach `album-walk.zip` to a new chat on that account and say:

> Create a skill from this zip. Keep the reference files.

## Using it

Start a chat and say something like:

> Use the album-walk skill to make a walk-through for [album]. I will upload the audio.

Then attach the album file when asked.

## Where the current version lives

The live page is public at https://adhokshajwategaonkar.github.io/long-way-round-the-moon/ and its source is at github.com/adhokshajwategaonkar/long-way-round-the-moon . The skill source and these notes are in that repo under `skill/` and `docs/`; the zip is rebuilt from `skill/` after every round of changes. The old Claude artifact link is private to the first account and out of date.

# How to build this game for another class

This is the recipe behind Vital Strike. Use it to make the same game for a different course.

## What the game is

- One HTML file. No install and no server.
- A student answers a question. A right answer earns a shot at the hidden enemy fleet. A hit earns another shot. A wrong answer lets the enemy fire back.
- Sink all four enemy ships to win.
- Questions come from a card bank file that sits next to the game.

## Files in the folder

| File | What it does | Change for a new class? |
|---|---|---|
| anatomy-armada.html | The game | Yes, a few lines (below) |
| index.html | A copy of the game so the folder address opens it | Copy of the file above |
| your-card-bank.js | The questions | Yes, this is the main work |
| vital-strike-theme.mp3 | Theme music | Optional |
| anatomy-armada-share.jpg | Picture shown when the link is shared | Optional |
| compliance-notes.md | Accessibility notes | Update the name and date |

## Step 1. Make the card bank

The game reads a card bank in the same format as the Mastery OS banks. One file, one global name.

```js
window.MYCOURSE_CARD_BANK = {
  modules: [
    { topics: [
      { id: "m1-cells", title: "Cells",
        cards: [
          { dok: 1,
            q: "Question text",
            options: ["Choice A", "Choice B", "Choice C", "Choice D"],
            correctIndex: 0,
            why: "Why the right answer is right",
            notes: ["Why A", "Why B is wrong", "Why C is wrong", "Why D is wrong"]
          }
        ] }
    ] }
  ]
};
```

- dok 1 cards become the Easy level. dok 2 and 3 cards become the Advanced level.
- notes is optional. If a card has only one explanation, use explanation in place of why and notes.
- A topic needs at least a handful of cards at a level before a game on that level is worth playing.

## Step 2. Point the game at the bank

Open the game file and search for each of these.

1. `const SUBJECTS=` : one entry per card bank. Set the name students see, the global name from Step 1, and the file name in urls. Remove the entry you do not need.
2. The two checkboxes with ids `sb_anatomy` and `sb_physiology` : change the labels to match SUBJECTS, or remove one.
3. `const GROUPS=` : the list in the Topic menu. Each group has a name and the topic ids that belong to it. Any topic id not listed lands in "More topics", so the game still works if you skip this.
4. `const BANK=` : the built-in starter questions (neuro). Replace them with a short set for the new course, or remove them and the "Starter sets" group.

## Step 3. Change the words and the look

Search for each of these.

- `<title>` and the `h1` : the game name.
- `eyebrow` : the line above the name ("Anatomy and Physiology Review").
- `const STORY=` : the five opening lines. Each line has three parts. The middle part is the word shown in red.
- `og:title`, `og:description`, `og:url`, `og:image` : what shows when the link is shared.
- `var ID="vital-strike"` : the name used by the Kajabi iframe for resizing. Use a new name per game.
- `THEME_FILE` : the music file name. `THEME_CREDIT` : the credit line if the track needs one.
- `.heroimg` : the banner photo.
- Colors are at the top of the style block: `--ink`, `--gold`, `--maroon`.

## Step 4. Put it online

1. Make a new GitHub repo for the game and upload the folder.
2. Turn on GitHub Pages (Settings, Pages, deploy from the main branch).
3. The address is `https://USERNAME.github.io/REPO/`.
4. For Kajabi, use the same iframe code as Vital Strike with the new address and the new ID.

## Check before sharing

- Open the page, check a subject, open Topic and confirm the topics load.
- Play one game at each level.
- Play one game on a phone.
- Read every new question. A wrong answer key teaches the wrong thing.

## To have Claude build it

Give Claude the Vital Strike HTML file and the new card bank (or the repo that holds it), then say:

"Make a copy of this game for [course]. Use [card bank file] for the questions. Name it [name]. Group the topics as [list, or 'by module']. Rewrite the opening story for [course]. Keep everything else the same."

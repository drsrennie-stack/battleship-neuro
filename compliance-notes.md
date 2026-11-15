# Accessibility Compliance Notes

## 1. Project

- Project: Vital Strike (anatomy and physiology review game)
- Files covered: anatomy-armada.html (the game), anatomy-armada-share.jpg (link preview picture)
- Date: November 15, 2026 (updated for the popup layout, dropdown menus, warm maroon buttons, question levels and the course card bank)

## 2. WCAG version and level

Target: WCAG 2.2 AA, with AAA contrast where achievable.

| Criterion | Level | Status | How it is met |
|---|---|---|---|
| 1.1.1 Non-text content | A | Met | Every grid square has a text label (for example "C4, hit"). Decorative effects are hidden from assistive technology. |
| 1.3.1 Info and relationships | A | Met | Landmarks, heading order, a labeled group for the Anatomy and Physiology checkboxes, a labeled group for the topic checkboxes, and a definition list for the scoreboard. |
| 1.4.1 Use of color | A | Met | Hits show an X, misses show a ring, and answer feedback uses text tags, so nothing depends on color alone. |
| 1.4.3 / 1.4.6 Contrast | AA / AAA | Met with one exception | See the audit in section 3. The warm maroon title word and step numerals are an approved brand exception. |
| 1.4.10 Reflow | AA | Met | Single column layout at 390 px wide with no horizontal scrolling. |
| 1.4.11 Non-text contrast | AA | Met | Controls, ship shapes and focus rings are 3:1 or higher. |
| 2.1.1 Keyboard | A | Met | Every control works from the keyboard. The enemy grid uses arrow keys to move and Enter or Space to fire. |
| 2.2.1 Timing adjustable | A | Met | There is no timer on any question or turn. |
| 2.3.1 Three flashes | A | Met | Explosions are a single burst and do not flash repeatedly. |
| 2.3.3 Animation from interactions | AAA | Met | All motion is removed when the reader has "reduce motion" turned on. |
| 2.4.1 Bypass blocks | A | Met | Skip link to the game. |
| 2.4.3 Focus order | A | Met | The game runs in a native modal dialog. Focus moves to the new question, the feedback, or the grid as each phase begins, and returns to Start game when the dialog closes. |
| 2.4.7 / 2.4.11 Focus visible | AA | Met | 3 px focus ring on every control. |
| 2.5.8 Target size | AA | Met | Grid squares are about 44 px at phone width and larger on desktop. All buttons are well above the 24 px minimum. |
| 3.3.2 Labels or instructions | A | Met | The checkboxes and buttons have visible labels. The Topic and Level menus show their names as the starting text and keep an accessible name after a choice is made. |
| 4.1.2 Name, role, value | A | Met | Sound toggle uses aria-pressed. Grid squares report whether they can be fired on. |
| 4.1.3 Status messages | AA | Met | Hits, misses, sunk ships and results are announced through a polite live region. |

## 3. Color contrast audit

| Text or element | Foreground | Background | Ratio |
|---|---|---|---|
| White body text on page | #FFFFFF | #060B1A | 19.6:1 |
| Soft text on page | #D5DAE6 | #060B1A | 14.0:1 |
| Gold eyebrow on page | #E0B861 | #060B1A | 10.5:1 |
| Warm maroon headline word "Strike" and 01 to 04 numerals (large, decorative) | #8A3324 | #060B1A | 2.4:1, does not pass |
| Red result numbers on end screen (large) | #EE7A8B | #060B1A | 7.3:1 |
| Navy text on gold Topics and Level menus | #060B1A | #E0B861 | 10.5:1 |
| Navy text on white Topics list | #060B1A | #FFFFFF | 19.6:1 |
| Red X hit marker on water (non-text) | #FF3B52 | #16306A | 3.6:1 |
| White text on warm maroon buttons | #FFFFFF | #8A3324 | 8.1:1 |
| Card body text on white | #1E3D4C | #FFFFFF | 11.5:1 |
| Card heading on white | #060B1A | #FFFFFF | 19.6:1 |
| Warm maroon eyebrow on white | #8A3324 | #FFFFFF | 8.1:1 |
| Text on correct-answer fill | #1E3D4C | #EDF1F3 | 10.1:1 |
| White on navy tag | #FFFFFF | #1E3D4C | 11.5:1 |
| White on warm maroon tag | #FFFFFF | #8A3324 | 8.1:1 |
| White X on hit square (large bold symbol) | #FFFFFF | #D8374F | 4.6:1 |
| White miss ring on water (non-text) | #FFFFFF | #16306A | 12.6:1 |
| Ship shape on water (non-text) | #9FB0CC | #16306A | 5.7:1 |
| Gold focus ring on water (non-text) | #E0B861 | #16306A | 6.7:1 |
| Answer button border on white (non-text) | #75818E | #FFFFFF | 4.0:1 |

All pairs pass AA except the warm maroon headline word and step numerals on the dark page (2.4:1), which are a brand color choice approved by Dr. Rennie. The title is also in the browser title and each numeral sits beside a text label. All other text pairs pass AAA except the X on a hit square, which passes AAA for large text.

## 4. Keyboard navigation flow verified

Verified with automated browser tests that played complete games at desktop (1200 px) and phone (390 px) widths.

1. Skip link
2. Sound and How to play buttons in the banner, Anatomy and Physiology checkboxes, Topic menu button (opens a list with one checkbox per body system and a + button that shows the topics inside each system, closes with Escape), Level menu (a standard select), Start game. A message says what is still missing if Start game is pressed too early. The game opens in a modal dialog that holds focus and closes with Escape or the Close game button.
3. Question heading receives focus, then the four answer buttons in order
4. Feedback heading receives focus, then the Go to the grid or Continue button
5. Focus moves to the enemy grid. Arrow keys move between squares and Enter fires.
6. End screen heading receives focus, then Play again and Change question set
7. Sound and Close game buttons are in the bar at the top of the dialog

## 5. Screen reader testing

Not yet tested with a screen reader. The markup was written for screen reader use (landmarks, labels on every square, live announcements for every hit, miss and sunk ship), but no reader has been run against it.

## 6. Known limitations and remediation plan

- The 3D battlefield is drawn on a canvas that is hidden from assistive technology. The regular grid buttons stay in the page for keyboard and screen reader use, and the square in focus is highlighted in the 3D view. Mouse and touch players click the 3D grid directly.
- If the 3D library cannot load, WebGL is unavailable, or the player has "reduce motion" turned on, the game uses the flat boards.
- The opening intro plays by itself when the page loads. It tells a short story for about 40 seconds, with each line on screen for about six seconds, then waits on the title for the player to press Press start. A Skip intro button is there the whole time (WCAG 2.2.2). The directions are also in the How to play window, opened with the "?" button. With "reduce motion" on, the intro is skipped entirely.
- Theme music starts with the intro where the browser allows it, and otherwise when the player presses Press start or Skip intro, and a sound button in the banner turns it off (WCAG 1.4.2). It fades out when the game starts.
- Screen reader testing is still needed. Plan: run one full game in VoiceOver or NVDA and confirm the announcements read in a sensible order.
- A blind player can fire on the enemy grid and hears every result, but the layout of their own fleet is summarized (ships afloat and hits taken) instead of read square by square.
- Sound effects have no captions. Every sound has a matching text announcement, and sound can be turned off.

## 7. Reviewer

Prepared by Claude for Dr. Sharilyn Rennie. Awaiting her review.

## Update, November 15, 2026 (phone layout, levels, music)

- Topic menu: tapping or clicking a body system name now checks it. Before, the menu closed without selecting. Fixed by making the menu container focusable by script only (tabindex -1). Keyboard order is unchanged.
- Phone layout: single column, question card first, battlefield below. Enemy grid squares are about 39 px wide on a 390 px phone, which meets the WCAG 2.2 minimum target size of 24 px (2.5.8, AA) but not the 44 px AAA size (2.5.5). The keyboard and screen reader grid is unchanged.
- Wording: "click" changed to "pick" so the hints fit touch, mouse and keyboard.
- Levels: Easy uses course cards tagged DOK 1. Advanced uses DOK 2 and 3. Expert has starter sets only so far.
- Music: the theme now starts on the first tap, click or key press if the browser blocked it at page load. The music note button still turns all sound off (1.4.2 Audio Control).
- Tested on an emulated iPhone 13 in Chromium only. Not yet tested on a real phone or with a phone screen reader (VoiceOver, TalkBack).

## Update, November 15, 2026 (phone view switching)

- On screens up to 860 px wide the game shows one view at a time: the question card, or the battlefield after "Go to the grid". The battlefield stays up until the shots are used, then the next question returns. Nothing depends on scrolling, which was unreliable inside the Kajabi page.
- The hidden view is removed from the tab order and from screen readers (display none for the card, visibility hidden for the battlefield). The keyboard and screen reader grid is unchanged.
- Top bar on phones is shorter (about 133 px, was 196 px) so the question card starts higher.
- Scroll jumps are instant, with no smooth scrolling.
- Tested at emulated phone size (390 px) and laptop size (1280 by 640) in Chromium. Not yet tested on a real phone or inside Kajabi.

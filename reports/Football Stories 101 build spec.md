# Football Stories 101: build specification

Version 1.1, 18 October 2026. This is the hand-off document for the coding session. It turns the research report ("Football stories website plan") plus the owner's decisions into a concrete, buildable plan. Anything marked **DECIDED** is settled by the owner. Anything marked **ASSUMED** is the planner's default and can be overridden before coding starts. Anything marked **LATER** is deliberately deferred.

---

## 1. What we are building, in one paragraph

A free, non-commercial football storytelling publication called **Football Stories 101**, modelled directly on The Morning Founder's structure: one researched story every day, seven days a week, 1,200 to 1,800 words, each with its own illustration, delivered by email at 8:00 am Singapore time on weekdays and 10:00 am on weekends, and archived on a fast static website. Scope is global: footballers and stars past and present, clubs, and periods of success or dynasty eras. The publication speaks in a brand voice under a pen name; the owner stays out of frame. Stories are then posted daily to Facebook, Instagram, Threads and Telegram. There is no monetisation, no paywall and no sponsorship.

## 2. Decisions locked by the owner

| Topic | Decision |
|---|---|
| Purpose | Fun and sharing with other football lovers. No monetisation. **DECIDED** |
| Name | Football Stories 101. **DECIDED** |
| Scope | Global football: players and stars, clubs, history, dynasty and success periods. No Singapore/SEA core. **DECIDED** |
| Cadence | One story a day, seven days a week. **DECIDED** |
| Length | 1,200 to 1,800 words per story. **DECIDED** |
| Send times | 8:00 am SGT Monday to Friday, 10:00 am SGT Saturday and Sunday. **DECIDED** |
| Visuals | One illustration per story, in the spirit of The Morning Founder's watercolours. Style and production method to be chosen later. **LATER** |
| Voice | Brand voice, byline "The Editor, Football Stories 101", owner out of frame. **DECIDED** |
| Email first | Yes, the email is the product, the website is the archive. **DECIDED** |
| Socials | Facebook, Instagram, Threads, Telegram. Not LinkedIn. **DECIDED** |
| Repository | Likely a new repository, to be confirmed. **LATER** |
| Success metric | None required. **DECIDED** |

## 3. Planner's assumptions to confirm

1. **Email first, website one week later. DECIDED.** Exactly The Morning Founder's structure: the email carries the full story at the fixed time, the website publishes the same story seven days later. Implemented as a single setting (`WEB_LAG_DAYS`, default 7); social posts go out on email day and link to the Subscribe page until the web version is live.
2. **Each story is a numbered issue. DECIDED.** "Story No. 001" and so on, mirroring the "Plate" numbering, shown on the story page, in the email subject and in the social caption.
3. **Newsletter provider is Buttondown. DECIDED.** Reasons: it accepts Markdown, so the exact story file that builds the web page is the email body; it has a full API on every plan including free, which the automated send needs; the archive stays on our site. Cost is free to 100 subscribers, then about US$9 a month. If zero cost matters more, Kit's free tier (reported up to 10,000 subscribers, single-sourced) is the fallback; the send script is written against a thin adapter so the provider can be swapped. The Morning Founder itself uses beehiiv; beehiiv is a fine alternative but its API, which the automated daily send needs, is not on the free tier, so matching it exactly costs money from day one.
4. **Domain is footballstories101.com if available, else .co or .net. DECIDED.** Availability has not been checked from this session. The site works at the github.io address until a domain is bought.
5. **Four content pillars: Players, Clubs, Eras & Dynasties, Moments. DECIDED.** "Moments" covers single matches, finals and turning points, which the owner's scope implies but did not name.
6. **The first thirty stories are written before launch day. DECIDED.** See section 8.

## 4. Honest note on the daily cadence

Seven stories a week at 1,200 to 1,800 words is roughly 10,000 words of researched, fact-checked prose every week, indefinitely. Joel Chue does this as his main occupation after a 20-year career, and keeps a backlog of about 260 researched stories. Every solo creator in the research who tried daily output without a backlog either burned out or decayed to irregular posting. The owner has chosen daily, so the plan makes daily sustainable rather than arguing against it: a pre-launch backlog, a research-to-draft workflow that uses AI assistance under strict sourcing rules, scheduled publishing so a missed morning never happens live, and a "repeat" mechanism that re-sends an archive story if the queue runs dry. If the cadence later proves too heavy, the only change needed is the schedule file.

## 5. Content system

### 5.1 The story template (fixed unit, repeated daily)

- **Headline** in the "Subject / angle" convention, for example "Ferenc Puskás / The exile who scored 156 goals for Real Madrid" or "Nottingham Forest / Two European Cups from the Second Division".
- **Dek**: one sentence, the counter-intuitive hook or striking number.
- **Opening**: start inside a specific moment, date and place. No throat-clearing.
- **Body**: 1,200 to 1,800 words, chronological or hinge-and-flashback, with two or three pull quotes drawn from sourced interviews or contemporary reports.
- **Turn**: the decision, accident or trait that explains the outcome.
- **Close**: a short "What it tells us" paragraph of two to four sentences, then a one-line question to the reader (drives comments on Facebook and replies on email).
- **Sources footer**: every story lists its sources. Two independent sources for every factual claim; disagreements stated in the text.
- **Illustration**: one hero image per story, square-friendly crop, used for the web hero, email header, Instagram post and share card.

### 5.2 Pillars and taxonomy

| Pillar | Examples | Sourcing difficulty | Evergreen value |
|---|---|---|---|
| Players | Puskás, Garrincha, Weah, Baggio, Schmeichel, one-club men, cult heroes, forgotten pioneers, women's pioneers | Low for legends, medium for obscure | High |
| Clubs | Origins, derby roots, stadium moves, badge and colour stories, relegation-to-glory arcs | Low to medium | High |
| Eras & Dynasties | Real Madrid 1956 to 1960, Ajax 1971 to 1973, Milan under Sacchi, Lyon's seven titles, Barcelona 2008 to 2012, Celtic's nine | Low | High |
| Moments | Forgotten finals, the match that changed a club, famous debuts and farewells, on-this-day anniversaries | Low | High, with annual spikes |

Cross-cutting tags on every story: `clubs`, `players`, `countries`, `competitions`, `decades`, `themes` (migration, politics, injury, money, management, goalkeeping, youth). Optional `series` with an order number for multi-part runs, for example "The seven who beat Real Madrid".

### 5.3 Living-persons rule (non-negotiable)

Any allegation about a living person (match-fixing, doping, misconduct, private life) is included only if it is an established fact from a reputable primary source (conviction, official finding, the person's own admission), phrased as attributed fact, and only if the story needs it. Otherwise omit. Prefer documented events and, where in doubt, deceased subjects. Singapore treats republication as publication; defamation awards against individual bloggers have reached six figures in Singapore dollars.

### 5.4 Image rules

- Default hero is the commissioned or generated illustration (method decided later). This also solves the share-image problem.
- Photos only from Wikimedia Commons with author, licence and source link in the credit; from the owner's own photography; or under a paid licence (Alamy individual licences from about £17). No Getty editorial of English football without the extra FAPL licence. No match footage anywhere.
- No club crests as design elements or in share images (registered trademarks). Use club names, colour swatches or kit silhouettes.

### 5.5 Style guide essentials for the brand voice

Third person, past tense for history, present tense for the "What it tells us" close. British English spelling. Numbers as numerals for scores, ages, fees and attendances. Full names on first mention. No "I". No exclamation marks. Headline convention and dek length enforced by the CMS schema (dek max 160 characters).

## 6. Site architecture

### 6.1 Content model (front matter, also the CMS form)

```yaml
number: 1                     # Story No., integer, unique
title: "Ferenc Puskás / The exile who scored 156 goals for Real Madrid"
dek: "He arrived fat, 31 and banned. He left with three European Cups."
slug: "ferenc-puskas-real-madrid-exile"
date: 2027-01-04T00:00:00Z    # publish instant in UTC (8am SGT weekdays = 00:00Z, 10am SGT weekends = 02:00Z)
updated: 2027-01-04
pillar: players               # players | clubs | eras | moments
players: ["Ferenc Puskás"]
clubs: ["Real Madrid", "Budapest Honvéd"]
countries: ["Hungary", "Spain"]
competitions: ["European Cup", "La Liga"]
decades: ["1950s", "1960s"]
themes: ["exile", "late-career"]
series: null
seriesOrder: null
hero:
  src: "/images/stories/001-puskas.jpg"
  alt: "Watercolour of a stocky forward in white striking a left-footed shot"
  credit: "Illustration: Football Stories 101"
sources:
  - "Puskás on Puskás, Rogan Taylor and Klara Jamrich (1998)"
  - "https://www.rsssf.org/..."
draft: false
```

Reading time is computed at build. Validation rejects a story with no sources, no alt text, a dek over 160 characters, a duplicate number, or a body outside 1,100 to 1,900 words (soft warning, not a hard fail).

### 6.2 Pages

- **Home**: today's story as the lead, "On this day" slot driven by the anniversary calendar, latest seven stories, pillar entry points, subscribe box.
- **Story page**: hero and credit, Story No., date, reading time, body with pull-quote and captioned-image components, "What it tells us" close, sources footer, plain-URL share buttons (WhatsApp, Facebook, Threads, X, Telegram, copy link; no third-party scripts), related stories by club, pillar and era computed at build, previous and next within a series, subscribe box.
- **Index pages**, auto-generated: per pillar, club, player, country, competition, decade, theme and series; archive by year and month; "all stories by number".
- **Timeline component** for club histories and careers, reusable inside story bodies (MDX).
- **Search** page with Pagefind (static index, no server).
- **About**: what the publication is, the editorial standards, the two-source rule, the AI-assistance disclosure, the living-persons rule, a corrections log page.
- **Subscribe** page: the form, the send times, a one-line PDPA consent note, link to a short privacy page.
- **Links** page (replaces Linktree) for the Instagram bio.
- **RSS** (full text), sitemap, robots, 404, favicon set, web manifest.

### 6.3 Plumbing and quality bar

Open Graph and Twitter-card meta on every page; per-story share image (1200x630) and Instagram card (1080x1350) generated at build from the hero and headline; Article JSON-LD; canonical URLs; system or self-hosted fonts; AVIF/WebP responsive images with dimensions set; dark mode; mandatory alt text; Lighthouse mobile target 95 or higher on story pages.

## 7. Technical stack

| Layer | Choice | Why |
|---|---|---|
| Generator | Astro with Markdown/MDX content collections | Components for timelines and pull quotes, build-time image and share-card generation, fast static output |
| Hosting | GitHub Pages via GitHub Actions (`withastro/action`) | Free, already in use, Actions deploys are exempt from the 10-builds-per-hour limit |
| Editor | Pages CMS, configured by `.pages.yml` | Hosted, free, GitHub login, no OAuth server to run, form fields mirror the front matter |
| Search | Pagefind | Static, small index, no server |
| Share images | `astro-og-canvas` or Satori + resvg-js | Build-time, no external service |
| Newsletter | Buttondown (adapter pattern; Kit as fallback) | Markdown emails, API on free tier, scheduled sends |
| Telegram | Telegram Bot API from the publish workflow | Free, trivial, fully automated daily post |
| Analytics | Umami Cloud free tier or GoatCounter | Cookieless, no consent banner |
| Dependencies | Dependabot grouped monthly | Reviewable update bundles |

### 7.1 The daily publish pipeline (the heart of the build)

Two scheduled GitHub Actions workflows plus one on-push workflow:

```
cron "0 0 * * 1-5"   -> 08:00 SGT Monday to Friday
cron "0 2 * * 0,6"   -> 10:00 SGT Saturday and Sunday
on: push to main     -> rebuild only (no send)
```

Each scheduled run:

1. **Build** the site including only stories with `date <= now - WEB_LAG_DAYS` and `draft: false`, so a story appears on the web seven days after its email. The home page shows the latest web-published story and a "Today's story is in your inbox" subscribe prompt.
2. **Deploy** to GitHub Pages.
3. **Select** today's story: the one whose `date` falls in the last 24 hours and is not yet in `data/sent.json`.
4. **Send** the email via the provider API: subject "Story No. 001 · Ferenc Puskás / The exile who scored 156 goals for Real Madrid", body is the story Markdown with the hero at the top and a footer linking to the web page and unsubscribe.
5. **Post to Telegram**: hero image plus headline, dek and link.
6. **Write social assets** to `social/NNN.md`: Facebook caption (text story summary ending in the reader question, link in first comment), Instagram caption with hashtags and alt text, Threads post (hook plus three to five facts), and the paths of the generated 1080x1350 cards. The owner copies these into Meta Business Suite or a free scheduler; automation of Facebook, Instagram and Threads through the Meta API is a later phase.
7. **Record** the send in `data/sent.json` and commit it back, so a re-run never double-sends.
8. **Fallback**: if no story is due, pick the archive story with the nearest anniversary and send it as "From the archive". This guarantees the daily rhythm even on a missed day.

GitHub cron can run several minutes late under load; this is acceptable for a newsletter. Secrets (newsletter API key, Telegram bot token, chat id) live in repository secrets.

### 7.2 Repository plan

Create a new repository, working name `football-stories-101`, served first at `<user>.github.io/football-stories-101` or at the custom domain once bought. Reason: the existing `inzyspencersg.github.io` repo hosts an auto-committing dashboard that refreshes several times a day, which would trigger constant unrelated rebuilds. The coding session needs GitHub access to the new repository granted first (the current session's pushes were refused with a 403).

Suggested layout:

```
football-stories-101/
  .github/workflows/        build-deploy.yml, publish-daily.yml
  .pages.yml                Pages CMS schema
  astro.config.mjs
  src/content/stories/      001-ferenc-puskas.mdx ...
  src/content/calendar/     on-this-day anniversaries
  src/components/           PullQuote, Timeline, Figure, Share, Subscribe
  src/layouts/, src/pages/
  public/images/stories/
  scripts/                  publish.ts (select, send, telegram, social), validate.ts
  data/sent.json
  docs/                     style guide, living-persons rule, image rules, runbook
```

## 8. Editorial operations for a daily publication

### 8.1 Research-to-publish workflow per story (target 60 to 90 minutes with AI assistance)

1. Pick from the **story bank** (a spreadsheet or Markdown list of candidate angles, tagged by pillar and anniversary date). Keep at least 100 angles banked.
2. **Research brief**: gather five to ten sources (books, RSSSF, 11v11, Transfermarkt for dates and fees, contemporary newspaper archives, club official histories, long-form pieces). Note the two best sources per key claim.
3. **Draft** from the brief. AI assistance is allowed for structure and prose, never for facts: every fact in the draft must trace to a source in the brief. The AI-use disclosure on the About page says exactly this.
4. **Fact-check pass**: dates, scores, spellings, quotes verbatim, living-persons rule.
5. **Illustration** produced or commissioned to the brief (method decided later).
6. **Enter** in Pages CMS, set the publish date, `draft: false`. The pipeline does the rest.

### 8.2 Backlog policy

- Launch with 30 finished stories scheduled (one month of mornings).
- Maintain a rolling buffer of at least 14 scheduled stories at all times.
- Batch-write on weekends; two sessions of three stories each keeps the buffer flat.
- Anniversary stories are written the month before and parked on their date.

### 8.3 Weekly rhythm (owner)

| Day | Task |
|---|---|
| Daily, 10 minutes | Post the generated Facebook, Instagram and Threads assets; reply to comments and email replies |
| Weekday evenings, optional | One story draft |
| Saturday | Three stories: research, draft, check |
| Sunday | Three stories plus fill the story bank and check next week's calendar |

## 9. Distribution plan

- **Email**: the complete story at the fixed time. Clicks, not opens, are the metric that still works after Apple Mail Privacy Protection.
- **Telegram channel**: fully automated daily post from the pipeline. Promote it as the "no email" option.
- **Facebook page**: text summary plus illustration natively, link in the first comment, ending with the reader question. Facebook penalises links and rewards native text and images.
- **Instagram**: 1080x1350 carousel from the build (cover with the hook, three to six fact or quote slides, closing slide with "Full story in the link in bio"). Optimise for sends, which Instagram now weights for non-followers.
- **Threads**: hook plus facts, link in reply. Expect little traffic; cheap to maintain.
- **Growth mechanics that worked elsewhere**: personal one-to-one invitations for the first few hundred subscribers; recommendation swaps with adjacent newsletters (English-language football Substacks, football history pages); series that run across consecutive days to build habit.
- **Not in year one**: short video, paid promotion, LinkedIn.

## 10. Legal and compliance checklist

- Living-persons rule applied to every story (section 5.3).
- Sources footer on every story; quotations short and attributed (Singapore Copyright Act 2021 fair use).
- Images per section 5.4; no crests, no footage.
- Subscribe form: purpose stated, consent note, unsubscribe in every email, unsubscribes honoured within 10 business days (PDPA and Spam Control Act). Short privacy page.
- Corrections page, dated, linked from About.
- Pen name is fine; the About page should still give a contact email for corrections and takedown requests.

## 11. Budget (year one, no monetisation)

| Item | Cost |
|---|---|
| Domain | about US$11 a year |
| Hosting, CMS, search, analytics, Telegram, GitHub Actions | US$0 |
| Newsletter | US$0 to 100 subscribers; about US$9 a month after (Buttondown), or US$0 longer on Kit |
| Illustrations | depends on the later decision; US$0 if self-produced |
| Occasional licensed photo | about £17 each, optional |
| Newspaper archive subscription | about £80 a year, optional |
| **Realistic total** | **US$11 minimum; US$120 to 300 if the newsletter crosses 100 subscribers and a few images are licensed** |

## 12. 90-day plan

| Fortnight | Owner | Coding session |
|---|---|---|
| 1 | Confirm assumptions in section 3; pick pen name; buy domain; open Buttondown, Telegram channel, Facebook page, Instagram, Threads; start the story bank (50 angles) | Create repo; scaffold Astro site, content schema, validation, Pages CMS config, build-deploy workflow; placeholder illustration style |
| 2 | Write stories 1 to 8 | Story page, index pages, search, RSS, share images, subscribe form, analytics; publish pipeline with email and Telegram against a test list |
| 3 | Stories 9 to 16; test-read emails on phone | Instagram card generation, social.md output, fallback archive send, About, Subscribe, Links, privacy and corrections pages; Lighthouse pass |
| 4 | Stories 17 to 24; decide illustration method and produce art for 1 to 24 | Dark mode, timeline component, on-this-day calendar, runbook in `docs/` |
| 5 | Stories 25 to 30; soft launch to friends and football group chats; first recommendation-swap outreach | Fix issues from soft launch; Dependabot; backup export of subscribers |
| 6 | **Public launch, Story No. 001 goes out at 8:00 am SGT**; keep buffer at 14 | On-call for pipeline issues; hand over runbook |

## 13. Status of open questions

All assumptions in section 3 were confirmed by the owner on 18 October 2026. The byline is "The Editor, Football Stories 101". Story No. 001 is still to be chosen; it sets the tone and is the one most people will read, so pick it with care.

## 14. Instruction block for the coding session

Build the site described in sections 6 and 7 in a new repository, in this order: scaffold and content schema with validation, story and index pages, search and RSS, share and Instagram card generation, Pages CMS configuration, build-deploy workflow, then the daily publish workflow with the provider adapter, Telegram post, social.md output, sent.json idempotency and archive fallback. Seed the repository with three sample stories (one per pillar, using placeholder illustrations and real sources) so every page type renders. Write `docs/runbook.md` explaining how the owner adds a story, how the schedule works, how to change send times, and how to rotate secrets. Do not add monetisation, comments systems, third-party share SDKs, cookie banners or club crests.

# The Claude Code tools I use every day

Every week brings new plugins, skills and MCP servers for Claude Code. In that noise, these are the 24 I run every day at [gaja](https://trygaja.com), in four categories, plus four worth a try. For each one: what you get, the install lines, and what it adds to every message you send.

## Before you install anything

A skill is cheap to install and easy to forget. Every skill puts its name and description into **every message you send**, whether you use it that day or not, and every MCP server adds its tools. Ten plugins with thirty skills each make a slower, more expensive Claude that follows each instruction less closely.

| Command | What it tells you |
|---|---|
| `claude plugin details NAME` | what a plugin adds to every message, in tokens |
| `claude plugin list` | which plugins are installed, and which are on |
| `claude mcp list` | which MCP servers are connected |
| `/plugin install NAME --scope project` | installs a plugin for one project only |

My rule:

- **On everywhere** only what changes how every session runs, like superpowers.
- **On per project** what serves one kind of work, like gsap-skills, on only for animation work.
- **Off** what you used once.
- **Reviewed before install** when you did not write it. A skill runs with your permissions: [review-skill](https://github.com/unclegian/how-to-build-a-skill) reads it for hidden instructions, secrets read and data sent out, and never runs it.

## Four ways to install

| Route | The line | Rows that use it |
|---|---|---|
| Plugin | `/plugin install NAME@MARKETPLACE` | superpowers, hallmark, watch |
| Skill on its own | `npx skills add OWNER/REPO`, the Skills command line | huashu-design, remotion, defuddle |
| MCP server | `claude mcp add`, or the tool's own setup command | context7, scrapegraph, earshot |
| Its own command line | `npx`, `brew` or `cargo` | gws, ffmpeg-skill, rea |

Rows marked `@claude-plugins-official` install from Anthropic's marketplace. If `/plugin` does not list it, add it first:

```
/plugin marketplace add anthropics/claude-plugins-official
```

---

## 1. Productivity

These change how every session runs: a plan before the work, proof before "done", answers that start with the action, past chats you can search, your Google Workspace from the terminal.

| Tool | What you get | Install | Cost and note |
|---|---|---|---|
| [superpowers](https://github.com/obra/superpowers) | Claude brainstorms with you, writes a plan, works test-first and verifies before it says done | `/plugin install superpowers@claude-plugins-official` | 15 skills, about 850 tokens. On everywhere |
| [mattpocock-skills](https://github.com/mattpocock/skills) | grilling interviews that find the gaps in a plan, specs turned into tickets, handoffs from one session to the next | `/plugin install mattpocock-skills@claude-plugins-official` | 25 skills, about 1,600 tokens |
| [i-have-adhd](https://github.com/ayghri/i-have-adhd) | replies that start with the next action: numbered steps, short, one thing to do at the end | `/plugin marketplace add ayghri/i-have-adhd`<br>`/plugin install i-have-adhd@i-have-adhd` | 1 skill and a hook, about 110 tokens. On everywhere |
| [episodic-memory](https://github.com/obra/episodic-memory) | search by meaning over your past Claude Code conversations, so a decision from last month is one question away | `/plugin marketplace add obra/superpowers-marketplace`<br>`/plugin install episodic-memory@superpowers-marketplace` | 1 skill and a hook, about 100 tokens. After a Node upgrade, run `npm rebuild better-sqlite3` in its plugin folder |
| [understand-anything](https://github.com/Egonex-AI/Understand-Anything) | turns a codebase, a folder of docs or a markdown wiki into a knowledge graph you browse in a dashboard, then answers questions on it: how a flow works, what a change touches, where a new person should start | `/plugin marketplace add Egonex-AI/Understand-Anything`<br>`/plugin install understand-anything` | 9 skills. Run `/understand` once per repository, `/understand-knowledge` on a wiki. The first run reads every file, so it is the expensive one; later runs re-read only what changed |
| [gws](https://github.com/googleworkspace/cli) | Gmail, Drive, Docs, Sheets and Calendar from the terminal, with one skill per service so Claude reads and writes them | `brew install googleworkspace-cli`<br>`npx skills add https://github.com/googleworkspace/cli` | About 70 tokens for the five skills I use. Install only the services you need, for example `.../cli/tree/main/skills/gws-gmail`. Needs your own Google Cloud OAuth client. Not an official Google product |
| [claude-code-setup](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/claude-code-setup) | reads a repository and recommends the hooks, skills, MCP servers and subagents worth adding | `/plugin install claude-code-setup@claude-plugins-official` | 1 skill, about 140 tokens. Run it once per repository |

## 2. Design

For anything a customer sees: the site, decks, product screens. Generated interfaces start to look alike when everyone runs the same design skills, so I review this category every quarter.

| Tool | What you get | Install | Cost and note |
|---|---|---|---|
| [taste-skill](https://github.com/Leonxlnx/taste-skill) | art direction for interfaces that stop looking generated: named styles (minimalist, brutalist, soft), quality bars, reference images | `/plugin marketplace add Leonxlnx/taste-skill`<br>`/plugin install taste-skill@taste-skill` | 13 skills, about 1,700 tokens. Per project |
| [gsap-skills](https://github.com/greensock/gsap-skills) | GreenSock's own guidance for GSAP animations, timelines and scroll effects | `/plugin marketplace add greensock/gsap-skills`<br>`/plugin install gsap-skills@gsap-skills` | 8 skills, about 1,140 tokens. On only for animation work |
| [impeccable](https://github.com/pbakaus/impeccable) | a design vocabulary for the agent: steer with commands like polish and bolder, review with critique, and scan code or a live page for AI design patterns with `npx impeccable detect` | `npx impeccable install` | About 115 tokens. Scanning a URL needs Chrome or Edge installed |
| [huashu-design](https://github.com/alchaincyf/huashu-design) | one sentence in, a design you can hand over: web pages, clickable app prototypes, editable PPTX decks, launch animations, infographics. With no brand assets it shows six thumbnails and develops three directions | `npx skills add alchaincyf/huashu-design` | The README is in Chinese, with `README.en.md` beside it |
| [hallmark](https://github.com/Nutlope/hallmark) | an anti-AI-slop design skill: new pages, audits, redesigns, and a design extracted from a URL or a screenshot, checked with its own `sloplint` | `/plugin marketplace add nutlope/hallmark`<br>`/plugin install hallmark@hallmark` | About 70 tokens. Node 18 or later; the browser checks also need `puppeteer-core` |

## 3. Research and web

For when Claude reads the web: account research, competitor pages, pages that only load with JavaScript, the docs of the library you code against. Most of these are an MCP server with few skills or none, cheap to keep connected. The cost is the API credits each call spends.

| Tool | What you get | Install | Cost and note |
|---|---|---|---|
| [playwright](https://github.com/microsoft/playwright-mcp) | Microsoft's browser connector: click, fill forms, take screenshots, read pages that need JavaScript | `/plugin install playwright@claude-plugins-official` | No skills, close to 0 tokens |
| [firecrawl](https://github.com/firecrawl/firecrawl) | scrape, crawl, search and extract structured data from sites | `/plugin install firecrawl@claude-plugins-official` | 3 skills, about 230 tokens. API key |
| [exa](https://github.com/exa-labs/exa-mcp-server) | web search by meaning, research on companies and people, the content of a page | `/plugin install exa@claude-plugins-official` | 2 skills, about 190 tokens. API key |
| [agent-reach](https://github.com/Panniantong/Agent-Reach) | search and read the places Claude's own web tools barely reach: X, Reddit, YouTube, Xiaohongshu and more | Paste to Claude:<br>`Install Agent Reach: https://raw.githubusercontent.com/Panniantong/Agent-Reach/main/docs/install.md` | About 330 tokens. Some platforms need a login. The package called agent-reach on PyPI is a different project: install from the GitHub link only |
| [scrapegraph](https://github.com/ScrapeGraphAI/scrapegraph-mcp) | say in plain words what you want from a page and get structured data back; scrape, crawl, and watch pages for changes | `claude mcp add --transport http scrapegraph https://mcp.scrapegraphai.com/mcp --header "X-API-Key: YOUR_KEY"` | MCP server, no skills. API key from the ScrapeGraph dashboard |
| [context7](https://github.com/upstash/context7) | current, version-specific docs and code examples for the library you code against, so Claude stops writing APIs from old training data | `npx ctx7 setup --claude` | MCP server or skill, you choose at setup. A free API key raises the limits. Node 22.13 or later |
| [defuddle](https://github.com/kepano/defuddle) | turns a web page into clean markdown without the menus and the clutter, so reading a page costs fewer tokens | `npx skills add kepano/obsidian-skills --skill defuddle` | About 70 tokens. The skill comes from Steph Ango's obsidian-skills; the command line alone is `npx defuddle parse URL --markdown` |

## 4. Content and video

For when you publish: launch films, product videos, their sound. These cover the input, a video Claude watches, and the output, a video Claude writes, edits and checks. The writing itself still needs your own voice rules.

| Tool | What you get | Install | Cost and note |
|---|---|---|---|
| [watch](https://github.com/bradautomates/claude-video) | Claude watches a video, from a link or a file: frames plus transcript | `/plugin marketplace add bradautomates/claude-video`<br>`/plugin install watch@claude-video` | 1 skill and a hook, about 100 tokens, about 8,000 per video. Its frame extraction fails on ffmpeg 9: extract the frames with ffmpeg by hand |
| [hyperframes](https://github.com/heygen-com/hyperframes) | HeyGen's video as HTML: compositions, captions, voiceover, a website turned into a video, and a review of the result frame by frame | `/plugin install hyperframes@claude-plugins-official` | 9 skills. Its command line also measures a finished mp4: `npx hyperframes measure cuts FILE`. Set `HYPERFRAMES_NO_TELEMETRY=1` |
| [remotion](https://github.com/remotion-dev/skills) | Remotion's own skills for videos written in React: compositions, animation, rendering | `npx skills add remotion-dev/skills` | The skills repository declares no licence. Read Remotion's licence before company use |
| [earshot](https://github.com/Leonxlnx/earshot) | Claude hears, reviews and makes sound: a bank of sound effects made in code, and `earshot critique`, a scorecard of a film's audio against professional launch films | `uv tool install "earshot[mcp] @ git+https://github.com/Leonxlnx/earshot"`<br>`claude mcp add earshot --scope user -- earshot mcp` | Runs on CPU. Sound effects need no models; the analysis downloads about 1.1 GB once, with `earshot doctor --fetch`. Run critique on the final mp4, since encoding can change the loudness |
| [ffmpeg-skill](https://github.com/kajisho5/ffmpeg-skill) | a local video editor for Claude: probe, cut, reframe 16:9 to 9:16, animated captions and export across 42 FFmpeg tools, and a check of its own output | `npx ffmpeg-skill` | No cloud, no API key. Captions from speech need `pip install faster-whisper`. Run the install again to update |

Prefer plain files you own and can read for memory? [claude-personal-memory](https://github.com/unclegian/claude-personal-memory) is my take: a small personal brain with a journal per day, a mistakes log, and six skills that read and write it.

---

## Worth a try

Not part of my day yet. Each one does something no tool above does.

| Tool | What you get | Install | Note |
|---|---|---|---|
| [cli-anything](https://github.com/HKUDS/CLI-Anything) | builds a command line for desktop software, so Claude can drive apps that have no API; CLI-Hub lists the ones others built | `/plugin marketplace add HKUDS/CLI-Anything`<br>`/plugin install cli-anything` | Installed here and switched off. The hub: `pip install cli-anything-hub` |
| [rea](https://github.com/morluto/rea) | Reverse Engineer Anything: one MCP that inspects native binaries, JavaScript and Electron apps, .NET assemblies and websites, explains how a feature works with the evidence, and builds a version for your project | `npx rea-agents setup` | Analysis runs locally. Native analysis uses Hopper, Ghidra or IDA if installed. Repositories with similar names exist: install only from morluto/rea, rea.tools or the rea-agents npm package |
| [craft-anything](https://github.com/storytold/craft-anything) | point it at a website, an app or a game and say what you want: it studies the original, has your coding agent build your own version, and scores how alike they are | `git clone https://github.com/storytold/craft-anything && cd craft-anything`<br>`cargo install --path apps/craft-anything-cli` | A clean-room engine in Rust, 1.97 or later, plus a coding agent signed in. A desktop app is on its downloads page |
| [humanizer](https://github.com/blader/humanizer) | removes the tells of AI writing from a draft | `/plugin marketplace add blader/humanizer`<br>`/plugin install humanizer@humanizer` | 1 skill. Claude Code 2.1.142 or later. My own check is [claude-antislop](https://github.com/unclegian/claude-antislop), which runs as hooks on every file and reply; humanizer is the rewrite you call by hand |

---

## Related lists

- [awesome-claude-code-for-gtm](https://github.com/matteotitta/awesome-claude-code-for-gtm), Matteo Titta's list for go-to-market work: skills, agents, connectors and courses. The one that gave me the idea for this page.
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code), the general list.
- [claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice), a guide to setting Claude Code up.
- [claude-code-system-prompts](https://github.com/Piebald-AI/claude-code-system-prompts), the prompts Claude Code runs on, for reference.

## The Skill kit

This repository is one of four:

- [How to build a skill](https://github.com/unclegian/how-to-build-a-skill): the guide, the format, a template, and two skills that create and review skills.
- [Claude personal memory](https://github.com/unclegian/claude-personal-memory): a small personal brain in plain files you own. Claude remembers who you are, your goals and what you corrected.
- Claude Code daily: this one.
- [Claude antislop](https://github.com/unclegian/claude-antislop): keeps the tells of AI writing out of what Claude writes, with a list of 61 patterns, hooks that check every file and reply, and a skill that rewrites a draft until it is clean.

<!-- CTA -->
---

## Want these tools working on your team's go-to-market?

At gaja we build two things for go-to-market teams:

- **The knowledge your Claude reads**: your ICP, your deal stages, your objections, your voice, built from your calls, docs, tools and team.
- **The shared skills your team runs**: written on the processes you already follow, deployed to the whole team, all reading the same knowledge.

Get in touch:

- Gianluca D'Auria, Co-founder at gaja: gianluca@trygaja.com, [LinkedIn](https://www.linkedin.com/in/gianlucadauria-gaja/)
- gaja: [trygaja.com](https://trygaja.com), [LinkedIn](https://www.linkedin.com/company/gaja-brain/)

MIT licence.

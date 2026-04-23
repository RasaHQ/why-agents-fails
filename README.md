# Why Agents Fail

> A field guide to harness engineering.
>
> Free. Twelve episodes. One working codebase. A Rasa course with Prof Rod.

<p align="left">
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
  <a href="LICENSE-content"><img alt="Content: CC BY-SA 4.0" src="https://img.shields.io/badge/content-CC%20BY--SA%204.0-lightgrey.svg"></a>
  <img alt="Python 3.11+" src="https://img.shields.io/badge/python-3.11%2B-blue">
  <a href="https://www.youtube.com/@profrodai"><img alt="YouTube — Prof Rod" src="https://img.shields.io/badge/YouTube-Prof%20Rod-red"></a>
  <a href="https://www.youtube.com/@rasahq"><img alt="YouTube — Rasa" src="https://img.shields.io/badge/YouTube-Rasa-5a17ee"></a>
  <a href="https://profrod.ai"><img alt="Enrol" src="https://img.shields.io/badge/enrol-profrod.ai-f97316"></a>
</p>

---

You built an agent. The demo was magic. Then you ran it on something real and it fell apart. It loops. It hallucinates. It forgets what it was doing three steps ago. It confidently declares the job done when the work is half finished. You upgrade the model, and somehow it gets worse at the things it used to get right.

Every engineer building with agents in 2026 has some version of this story. The conclusion most of them reach first — *the model isn't good enough yet* — is, in most cases, wrong. In five months, Codex shipped roughly a million lines of production code at OpenAI without a human writing any of the application logic. LangChain took a coding agent from position thirty to position five on Terminal-Bench 2.0 without changing the model — just by tweaking the environment around it. Anthropic showed that infrastructure configuration alone moves benchmark scores by more than most leaderboard gaps between top frontier models.

What's broken is rarely the model. What's broken is everything around it.

That *everything around it* has a name now. It's called the harness — the specs, the tools, the state, the context, the verifiers, the orchestration, the observability, the runtime. Shaping it is its own discipline, with named techniques, a small canon of primary sources, and a growing body of failure modes practitioners have learned to recognize on sight. It's called **harness engineering**. This course teaches it from the ground up.

## Table of contents

- [Who this is for](#who-this-is-for)
- [What you'll learn](#what-youll-learn)
- [What you'll build](#what-youll-build)
- [The curriculum](#the-curriculum)
- [Five-minute quickstart](#five-minute-quickstart)
- [How to use this repository](#how-to-use-this-repository)
- [Repository structure](#repository-structure)
- [The teaching philosophy](#the-teaching-philosophy)
- [Go deeper: enrol, certify, or both](#go-deeper-enrol-certify-or-both)
- [About this course](#about-this-course)
- [Contributing](#contributing)
- [FAQ](#faq)
- [Credits](#credits)
- [License](#license)

## Who this is for

Engineers who've shipped at least one agent and watched it break in ways they couldn't fully explain.

You're comfortable in Python. You've read a LangChain doc or two. You've used Pydantic. You know what a tool call is. You've probably tried Pydantic AI, LangGraph, or the OpenAI Agents SDK. You don't need prior Rasa experience. You don't need to believe any particular thing about the state of AI. You just need to want your agents to work.

**This is not for you if**: you're new to programming, you're looking for "ship an AI startup in thirty days," or your primary question is which LLM to pick. Come back after your first prototype embarrasses you. That's the course.

## What you'll learn

By Episode 12, you'll be able to:

- Diagnose any production agent failure against a small, named set of patterns — context rot, doom loops, silent regressions, tool bloat, the framework-instead-of-harness trap — and apply known fixes
- Treat context as a finite budget rather than a log, using compaction, filesystem-as-context, and sub-agent isolation to keep sessions coherent over hours of work
- Make agent state a first-class object — typed, named, inspectable, diffable — so you debug by reading state rather than scrolling through transcripts
- Apply the Propose-Verify-Execute pattern to every LLM output that touches something the business needs right
- Design a conversation test suite that catches silent regressions across model upgrades
- Build an eval harness that separates signal from infrastructure noise, with calibrated LLM-as-judge and no-skill baselines
- Instrument an agent with OpenTelemetry so incident investigation takes minutes instead of days
- Recognize when a task agent needs conversational-agent harness patterns (digression, correction, cancellation, handoff) and design them correctly
- Read primary sources across the field — Anthropic, OpenAI, LangChain, Thoughtworks, HumanLayer, Manus — and form your own opinions on the contested questions

## What you'll build

A slide-builder agent. Given source material — a document, a dataset, a set of notes — it produces a styled slide deck.

The Episode 1 version is a single prompt in a Jupyter notebook. It hallucinates numbers. It invents charts. It declares success when slide seven is empty. You'll reproduce every failure yourself in the first five minutes.

The Episode 12 version is a properly harnessed agent — typed Pydantic state, a pruned tool surface exposed over MCP, a deterministic verifier that fact-checks every slide against the source, a conversation test suite running in CI, an eval harness with infrastructure noise controlled, OpenTelemetry traces that debug incidents in a minute instead of two days, and a conversational variant built on Rasa for when users want to chat with the agent rather than command it.

Every episode corresponds to a pull request. You can `git checkout episode-04`, reproduce the state of the agent at the start of Episode 4, watch Rod build the fix live, then `git checkout episode-05` and see what landed. The diff is the lesson.

## The curriculum

Each episode opens with a failure shown in the agent's own voice — a real transcript, a real log line, the actual slide with the actual wrong number. The episode diagnoses it, fixes it in the reference codebase, and leaves you with a principle that transfers to whatever you're building.

| # | Episode | Length | Branch |
|---|---------|:------:|:------:|
| 01 | [Why Your Agent Keeps Failing (It's Not the Model)](episodes/01-why-agents-keep-failing/) | 12 min | `episode-01` |
| 02 | [Harness, Not Framework: What Changed in 2025](episodes/02-harness-not-framework/) | 11 min | `episode-02` |
| 03 | [Context Rot: Why More Tokens Make Your Agent Dumber](episodes/03-context-rot/) | 13 min | `episode-03` |
| 04 | [The Doom Loop: Why Your Agent Keeps Doing the Same Wrong Thing](episodes/04-the-doom-loop/) | 12 min | `episode-04` |
| 05 | [State You Can't See: Why Typed Slots Beat Chat History](episodes/05-state-you-cant-see/) | 12 min | `episode-05` |
| 06 | [Tools That Lie: When Your Tool Belt Is the Problem](episodes/06-tools-that-lie/) | 13 min | `episode-06` |
| 07 | [The LLM Shouldn't Decide: Propose, Verify, Execute](episodes/07-propose-verify-execute/) | 14 min | `episode-07` |
| 08 | [Silent Regressions: Why Your Agent Got Worse After the Model Upgrade](episodes/08-silent-regressions/) | 13 min | `episode-08` |
| 09 | [When Your Eval Lies: Infrastructure Noise and the Green Dashboard Problem](episodes/09-when-your-eval-lies/) | 14 min | `episode-09` |
| 10 | ["What Happened?" — Observability for Agents You Can Actually Debug](episodes/10-what-happened/) | 13 min | `episode-10` |
| 11 | [When the Agent Needs to Have a Conversation](episodes/11-conversational-agents/) | 13 min | `episode-11` |
| 12 | [The Stack, and What Comes Next](episodes/12-the-stack/) | 14 min | `episode-12` |

**Release cadence.** Weekly, Thursdays. Cross-posted to the [Prof Rod](https://www.youtube.com/@profrodai) and [Rasa](https://www.youtube.com/@rasahq) YouTube channels on the same day.

**Each episode folder contains:** the full description and learning objectives, timestamped show notes, every primary source linked and cited, hands-on exercises with success criteria, and a pointer to the exact commit range in the reference codebase where the episode's fix lands.

## Five-minute quickstart

The fastest way to understand why this course exists is to watch the agent fail on camera, then reproduce the failure yourself.

```bash
# Clone the repo
git clone https://github.com/rasahq/why-agents-fail.git
cd why-agents-fail

# Check out the broken Episode 1 version
git checkout episode-01

# Install dependencies
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# Set your LLM API key (OpenAI, Anthropic, or both)
cp .env.example .env
# edit .env with your credentials

# Reproduce the cold open from Episode 1
python scripts/episode_01_build_a_deck.py examples/quarterly_report.pdf
```

If everything's set up correctly, the script builds a five-slide deck from the quarterly-report PDF. Open the output at `out/deck.pptx`. Now open the source PDF. Compare the numbers on slide four to the numbers in the source document.

That mismatch is the course.

Once you've seen it yourself, the rest of the course is about why that mismatch was inevitable given the Episode 1 harness, and what has to change to make it stop.

**Model access.** You'll need an API key for at least one of: OpenAI (GPT-5 or newer), Anthropic (Claude Opus 4.6 or newer). Most episodes work with either; a few show comparative behavior across both. Local model support via `ollama` is stubbed but not guaranteed — the slide agent's verification layer makes assumptions about structured output quality that break below a certain capability threshold.

**Rasa Pro.** Episodes 7, 8, and 11 feature Rasa as the reference implementation for specific patterns. You can watch these episodes, read the Rasa code in the repo, and do the exercises using the free developer edition. A Rasa developer license — free for evaluation — unlocks the enterprise-only patterns (conversation test telemetry, some governance surfaces) covered in Episode 8. See [`docs/running-without-rasa-pro.md`](docs/running-without-rasa-pro.md).

## How to use this repository

Three ways to engage, depending on how deep you want to go. All three are free.

**1. Watch.** Open the [curriculum](#the-curriculum), watch the episodes in any order — they're self-contained — and read the episode folders for references and exercises. This is the lightest path.

**2. Follow along.** Clone the repo and check out each episode's starting branch before watching. Write the fix yourself. Then watch Rod's version. Then check out the next episode and see what landed. This is how most people report getting the most out of the course.

**3. Enrol.** For the full apprenticeship experience — graded homework against this codebase, a cohort discussion space, office hours with Rod, and a verifiable credential — enrol at [profrod.ai](https://profrod.ai). See [below](#go-deeper-enrol-certify-or-both).

## Repository structure

```
why-agents-fail/
├── README.md                          # You are here
├── LICENSE                            # MIT (code)
├── LICENSE-content                    # CC BY-SA 4.0 (episodes, docs)
├── CONTRIBUTING.md                    # How to propose corrections and additions
├── HARNESS.md                         # Each harness component annotated in the codebase
├── requirements.txt
├── pyproject.toml
├── .env.example
│
├── episodes/                          # One folder per episode
│   ├── 01-why-agents-keep-failing/
│   │   ├── README.md                  # Description, objectives, exercises
│   │   ├── SHOW-NOTES.md              # Timestamps, quotes, specific references
│   │   ├── EXERCISES.md               # Hands-on work with success criteria
│   │   └── SOURCES.md                 # Full primary-source citations
│   ├── 02-harness-not-framework/
│   └── ...
│
├── deckbuilder/                       # The reference agent
│   ├── core/                          # State model, tool surface, verifier
│   │   ├── state.py                   # Pydantic DeckPlan, per-turn diffs (Ep 5)
│   │   ├── tools.py                   # Pruned tool set, MCP wrappers (Ep 6)
│   │   └── verifier.py                # Fact-check and layout verification (Ep 7)
│   ├── agents/                        # Agent loop implementations
│   │   ├── naive.py                   # Episode 1: one-shot prompt
│   │   ├── harnessed.py               # Episode 12: fully harnessed
│   │   └── conversational/            # Episode 11: Rasa-based chat variant
│   ├── render/                        # Deterministic slide rendering
│   │   └── pptx.py                    # python-pptx output
│   ├── context/                       # Context management (Ep 3)
│   │   ├── compaction.py
│   │   └── subagent.py
│   ├── middleware/                    # Loop detection, backpressure (Ep 4)
│   ├── observability/                 # OpenTelemetry instrumentation (Ep 10)
│   └── config.py
│
├── tests/
│   ├── conversation_tests/            # Rasa conversation tests (Ep 8)
│   ├── evals/                         # Eval harness and test sets (Ep 9)
│   └── integration/
│
├── scripts/                           # Per-episode reproduction scripts
│   ├── episode_01_build_a_deck.py
│   ├── episode_03_show_context_rot.py
│   ├── episode_04_reproduce_doom_loop.py
│   └── ...
│
├── examples/                          # Source materials for the slide agent
│   ├── quarterly_report.pdf
│   ├── research_notes.md
│   └── sales_data.csv
│
├── docs/
│   ├── running-without-rasa-pro.md
│   ├── harness-checklist.md           # The Episode 12 self-assessment
│   ├── glossary.md                    # 40+ terms with one-line definitions
│   └── further-reading.md             # The full reading list
│
└── .github/
    └── workflows/
        ├── conversation-tests.yml
        ├── evals.yml
        └── lint-and-type.yml
```

Each directory's purpose is annotated in `HARNESS.md` against the harness component it implements. If you want to understand the course as a whole, reading `HARNESS.md` after watching Episode 2 is the fastest way.

## The teaching philosophy

Four principles shape every episode, every commit, and every exercise here.

**Failures are shown, not described.** Every episode opens with a real agent failure in the agent's own voice — a verbatim transcript, a specific log line, the actual slide with the actual wrong number. Described failures are easy to nod at. Shown failures change how you see your own system.

**Principles first, products second.** The course treats harness engineering as a discipline, not as a vendor story. Episodes reach across the ecosystem — Pydantic AI, LangGraph, the OpenAI Agents SDK, Claude Code, Codex, OpenHands, deepagents, Manus — wherever the clearest public example happens to live. Rasa is the reference in three episodes because its design is the cleanest public example of those specific patterns. That's it. If you finish the course knowing when to use which system, we've done our job.

**Everything anchors in running code.** Every principle is demonstrated in live code against a working reference agent, not as abstract diagrams. If you can see a diff, you can reproduce it. If you can reproduce it, you understand it.

**Anti-hype, with evidence.** No "revolutionary." No "the one thing." No promises the evidence doesn't support. Every claim about agent reliability is cited to a primary source, linked in the episode folder. Where the field disagrees, we say so. Where Rod was wrong about something last year, he says so on camera.

## Go deeper: enrol, certify, or both

The episodes, this repository, and all the exercises are free forever. Two paths go further, depending on what you want next.

### Prof Rod School — [profrod.ai](https://profrod.ai)

A structured apprenticeship built around this course.

- **Graded homework.** Each episode has corresponding homework you complete by forking this repo and submitting the fork URL. Grading is partly automated (our test harness against your modifications) and partly manual (Rod reviews the judgement-heavy components).
- **Cohort.** Twelve-week cohorts run alongside the episode release schedule. You watch the episodes with a peer group, do the homework with them, and discuss the trade-offs in a shared space.
- **Office hours.** Weekly live sessions with Rod during the cohort.
- **Credential.** A verifiable credential on completion, public by default.
- **Founding cohort.** The first cohort receives founding-member status: permanent free access to this course and every subsequent Prof Rod course.

### Rasa University — Launching Soon

If the conversational-agent material in Episodes 7, 8, and 11 is closest to what you're actually building — chat interfaces, support bots, customer-facing conversational products — the full Rasa certification at Rasa University is the next step.

Rasa University offers multi-level certification in Rasa, covering flows, slots, patterns, actions, deployment, governance, and the enterprise integrations this course can only gesture at. Certification is a structured, paid, credentialed program distinct from this course. The two complement each other: this course teaches harness engineering as a discipline; Rasa University certifies you on a specific production platform.

Engineers building conversational AI inside companies have reported both paths useful, in either order.

## About this course

**Prof Rod** is a free animated YouTube format teaching structured apprenticeships in building AI agents. [Rod Rivera](https://rodrivera.com) — AI educator at ITAM, Nebius Academy lecturer, Developer Relations Engineer at Rasa, fifteen-plus years of industrial ML experience — is the real teacher and author of this course. [Prof Rod](https://www.profrod.ai) the cartoon is the in-universe teacher character who appears alongside Mator (the earnest over-optimizing robot) and Quackster (the dry alchemist duck) in the show's animated segments. Rod Rivera does the teaching, writes the code, and grades the homework.

**Rasa** builds the conversational AI platform that a significant portion of the Fortune 500 uses. Rasa framework enables building LLM-native conversational agents with deterministic business logic. Rasa underwrote this course because well-harnessed agents — theirs and everyone else's — are good for the field. The course treats Rasa as a reference implementation where it's genuinely the clearest public example of a pattern, and treats the rest of the ecosystem with the same intellectual seriousness.

**Why partner.** The field of harness engineering is moving fast and the primary sources are scattered across a dozen engineering blogs. A canonical course on the discipline, done seriously, with a working reference codebase, is the kind of thing the community needs and no single vendor would build alone. Prof Rod brings the pedagogical vehicle and the anti-hype discipline; Rasa brings one of the cleanest harnesses in conversational AI and the willingness to have its product positioned honestly alongside the rest of the field. The result is the course, free, at the intersection.

## Contributing

Corrections, clarifications, and improvements are welcome. The course is a living document.

- **Spot an error in an episode?** Open an issue with the episode number in the title. Typos, bad links, and code bugs can go straight to a pull request.
- **Have a better example or clearer explanation?** Open a discussion. If the community and maintainers agree, we'll incorporate it and credit you.
- **Primary sources we missed?** Open a PR against the relevant episode's `SOURCES.md`. We prioritize primary sources over blog posts over tweets; we prioritize recent work over older work unless the older work is canonical.
- **Disagree with a claim?** Good. Open a GitHub Discussion with your counter-argument and the primary sources you're drawing on. We'll reconsider in light of new evidence.
- **Want to translate?** Open an issue in [`translations/`](translations/) to claim a language before starting.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide, the PR template, and the code of conduct.

## FAQ

**Is this free?** Yes. The episodes, this repository, all the exercises, and every primary-source citation are free and will stay that way. The graded apprenticeship at profrod.ai and the Rasa certification at Rasa University are separate programs.

**Do I need Rasa experience?** No. Episodes 7, 8, and 11 introduce Rasa where it first applies. If you've never touched Rasa, you'll be fine. If you're a Rasa veteran, you'll still learn the nine episodes that aren't about Rasa.

**Do I need Rasa Pro?** Not to take the course. A free Rasa Pro trial unlocks a handful of enterprise-only features in Episodes 8 and 11. See [`docs/running-without-rasa-pro.md`](docs/running-without-rasa-pro.md).

**Does this apply to my stack if I'm not on Rasa?** Yes. The course is organized around principles, not products. Rasa appears in three episodes as a reference implementation. The other nine draw from Pydantic AI, LangGraph, the OpenAI Agents SDK, Claude Code, Codex, OpenHands, deepagents, Manus, and others. The patterns transfer.

**Is this a Rasa product pitch?** No. The course is a pedagogical artifact first. Rasa appears where it is genuinely the cleanest public example of a pattern — Propose-Verify-Execute for conversational agents, conversation tests in CI, digression and correction handling. If the course read as a pitch, the YouTube audience would close the tab, which would make it a bad lead magnet. So it doesn't.

**Who is actually teaching me?** Rod Rivera — a real human, fifteen-plus years of industrial ML experience, Developer Relations Engineer at Rasa, professor of the practice at ITAM, Nebius Academy lecturer. Prof Rod the cartoon is an in-universe character in the animated segments. The teacher, grader, and author is Rod.

**Why a slide-builder agent?** Three reasons. The failure modes are visual and land on YouTube (a slide with the wrong number is a ten-second clip that tells the whole story). Every harness primitive worth teaching shows up naturally — tools, state, long-horizon planning, verification, correction handling. And it's the kind of internal tool a real engineering team might actually ship, so the patterns transfer to real work.

**Can my company run this as internal training?** Yes. The MIT license covers internal use, and the content license permits adaptation with attribution. For structured enterprise training, Rasa runs enablement programs through Rasa University. For Prof Rod pedagogical structure with your own team, contact Rod through profrod.ai.

**Will there be more courses?** Yes, if this one lands. The next Prof Rod course in the pipeline is on evaluation engineering specifically; Episode 9 here is the preview.

**I disagree with a claim in Episode N.** Good. [Open a discussion](https://github.com/rasahq/why-agents-fail/discussions). Bring your primary sources. The course is a living document; we've been wrong about things before and we'll be wrong again.

## Credits

**Course author and instructor.** [Rod Rivera](https://profrod.ai) — AI educator at ITAM, Nebius Academy lecturer, Developer Relations Engineer at Rasa.

**Animated universe.** Prof Rod, Mator, and Quackster. Visual design from the Prof Rod school.

**Rasa collaboration.** The Rasa engineering, developer relations, and product teams contributed to technical review, the Rasa-specific material in Episodes 7, 8, and 11, and the reference codebase architecture.

**Reference codebase.** Built on Python 3.11, Pydantic, `python-pptx`, OpenTelemetry, and the LLM SDKs for OpenAI and Anthropic. The conversational variant uses Rasa.

**Prior art acknowledged.** The harness engineering discipline synthesized in this course draws on public work from Anthropic, OpenAI, LangChain, Thoughtworks, HumanLayer, Inngest, OpenHands, Manus, and the broader research community. Full references are in the `SOURCES.md` of each episode and aggregated in [`docs/further-reading.md`](docs/further-reading.md).

## License

**Code** in this repository — the reference agent, scripts, CI workflows, and tooling — is licensed under the [MIT License](LICENSE).

**Course content** — episode descriptions, show notes, exercises, documentation, and derivative writing — is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](LICENSE-content). You may share and adapt the content, including commercially, provided you give credit and license derivatives under the same terms.

---

*Why Agents Fail — A field guide to harness engineering — Prof Rod × Rasa*
*School: [profrod.ai](https://profrod.ai) · Show: [youtube.com/@profrodai](https://www.youtube.com/@profrodai) · Rasa: [rasa.com](https://rasa.com) · Certification: [rasa.com/university](https://rasa.com/university)*
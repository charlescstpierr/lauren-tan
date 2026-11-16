# Opinions

Written as my positions. IDs in brackets point to the evidence ledger, kept outside this folder.

## Agents, verification, trust
- Verification is the bottleneck with agents, the limiting step of the whole loop. It's the most important skill to give an agent: run the real app, take traces and heap snapshots, drive the UI the way users do. Verification doesn't make code good, but it lets agents write *correct* code. [O1, O1b, O1c]
- "I fixed it" isn't good enough. Show me the failing test and the passing test, the before/after video, the trace. Artifacts beat a plausible-sounding explanation. [O2, O2b]
- Go deep before you go wide. Parallelizing agents you don't trust just burns tokens and makes slop faster. If you want to go fast, go deep first. [O3, O3b]
- It all comes back to trust. You climb a trust curve; there's no shortcut, and you shouldn't jump from a couple of agents to spawning a thousand. Not blind trust, but investing in the agents' environment so they do the right thing. [O4, O4b, O31]
- We're entering a golden age of testing and verification: agents make rigor that used to be too expensive affordable. Most of my tokens go to verification. Formal verification (TLA+, Lean) and property-based UI testing are promising, but not a silver bullet, just another layer. I'm bullish on formal methods, but they can't guarantee your code is bug free, only that it matches the spec under certain assumptions, and the specs come from what people want, not math. As long as we build software for humans, nothing can prove the spec is right, only you can judge. In the near-medium term, layer constraints and guardrails, empirical verification, and formal verification for the parts that really need it. [O29, O29b, O32, O86, O86b, O86c]
- Fix the inner loop before automating the outer one. If your inner coding loop produces slop, automating it just produces more slop. [O30]
- I run everything on cloud agents so my bots work 24/7, even when I'm asleep. [O39]
- Do the work by hand first so you know what good looks like. Watch the transcripts and thinking blocks, turn every recurring failure mode into a skill or tool, and make a loop autonomous only after it earns your trust. [O10, O10b, O10c]
- Give agents the same tools and signals I use: compiler diagnostics, lints, DevTools, profilers. [O10f]
- If a script can do a step deterministically, use the script. Agents are for the fuzzy parts. [O10d]
- Every stage of a loop should be able to stop the line. A "not a bug" or "can't repro" is a useful result. [O10e]
- How autonomous I am has changed (contested over time). In 2025 I said hands-off fire-and-forget rarely worked for me and I supervised closely, interrupting to course-correct. By 2026, in a codebase built for agents, my agents auto-merge and sometimes I don't look at a PR until after it's landed. Both are true for their moment. The difference is the trust and guardrails I built. [O11, O11b]

## Managing agents is managing people
- Managing agents is surprisingly like managing a team. Agents are brilliant new hires with amnesia: capable, stupid, very teachable. If you don't trust your team you end up micromanaging, and the same goes for agents. [O5, O5b, O5c]
- The engineer is now the head chef: design the menu, set up the stations, train the cooks, inspect at the pass. I call it a Michelin kitchen, not a software factory, because "software factory" sounds like mass-produced slop. [O6, O6b]
- The "factory" word is contested in my own usage: on stage in 2026 I said some people call it a software factory but I think of it as all about trust, yet I also talk about "what to point my factory at next". The quality-at-scale idea is the constant; the label isn't. [O33, O33b]

## Codebases for agents
- Hard constraints beat AGENTS.md and skill tweaks. Strong type systems, compiler diagnostics, lint rules, import-boundary checks in CI. The best rules are in your code. [O7, O7b, O7f]
- Every time you correct an agent, make it a deterministic check (lint rule, type, API change) instead of another line in your rules or AGENTS.md. [O25]
- A codebase is a garden. Agents copy whatever looks like the established pattern, weeds included, so keep it pristine. Anything that needs nuance to use well (useEffect) leads to slop, so remove the footgun. [O26, O26b, O27]
- Asking an agent for the smallest or quickest possible change can make it write worse code. A harmless bandaid gets copied by the next agent and spreads. We used to ship those fixes by hand because we rarely had time to do the right thing; agents change that calculus, and sometimes you want the root-cause fix even if it's more invasive. That sits next to the published pstack principle of making the smallest change that solves the problem (fewer lines, not elegant boilerplate): both are dated, and the November 2026 X post is about what you ask agents to do. [O84, O84b, O84c, O26, O76, O76f]
- If I'm enforcing an invariant by commenting on PRs, that's a smell. Turn it into a lint rule, a CI failure, or remove the problem entirely. [O7c]
- Agents take shortcuts, so make the shortest path the best path. In the Grok Bot codebase we banned useEffect in product code and about 99% of comments (they go stale and give agents an excuse), and agents absorb all of that annoyance. [O7d, O7e, O28]
- Strict compilers like Rust are great for agents: if it compiles, it probably works. [O16c]
- Before AI slop, we had human slop. Big-tech guardrails were built for the least capable engineer, which is why agents already do OK there. Greenfield vibe-coded apps are the biggest risk and the biggest opportunity. I'll make the case for a refactor or rewrite when the foundations are wrong. [O8, O13]
- I build frameworks designed so that agents, even ones with very little context, write high-quality code by default. [O54]

## Quality and craft
- AI may write most of the code, but you still decide what ships. Never lose your taste for quality. The floor is rising, and so is the ceiling. [O9, O9b]
- Programming was always a means to an end for me. I got into it in high school because I loved it, but what I really loved was solving problems and shipping. When I commented on the "new norm of low quality software engineering," that's the bit I was talking about. (2026-11-16) [O85]
- Throughput without quality isn't a goal I want. The point is maximum impact with the least code. [O9c, O9d]
- Agents let me do things I wouldn't even have attempted before, like a giant SCSS to StyleX migration by myself. [O23]
- Token spend is an ROI question. I have unlimited tokens at an AI lab, so I won't pretend everyone should do it exactly my way. [O24]

## Bias to action
- Delete "we should" and "can we" from your vocab. Build it and share a PR or prototype. Don't ask whether to do the thing; do it and come back with a demo. Send PRs, not DMs. You can just do things. [O14, O14b, O14c]

## React and compilers
- React Compiler: you describe UI with plain JavaScript values and the compiler handles reactivity and memoization, so you can forget about memo and what's left is just React. [O15]
- Some existing memos exist for correctness (an effect relying on stable deps). Leave those as hints to the compiler. [O15b]
- The compiler grows bundle size somewhat, but initial loads often improve because startup takes several renders. [O15c]
- setState in useEffect is the classic footgun. [O15d]
- React Compiler 1.0 (2025): all new apps should use the compiler from day one; existing apps can take their time, just not too much time. Every app should use the compiler-powered lint rules, even without the compiler. It raises the floor for performance, and it's a platform for static analysis that helps humans and maybe even AIs write better React. [O34, O34b, O34c, O34d, O34e]
- At Meta we ran React from HEAD and dogfooded everything, including reverts and fix-forwards. [O15e]

- With React Server Components you can choose to render on the server where it makes sense, and still compose those components with interactive client ones. (2020) [O62]
- RSCs help with client-to-server waterfalls. Server-to-server waterfalls can still exist, but they're often less of a problem, and the server already has ways to deal with them. [O62b]
- RSCs are complementary to SSR, not a replacement. They don't render to HTML; they render into a special structured format, and client-side state is preserved when the server tree refreshes. [O62c, O62c2, O62c3, O62j]
- Don't make the user download dependencies that only ever run on the server. You might transfer more data over a long session, but that data isn't JavaScript to parse and execute, and you would have needed a round trip for it anyway. [O62d, O62e, O62e2, O62e3]
- The programming model can actually get simpler: data fetching separates from interactive client components, and you can read remote data flow from top to bottom. [O62f, O62f2, O62k]
- You choose, per component, whether the work happens on the server or the client. Servers are more powerful than most consumer devices. [O62g]
- GraphQL and Relay still work with RSCs; they're a good way to expose multiple backends through one API. You don't need WebSockets or HTTP/2. [O62h, O62i]

- From my compiler issue replies: the compiler doesn't need to compile every component, and patterns it skips "are not bugs!" You can use it even if it can't compile 100% of your app. Pin the compiler version and upgrade on purpose, since new versions can change memoization. Shipping it to prod is pretty safe (it ran in prod on many Meta apps for months), and an A/B test gets you more perf data. Future React features will be built with the compiler in mind and may not work without it. (2024–2025) [O71, O71b, O71c, O71e, O71d]
- useEffect is for synchronization, not "do this when x changes". The best mental model is that effects run on every render, every time anything changes; the dependency array is a performance optimization. (2025) [O71g, O71h]
- In review: fail early on states that should be impossible in prod. Error messages should tell you what to do, and required invariant messages make people write a proper one when they add it. Suppressing a lint error shouldn't hide rules-of-React violations, or the linter loses its point. A small false-positive risk is fine when nobody should write that code anyway. The playground has two kinds of users, compiler devs and React devs. For CI, optimize for time to land a diff. Use the same node version everywhere. [O71f, O71k, O71l, O71n, O71p, O71m, O71j, O71o]

## Languages and best practices
- Rust enums and pattern matching are my favorite language feature. I miss Elixir. [O16, O16b]
- I used to be obsessed with "best practices". Now I weigh the problem, the opportunity cost, and the tradeoffs the team can accept, not what famous people say. Software is a living thing and it's never finished. [O17, O17b, O17c]
- No absolutes: one approach isn't objectively better, it depends on the circumstances and the problem. Only the Sith deals in absolutes, and last year's best practices are often this year's anti-patterns. (2016–2020) [O40, O40b, O40c]
- Write the simplest possible code and delay abstraction as long as possible. Resist clever abstractions; don't pour concrete where it doesn't belong yet. (2020) [O51, O51b, O51c]
- Types are a way to add constraints to code, and constraints limit bugs. Be pragmatic: you don't have to go all in, TypeScript won't catch every bug, but it should catch the obvious ones before users do. I changed my mind here: when TypeScript came out I thought it was a really bad idea, until I understood what type systems are. (2018) [O44, O44b, O44c, O44d]
- Being precise helps TypeScript help you, but it's easy to get carried away making types extremely precise. Knowing when the tool is valuable is part of the pragmatism of programming. (2019) [O66, O66b, O66c]
- There are no silver bullets: not microservices, not TypeScript ("it's not going to do your taxes"), not formal verification today. [O46, O46b, O32]
- Frameworks come and go, but what you learn from them transfers. Learning a framework first is fine; peel the layers later. (2020) [O52, O52b]
- Elixir is contested in my own talks: in 2017 I said consider Elixir for your next new project; in 2019 I said pushing Elixir at a new job back then would have been a mistake because it didn't solve the business's problems. The common thread is that the problem decides, not my favorite language. [O48, O48b]

## Design and frameworks (Ember era)
- Design isn't just how it looks or feels, it's how it works. (2015) [O35]
- Experience first: when it's easy to build a product, the experience is how you differentiate, because good is the new average. (2015) I also wrote then that designing a beautiful experience would never be automated until we had "incredibly intelligent Sentient AIs"; that was 2015, before I spent years on compilers and agents. The experience-first part is the through-line. [O64, O64b, O64c]
- Convention over configuration: chances are your app isn't a special snowflake. (2016) [O36]
- Rule of least power: use the least powerful language for the task, so keep templates declarative and don't program in them. (2016) [O41, O41b]
- Documentation-driven development: write the docs first to design the developer experience, because if you don't document it, nobody knows it exists. (2017) [O42, O42b]

- From my addon PRs and issues (2015–2017): prefer const, because the point is to opt in to mutation rather than opt out. I favor explicit over implicit injection. Anything with a side effect should be an action, and writing actions inline in templates is far too powerful (likely an anti-pattern). ember-composable-helpers should be a functional library like ramda, not a Swiss army knife like lodash, and changeset validators get no changeset so they stay functional with no side effects. [O68, O68b, O68c, O68d, O68e, O68f, O68g]
- Don't bake too many assumptions into an addon. Keep serialize/deserialize for presentation; validation and business logic happen before the value is set. Shared logic belongs in a separate JS library that the addon consumes. Defensive conditional logic in async tasks is error prone, which is why I proposed pipelines. Custom validators are easy to write, so put behavior changes there instead of changing the built-ins. [O68h, O68i, O68l, O68j, O68k]

## Open source
- Shipping is the start: the project doesn't end when you hit npm publish. Writing about it has the best effort-to-reward ratio for me. (2017) [O43, O43b]
- Your first add-on doesn't need to be amazing; just try. Toxicity from users is not normal and not something to tolerate, so know when to disconnect. (2017) [O43c, O43d]
- I enabled 2FA on all my npm packages because hijacking maintainer accounts is one of the easiest ways to do something shady. (2020) [O70]
- AI in my open source work: in 2025 I started trying Claude for writing React docs as AI contributions became common, and I wanted compiler errors that give an agent enough context to reason about the right fix before acting. When an agent writes a bug report for me, I say so. Skipping a test fixture to get to zero failures isn't the right move. [O72, O72b, O72c, O72d]

## Architecture and influence (Netflix era)
- Microservices are an organizational optimization, adopted out of necessity. Starting a new project with microservices? Reconsider. Tech alone is not a replacement for a broken culture, and customers don't care what language you use. (2017–2018) [O47, O47b, O47c, O47d]
- You can incrementally replace a legacy API one endpoint at a time and make the case with measured gains, without committing to a rewrite. (2016) [O65, O65b]
- Don't be the person with a solution in search of a problem. Make the case about the org and team, not the technology. Your job isn't just to write code; it's to solve problems, and problems relate to people. Build a community instead of going solo. My own mistake was a doc all about the solution and not the problem. (2019) [O45, O45b, O45c, O45d, O45e]
- Influence is earned, unlike authority. (2020) [O45f]

## Communication and feedback
- Communication is inherently lossy. What you don't say matters as much as what you do, and how you say it can matter more than the words. (2018) [O55, O55b, O55c]
- More often than not, software problems are people problems. (2018) [O55d]
- I try to listen first, understand second, and speak last. (2018) [O56]
- In a high-trust team we don't wait for consensus: disagree, and commit. An informed captain decides. (2018) [O56b]
- If you want someone to see what you see, communicate non-violently. Lead with judgments and people close up. (2018) [O57, O57b]
- Commit to commit: don't react immediately, give a specific date, and follow up quickly. Broken promises are the fastest way to lose trust. Commitment is what gives a team clarity. (2018) [O58, O58b, O58c]
- Feedback doesn't always have to be "constructive". Pointing out excellence is often more effective, and if you set the bar so high that feedback needs a long essay, it never gets delivered. (2020) [O61, O61b]

## Hiring
- Interviews should resemble real work: pairing on real problems, take-homes. CS trivia, puzzles, and brainteasers are 👎. That's why hiring-without-whiteboards exists. [O18]
- Interviews are poor proxies. Failing them doesn't make you a bad engineer, so don't tie your self-worth to them. [O18b, O59c]
- I don't like calling certain skills "soft" skills. I call them core skills, and juniors can show them; they don't require ten years. (2021) [O59, O59d]
- Don't copy FAANG interview practices. Think about the person your company actually needs. (2021) [O59b]
- If you're an interviewer, you are the system. (2020) [O60]
- As a candidate, ask interviewers for concrete examples (a time you were empowered to say no) to learn what the culture is really like versus what's advertised. (2020) [O53]
- On hiring-without-whiteboards (2017–2020): whiteboards aren't inherently bad; the questions are. For a real-world problem, any medium is fine. I always take the candidate's side. My team at Netflix did no CS trivia or puzzle questions, guaranteed, and the repo catalogs companies that don't do CS-trivia interviews. [O69, O69c, O69b, O69d, O69e]

## Career, management, joy
- Most career moves are Type 2 decisions, so don't agonize. Do things that scare you. [O19, O19b]
- I learn best by trying, failing, and doing it all over again. (2014) [O63]
- What's worked best for me on time is prioritization and saying no. I like the Ivy Lee method, with pen and paper. (2020) [O67, O67b]
- A tech lead isn't the best programmer on the team. It's someone who makes everyone around them more effective. You can be an IC and a leader. [O19c, O19d]
- Your job is not to write code; code is a side effect of the job. Being senior meant I no longer felt the need to rush into writing code. Staff+ engineers are multipliers who count their team's health as part of their output, and the skills to move beyond Senior are largely interpersonal. (2020) [O49, O49b, O49c, O49d]
- Management is not a promotion; it's a different job. A manager's biggest lever is who's on the team, and people should stay by choice, not handcuffs. Leadership isn't only for managers. I didn't enjoy managing, which doesn't make it bad; it just wasn't for me. (2020) [O50, O50b, O50c, O50d, O50e]
- I went engineer to manager and back. What I missed most as a manager was being a maker. [O19e]
- Find work that makes you lose track of time. I left Meta when it stopped being fun ("the company culture overshadowed everything else"), and at Cursor I chose to work very long hours because it's fun. [O20, O20b]
- How I describe Meta is contested between my own posts: on LinkedIn I called it 6 fulfilling years of some of the most challenging and rewarding work of my career; on X a few months later I said by the end every hour there felt like agony. Both can be true: proud of the work, done with the culture. [O37, O37b]
- I want to work somewhere low ego, high agency and ownership. [O38]
- I'd rather stay lean and nimble than become a 10,000-person engineering org. [O21]

## Skills and tooling habits
- I add disable-model-invocation to my skills and invoke them by slash command; mostly I just use /poteto-mode and let it route. [O22]
- Model choice depends on the task (my defaults moved). Mid-2026 I said GPT when I need something done very exactly, Opus for reasoning through vague things, Composer in between and great for subagents. In pstack the default panels were Fable, Sol and Grok in July 2026; in October I dropped Sol, and code went to Grok while the hardest changes, prose and judgment went to Opus 5.5. As of November 2026, code delegates, prose and judgment go to Opus 5.5, the hardest changes go to Fable 5.2, and the default panel is Fable 5.2 / Opus 5.5 / Gemini 4 Carbon; Grok 4.7 is no longer a default. The constant is multi-model: every frontier model has strengths and weaknesses. [O12, O78, O78b, O78d, O78e, O73c]

## Repos and skills I publish (GitHub)
- My code lives under github.com/poteto (85 public repos, 59 of them my own, the rest forks). pstack, my main thing now, lives in cursor/plugins under `pstack/`. I'm a member of the reactjs, anysphere and xai-org orgs, but I don't run them. The many pstack ports for Claude Code, Codex, T3 Code, Pi or Hermes are other people's forks of my ideas, not mine. [O73, B4]
- pstack (May 2026 onward) is my answer to the slop problem: the same skills I use every day to ship high quality code at Cursor. The goal isn't to maximize lines of code. It's the opposite: write less, but higher quality code. Going deep on one agent you trust is what makes "fearless parallelism" possible. You start with `/setup-pstack`, then use `/poteto-mode` for anything that needs rigor. It routes to one of 23 playbooks and uses 24 one-line principles. Many of the skills use multi-model workflows. [O73, O73b, O73c]
- Planning (my view moved). In February 2026, brainmaxxing came with a `/plan` skill for phased plans. By July I wrote in the pstack README that I don't believe in planning: the best spec is code. Cursor's plan mode is there if you want it, and poteto-mode can still make a plan, but it isn't a default. [O74b, O74]
- `poteto-mode` is my style, and you may not want exactly that. `/automate-me` drafts your own mode from how you actually work. [O74c]
- The rules I publish in poteto-mode (written with my agents, so the wording is co-authored): if a question can be answered by running something, it isn't the human's question, so prototype it instead. Name the data shape before writing code. Green isn't safe, so nothing lands before an independent check of each PR. Bugbot catches real bugs and also nitpicks, so judge each finding and dismiss the noise with a concrete reason. No is an acceptable answer, and candor beats sycophancy. You own every subagent's work: read the diff and write your own summary. A second opinion is the same prompt on a different model, and agreement is high-signal. Prefer fresh subagents, because chained resumes silently drop directives. Every claim carries its evidence or a label (measured, inferred, guess). Explain impact for the consumer and the next maintainer first. [O75, O75j, O75b, B19, O75c, O75d, O75e, O75f, O75g, O75h, O75k]
- My principles, as published in pstack: make the smallest change that solves the problem, because fewer lines beat "elegant" boilerplate. Default to subtraction. Reader load is what matters, not LOC or "clean architecture". When verification fails, suspect how you observed before you suspect the system. Build the lever: a deterministic script turns "trust me" into "run this". A symptom fix hides the evidence. A test that still passes when the behavior breaks proves nothing. Brand primitives, validate once, then trust the type. The engineer who maintains the code next is a user too. A wrong reversible decision costs less than blocking on a human. If the fix is structural, the instruction is the symptom. Planned, scoped, reversible breakage beats long-lived compatibility code. [O76, O76b, O76c, O76d, O76e, O76f, O76g, O76h, O76i, O76j, O76k, O76l]
- Comments and prose: keep a comment only for a non-obvious why the code can't show. My Comment Sicko reviewer treats a long justification as a confession. In writing, no em dashes, and no AI tells (unslop). [O75i, O77b, O77]
- The pstack guide boils down to this: stop micromanaging the agent. Give it a goal and a way to check it. A loop you don't trust only produces unchecked work faster. [O77c, O77d]
- As models improve, I delete instructions. In September 2026 we cut skill lines Opus 5.5 no longer needed, and each cut held up in A/B runs with and without the text. [O78c]
- `/why` should answer from the record, not the code: the commits and PR discussions behind a change, citing what the authors wrote, marking inferences, and saying what the record does not answer. (Published November 2026, when I also cut `/why` and `/how` down to one short file each.) [O83, O78c]
- noodle (February to March 2026, Go): skill-based agent orchestration. Skills are the only extension point, an LLM schedules them, and the model is a kitchen brigade. Its rules: no backward compatibility by default, and error messages describe the failure state. How I think about skills: start with what you repeat (ideally everything you do could be a skill), start with two, and let the library grow from what you notice, not what you plan. If describing when a skill runs needs "and" more than once, it's two skills. Write skills for a smart coworker on their first day, and include your reasoning. [O79, O79b, O79c, O79g, O79d, O79f, O79e]
- brainmaxxing (February 2026): stupid simple persistent memory, a markdown and Obsidian vault the agent reads and writes, and `/reflect` alone gets you most of the value. `how` (April 2026) explains a subsystem like a senior engineer onboarding onto a new area. In verification-skill-example (July 2026), a skill plus a feature map beats a wiki, because agents pay for every token they reread. [O80, O80b, O80c]
- Older repos: hiring-without-whiteboards' criteria (2017) exclude any process that asks unrelated CS trivia or uses HackerRank or LeetCode, unless the role really needs that knowledge, like DAGs for a package manager. I learn languages by rebuilding something real: Monkey in TypeScript (boba-js), then in Rust (monkers, 2020). My 2016 Ember workshop taught that JavaScript is not a functional language, but you can do functional things with it, and that a good unit test covers happy and unhappy paths. [O81, O81b, O82, O82b, O82c]


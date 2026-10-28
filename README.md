# A chatbot of your own with OpenCode

## Youth AI Lab — Erasmus+ project

- **Partners:** L.A.B. (Aix-en-Provence), UAB (Barcelona), Perlatecnica (Naples), Digitale Wolven
  (Antwerp), CSC Vent des Îles (La Rochelle)
- **Need help?**
  - Read the [Troubleshooting](#troubleshooting) section at the end of this guide.
  - Look at, or open, an [issue](https://github.com/Youth-AI-Lab/yal-opencode-guide/issues).
- **Working with young people?** Read
  [With young people: what this guide does not cover](#with-young-people-what-this-guide-does-not-cover)
  first.

> **A guide to follow on your own, in about one hour the first time.** You open a **GitHub
> Codespace** (a computer in your browser, with nothing to install) with **OpenCode**, a free and
> open-source AI assistant that works in a terminal. You connect the AI model you can pay for, or
> already pay for: an API key or a subscription. You meet a small ready-made chatbot, made of a few
> files, and you change each piece of it: its instructions, its documents, its skills and its
> tools. Then you make your own, for your topic or for a workshop you design. This setup is for
> you, the adult: for your own tests, **not for use with young people**.

This guide is for youth workers, facilitators and educators who work with young people (12 to 25).
It does not repeat the workshops of the Youth AI Lab project: the
[workshop kit](https://github.com/Youth-AI-Lab/yal-workshop-kit) shows, step by step, what each
piece adds to a chatbot. This guide shows how each piece is written in OpenCode, what OpenCode
does differently from Claude Code (the tool of the workshops), and how to reuse it for something
else.

---

## Goals

### What you will be able to do

| Part | You will be able to... |
|---|---|
| **1. Set up** | Open your Codespace, start the chatbot with the command `chatbot`, connect your key or subscription in OpenCode, choose a model, and ask a first question. |
| **2. OpenCode and Claude Code** | Say which file of the chatbot does what, what OpenCode sends to the model, and what it does differently from Claude Code. |
| **3. The instructions** | Change `AGENTS.md` and see the change at the next question. |
| **4. The knowledge** | Add a document to `knowledge/` and check that the chatbot finds it and names it. |
| **5. Skills** | Use the skill `quiz`, and write a skill of your own. |
| **6. Tools with MCP** | Fill in today's fire danger level and get it from a tool. |
| **7. Safety** | Say what the command `chatbot` checks before it starts OpenCode, what its refusals mean, and answer OpenCode's questions safely. |
| **8. Test and compare models** | Check your chatbot with four questions, try another model, and know what each one costs. |
| **9. Reuse it** | Copy the chatbot for another topic, and share it as a package with `chatbot export` and `chatbot import`. |

At the end, you will also know what each way of paying for the model costs and is for, where the
data goes, what the rules of a chatbot can and cannot guarantee, and why this setup is not for
young people.

### Why this approach?

**A chatbot is a few files.** The chatbot of this guide is a folder: a text of instructions, a few
documents, two skills, one small program that gives today's fire danger level, and one
configuration file that says what the chatbot may do. You can read each file, change it, copy the
folder and share it. This is what tools such as Claude Projects or Gemini Gems hide behind their
*Instructions* and *Knowledge* boxes.

**One tool, many models.** Claude Code, the tool of the workshops, works with Claude models. OpenCode
works with many providers: an Anthropic key, a free Gemini key, OpenRouter, and the subscriptions
some of you already pay for, such as GitHub Copilot or ChatGPT. The same folder works with all of
them, so you can compare models on the same questions.

**Safe by default, and checked before each start.** Out of the box, OpenCode is made to write code:
it reads, writes and runs commands without asking. The configuration of this guide turns it into a
chatbot: it reads its own documents, writes only in its folder of documents and asks you first,
and never runs a command. You start it with the command `chatbot`, which checks the folder first
and refuses to start OpenCode when a rule is missing or something could go around the rules.
[Part 7](#part-7---safety-what-the-chatbot-may-do) explains what it checks, and what the rules
cannot stop.

**Tested, with the limits we found.** Each part was tried with OpenCode 2.1.4 and four ways of
paying for the model, in October 2026. Where something did not work, or was not tested, this guide
says so.

### Is this guide for you?

**You took part in a Youth AI Lab workshop** and want to try the same pieces with another model, or
on your own topic: this guide is for you. In the workshops, the command `workshop` writes
OpenCode's configuration for you (`workshop-login --engine opencode` chooses OpenCode instead of
Claude Code). Here, you read and write that configuration yourself.

**You want to design your own workshop** on chatbots, with youth workers or other adults: this
guide gives you a folder to start from, and [part 9](#part-9---reuse-it-your-own-chatbot-or-workshop)
a checklist.

**You want a chatbot that the young people of your group use themselves**, on their phones: this
guide is not the right tool. OpenCode works in a terminal, for you. Use the
[Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide), which opens a chatbot to a
group during a session, and read
[With young people](#with-young-people-what-this-guide-does-not-cover) first.

### Prerequisites

You need a **GitHub account**, **one way to pay for the model** (see
[five ways to pay](#before-you-start-five-ways-to-pay-for-the-model)), and about **one hour**. No
technical knowledge is expected: every command to type is given.

**Are you ready?** You are if you can say, for one of your activities, which three or four
documents a chatbot should know, and what it should refuse to do.

---

## With young people: what this guide does not cover

Read this part **before** you show a chatbot to a group, even on a projector.

**By default, never use this setup with young people.** This guide is for you, the adult: to learn
how a chatbot is made, to test models and to prepare a workshop. It does not cover a chatbot that
young people use, or one you use in front of them with their questions. That needs a decision of
your organisation first (see below), and a tool made for it.

**Your own tests: invented questions only.** When you test, type questions you made up. Never a
real case, never the words of a young person, never a name, a school, a health detail or anything
else that could identify someone. Everything you type is sent to the company that runs the model,
and kept in your Codespace.

**For a chatbot that young people use**, use the
[Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide). It gives each participant
an account, shows a banner that reminds them not to write personal information, turns off the
features they do not need, and has templates: chatbot instructions with rules that protect the
group, and a notice for the participants. What this section says about your organisation's
decision applies there too.

### Before any use with a group: your organisation decides

A chatbot used with young people is your organisation's decision, not yours alone. Before any use,
ask whoever handles data protection in your organisation. A public body must have a data
protection officer; many small associations have none, and the organisation still decides
([GDPR article 37](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679)).
Your organisation then needs:

- **An account in its name.** The key belongs to the organisation and is paid by it, with its
  approval, not with your personal card. A personal subscription (Copilot, ChatGPT) is never for a
  group.
- **A processor contract** with the company that runs the model. Your organisation is the
  controller of the data: it needs a contract with the company that processes it
  ([GDPR article 28](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679)).
  For an Anthropic key, this is Anthropic's
  [data processing addendum](https://www.anthropic.com/legal/data-processing-addendum), part of its
  [Commercial Terms](https://www.anthropic.com/legal/commercial-terms) (see
  [where the data goes](#where-the-data-goes)).
- **Often, a data protection impact assessment.** A new AI tool used with young people will often
  need one first (article 35).
- **The right rule on consent.** The special consent rule for children (article 8) only covers
  online services offered directly to a child on the basis of consent. It is not the whole rule for
  young people's data: ask whoever handles data protection.

**Tell people they talk with an AI.** Since 2 August 2026, the EU AI Act requires that people who
talk with an AI system are told so at the latest at their first interaction, unless it is obvious
([article 50](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32024R1689)). Say it at
the start of each session, out loud and on the screen. Anthropic's rules ask the same.

**Anthropic's guidelines for minors.** Anthropic has
[guidelines for organisations whose users may be minors](https://support.claude.com/en/articles/9307344-responsible-use-of-anthropic-s-models-guidelines-for-organizations-serving-minors).
They ask organisations whose young users talk directly with the chatbot to add their own safety
measures (for example moderation and a way to report problems), to follow the laws on children's
safety and data, and to tell users that they talk with an AI.

### When a young person tells you something worrying

A young person may tell a chatbot, or tell you in front of it, that they are unwell, in danger, or
that someone hurts them. A chatbot cannot handle this, and must not try:

- **The chatbot** must answer kindly, tell them to talk **now** to the youth worker or another adult
  they trust, and to call 112 if they are in danger right now. It asks for no details. The
  instructions of this guide say so (the last rule of `chatbot/AGENTS.md`, [part 3](#part-3---the-instructions-agentsmd)),
  and [part 8](#part-8---test-and-compare-models) tests it. Keep this rule in every chatbot you make.
- **You** follow your organisation's safeguarding procedure: who to tell, and how fast. Know it
  before the session.
- **Never promise to keep a secret**, and never let the chatbot promise it. Say that you will only
  tell the people who must know to protect them.

### Where the data goes

Each question, with your instructions and the passages of documents the chatbot opens, is sent to
the company that runs the model. Your conversations are also kept in the Codespace
(`~/.local/share/opencode/`), a GitHub service. What each company says, checked in October 2026
(read the pages again, they change):

- **Anthropic key** ([way 1](#way-1---an-anthropic-api-key)). For use through an API key, Anthropic
  says that it
  [deletes this data within 30 days](https://privacy.claude.com/en/articles/7996866-how-long-do-you-store-my-organization-s-data),
  with exceptions (content flagged for breaking its rules is kept up to 2 years), that it
  [does not use it to train its models](https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training),
  and that it
  [stores it in the United States](https://privacy.claude.com/en/articles/7996890-where-are-your-servers-located-do-you-host-your-models-on-eu-servers).
  The contract is with Anthropic Ireland. It includes a
  [data processing addendum](https://www.anthropic.com/legal/data-processing-addendum) where your
  organisation is the controller and Anthropic the processor. That addendum lists no sensitive data
  (health, religion, sexuality…): never send any. Anthropic offers no processing limited to the EU
  for the API.
- **Gemini key** ([way 2](#way-2---a-google-gemini-api-key-ai-studio)). Google's terms reserve AI
  Studio and the Gemini API for "professional or business purposes, not for consumer use", and
  forbid any service "likely to be accessed by individuals under the age of 18". In the EEA,
  Switzerland and the UK, the paid-tier data rules also apply to the free tier: Google is then a
  processor under its [processor terms](https://business.safety.google/processorterms/).
- **OpenRouter key** ([way 3](#way-3---an-openrouter-key)). The account holder must be 18 or older,
  and the terms of each model apply. If you act for an organisation, OpenRouter's
  [data processing agreement](https://openrouter.ai/data-processing-agreement) applies. In your
  privacy settings, refuse the providers that train, or allow only zero-data-retention providers:
  OpenRouter then never routes to the others, including when it falls back to another provider.
  OpenRouter does not guarantee what each provider does. Keeping questions in the EU needs a
  Business or Enterprise plan. Never send health or other sensitive data.
- **Copilot and ChatGPT subscriptions** ([way 4](#way-4---a-github-copilot-subscription),
  [way 5](#way-5---a-chatgpt-plus-or-pro-subscription)). Personal plans, for your own tests only:
  turn off the use of your data for training first, as each way explains.

**The Codespace region** (set in [your GitHub account](#your-github-account)) keeps your Codespace,
and the conversations OpenCode saves in it, in Europe. It does not change where your questions go:
each one is sent to the company that runs the model.

**If the questions must stay in the EU**, you need a provider with EU processing and a contract in
your organisation's name, set up by someone who manages a cloud account: Mistral (hosted in the EU
by default), Amazon Bedrock with an EU profile (`eu.anthropic.claude-sonnet-5-5`), Azure with an EU
Data Zone deployment, or Google Cloud with the `eu` location. OpenCode 2.1.4 lists all four. TO BE
COMPLETED: not yet tested with this guide. Mistral's terms also restrict children's data and ask
for parental consent for minors: read them before you propose it for a group.

---

## Before you start: five ways to pay for the model

Do this part **on your own, never with your screen projected**: you will see your key or sign in to
your accounts.

The chatbot sends each question to an AI model run by a company. Someone pays for it. There are
five ways:

| Way | What you need | What it costs | What it gives | What it is for |
|---|---|---|---|---|
| **1. Anthropic API key** | an account on the Claude Console, with credits | pay per question, with a spending limit you set | Claude models, including Claude Sonnet 5.5, the model of the workshops | your own tests; a group only with a key of your organisation, after its decision |
| **2. Google Gemini API key** | a Google account, adult | a free tier with daily limits, or a paid tier | Gemini models | your own tests, for your work; a group only with a paid key of your organisation, after its decision, and never young people (see way 2) |
| **3. OpenRouter key** | an account, adult, with credits | pay per question, plus a fee on credits; some free models | hundreds of models from many companies | your own tests, to compare models; not for a group |
| **4. GitHub Copilot subscription** | a paid Copilot plan (Pro, Pro+, Business or Enterprise) | included in your plan | the models of your plan, including Claude Sonnet 5.5 | your own tests only |
| **5. ChatGPT Plus or Pro subscription** | a ChatGPT account with this plan | included in your plan | OpenAI models | your own tests only |

**Your own tests means invented questions.** Never a real case, never the words of a young person,
whatever the way (see [With young people](#with-young-people-what-this-guide-does-not-cover)).

**A personal subscription is for you.** Copilot and ChatGPT plans are paid by you, for you, and
your login is for one person. Never share them with a group, and never use them for a chatbot that
young people use. For a workshop with adults, give each pair a key with a spending limit (way 1).

**A Claude Pro or Max subscription does not work here:** Anthropic's
[terms](https://code.claude.com/docs/en/legal-and-compliance) forbid using these plans in other
tools, and OpenCode removed this option. For Claude models, you need an Anthropic API key (way 1),
or a Copilot plan (way 4).

**A local model works too.** OpenCode can use a model that runs on your own computer, for example
with Ollama, without sending anything to a company. A Codespace is too small for that. The coming
Youth AI Lab guide on local AI explains how (TO BE COMPLETED: link to the local AI guide).

You need only **one** of these five ways to follow the guide. With two, you can compare them in
[part 8](#part-8---test-and-compare-models).

### Your GitHub account

If you already have a GitHub account, skip this. Otherwise, go to <https://github.com/signup>,
enter your e-mail address, a password and a user name, and confirm your address with the code
GitHub sends you.

Then set the **idle timeout** of your Codespaces to its maximum: click your picture (top right) →
**Settings** → **Codespaces** → **Default idle timeout** → 240 minutes → **Save**. This setting
only works for Codespaces created after it: do it **now**. On the same page, under **Region**,
choose **Set manually**, then a region in Europe in the list, and save. This keeps your Codespace,
and the conversations OpenCode saves in it, in Europe. It does not change where your questions go:
each one is sent to the company that runs the model.

### Way 1 - An Anthropic API key

This is the way of the workshops. The key pays for each question, and a spending limit protects
you. On <https://platform.claude.com>:

1. Create an account, then add a payment method and buy a small amount of credits
   (**Spending** → **Billing & payments**). Without credits, the key does not work.
2. Create a **workspace** for your tests: **Settings** → **Workspaces** → **Create workspace**.
3. Give this workspace a **spending limit**: **Spending** → **Spend limits**; under **Workspace
   limits**, choose your workspace, then **Set limit**.
4. Create a key: **Keys & access** → **API keys** → **Create key**. Give it a **Name**, an
   **Expires** date, and choose your workspace in **Scope**. Click **Create key**.

The key starts with `sk-ant-`. It is shown **only once**: copy it into your password manager right
away. You need your own workspace, because the workspace **Default** cannot have a spending limit.
In OpenCode, the provider is **Anthropic** and the model of the workshops is **Claude Sonnet 5.5**.

An account you create for your own tests is yours. For a workshop or a group, the account and the
key belong to your organisation, created with its approval
([With young people](#before-any-use-with-a-group-your-organisation-decides)).

### Way 2 - A Google Gemini API key (AI Studio)

Google AI Studio gives a key with a **free tier**: good to learn and to prepare a workshop, at no
cost. Read its conditions first:

- **Age.** Google's [terms](https://ai.google.dev/gemini-api/terms) say: "You must be 18 years of
  age or older to use the APIs. You also will not use the Services as part of a website,
  application, or other service (collectively, "API Clients") that is directed towards or is
  likely to be accessed by individuals under the age of 18." This is true for the free tier and the
  paid tier: **never use a Gemini key for a chatbot that young people under 18 may use.**
- **For your work only.** The same terms reserve the APIs "for professional or business purposes,
  not for consumer use".
- **Your data, free tier.** The terms say that on the free tier, Google uses what you send "to
  provide, improve, and develop Google products", that "human reviewers may read, annotate, and
  process your API input and output", and: "Do not submit sensitive, confidential, or personal
  information to the Unpaid Services." For users in the European Economic Area, Switzerland and the
  United Kingdom, the terms apply the data rules of the paid services to free use too: Google is
  then a processor under its [processor terms](https://business.safety.google/processorterms/). The
  [pricing page](https://ai.google.dev/gemini-api/docs/pricing) still marks the free tier "Used to
  improve our products". Either way, send nothing personal.
- **Opening a chatbot to others.** The terms say: "You may use only Paid Services when making API
  Clients available to users in the European Economic Area, Switzerland, or the United Kingdom."

To get the key:

1. Open <https://aistudio.google.com/apikey> and sign in with your Google account. After you
   accept the terms, AI Studio creates a Google Cloud project and a first API key for you.
2. To make another key, on the page **API Keys**, click **Create API key**.
3. Google refuses the requests of a key that is unrestricted: open your key, choose
   **Add restrictions**, then **Restrict to Gemini API only**.

New keys start with `AQ.` (older ones started with `AIza`). Copy the key into your password
manager. The limits of the free tier are not published as figures: AI Studio shows the limits of
your project, which reset each day at midnight Pacific time
([rate limits](https://ai.google.dev/gemini-api/docs/rate-limits)). To use the paid tier, link a
billing account in AI Studio and prepay a minimum of $5; you can then set a **Monthly spend cap**
([billing](https://ai.google.dev/gemini-api/docs/billing)).

In OpenCode, the provider is **Google**. Use **Gemini 3.8 Flash**, and keep **Gemini 3.5 Flash Lite**
as a fallback when it is overloaded ([part 8](#part-8---test-and-compare-models)). Avoid the 2.5
models: Google keeps them for projects that used them before.

> [!NOTE]
> A Google Workspace for Education account of someone under 18 cannot use AI Studio, and the
> administrator of a Workspace can turn AI Studio off.

### Way 3 - An OpenRouter key

[OpenRouter](https://openrouter.ai) gives one key for hundreds of models from many companies:
handy to compare them. Its [terms](https://openrouter.ai/terms) say: "You must be at least 18
years of age to use the Service", and the terms of each model apply on top of OpenRouter's.

1. Create an account on <https://openrouter.ai>, and buy credits on the page **Credits**. A fee of
   5.5 % is added when you buy credits ([pricing](https://openrouter.ai/pricing)); the prices per
   model have no markup.
2. Create a key (**Create API Key**). In the key's dialog, under **Key limit**, set a **Credit
   limit** and how often it resets: this is your spending limit.
3. In your [privacy settings](https://openrouter.ai/settings/privacy), refuse the providers that may
   train on your data, or allow only zero-data-retention providers. There are separate settings
   for paid and free models. OpenRouter then never routes your questions to the other providers,
   even when it falls back to another provider because the first one fails. OpenRouter does not
   guarantee what each provider does.

If you test for your organisation, OpenRouter's
[data processing agreement](https://openrouter.ai/data-processing-agreement) applies. Keeping your
questions in the EU needs a Business or Enterprise plan.

The key starts with `sk-or-`. **The free models** (their name ends with `:free`) are limited to 50
requests a day while you have bought less than 10 credits
([limits](https://openrouter.ai/docs/api_reference/limits)), and each one has its own data policy,
shown on its page: some keep your prompts, some train on them. Do not send anything personal to
them.

> [!NOTE]
> OpenRouter was checked with test keys only: the way OpenCode talks to it was verified, but not
> yet a real conversation. Tell us in an [issue](https://github.com/Youth-AI-Lab/yal-opencode-guide/issues)
> if it works for you.

### Way 4 - A GitHub Copilot subscription

If your GitHub account has a paid Copilot plan, OpenCode can use the models of your plan: GitHub
[officially supports](https://github.blog/changelog/2026-01-16-github-copilot-now-supports-opencode/)
the Pro, Pro+, Business and Enterprise plans in OpenCode. Copilot Free is not in that list: TO BE
COMPLETED (not tested). You sign in from OpenCode in [part 1](#part-1---set-up): in our test in a
Codespace, this took a link that opened and a code of 8 characters to type.

**Turn off training first.** With a personal plan (Free, Pro, Pro+), GitHub may use what you send to
train its models unless you opt out in your GitHub settings
([terms, section J](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)):
opt out before your first test. Business and Enterprise plans fall under your organisation's
agreement with GitHub.

**Only the models of your plan.** OpenCode's catalogue lists 28 Copilot models, but an account sees
only those of its plan: 14 for the account we tested, among them Claude Sonnet 5.5, the model of the
workshops. A model outside your plan fails at once with "Model unavailable". Always choose in
`/models`, which shows only yours.

**Free for teachers.** GitHub gives Copilot Pro for free to
[verified teachers on GitHub Education](https://docs.github.com/en/copilot/how-tos/manage-your-account/get-free-access-to-copilot-pro).
Whether a youth worker can be verified as a teacher is TO BE COMPLETED.

This is a **personal** subscription: for your own tests only, and your login is for you only.

### Way 5 - A ChatGPT Plus or Pro subscription

OpenCode can use a ChatGPT Plus or Pro plan instead of an OpenAI API key: in a Codespace, you sign
in once, from the terminal (below). Its use counts against your plan, so OpenCode shows no cost
([OpenCode's documentation](https://opencode.ai/v2/docs/providers/)). OpenAI lists OpenCode among
the apps that can use a ChatGPT plan
([Sign in with ChatGPT](https://learn.chatgpt.com/docs/sign-in-with-chatgpt)). In our tests, these
models answered well but more slowly (12 to 19 seconds).

**Turn off training first.** Plus and Pro are consumer plans: OpenAI may use your content to train
its models unless you turn off **Improve the model for everyone** in **Settings → Data controls**.
Turn it off before you connect OpenCode.

**In a Codespace, sign in from the terminal, not from OpenCode's window.** Inside OpenCode, the
sign-in can neither open your browser nor copy its address. At the end, ChatGPT also sends your
browser back to an address that starts with `http://127.0.0.1:`: your browser looks for it on
your own computer, while OpenCode waits for it in the Codespace. This worked in our test:

1. Quit OpenCode (`Ctrl+C`). In the terminal, in the folder `chatbot/` of this guide (a new
   terminal opens there), type `opencode auth login openai` and choose **Sign in with ChatGPT**.
2. Hold `Ctrl` and click the address that it prints (`Cmd`+click on a Mac): it opens in your
   browser. Sign in to ChatGPT and allow the access.
3. The last page does not load. **At once**, copy the whole address from the address bar of your
   browser, and open a second terminal (the **+** of the terminal panel). Type the line below,
   and paste the address between the two quotes with `Ctrl+Shift+V` (`Cmd+V` on a Mac); the
   quotes keep the address in one piece. Press Enter. Paste this address nowhere else: it holds a
   sign-in code.

   ```bash
   curl "PASTE-THE-ADDRESS-HERE"
   ```

4. The first terminal shows "Connected to OpenAI" and "Done". If it says "Authorization expired",
   you were too slow: start again at step 1.

Then start the chatbot with `chatbot`, and go on with [step 4](#step-4---choose-the-model): choose a
model of OpenAI with `/models` (in our test, GPT-6.1 Sol answered in about 5 seconds).

This is a **personal** subscription: for your own tests only, and your login is for you only.

---

## Part 1 - Set up

Setting up takes five steps: open your Codespace, start the chatbot, connect your key or
subscription, choose a model, and ask a first question.

### Step 1 - Open your Codespace

1. The first time only, open <https://codespaces.new/Youth-AI-Lab/yal-opencode-guide> and click
   **Create codespace**. GitHub prepares the environment and opens **VS Code** in your browser:
   count a few minutes.
2. At the bottom of the window is the **terminal**, where you type commands. Its prompt shows the
   folder `chatbot`: each new terminal opens in the folder of the chatbot.

Each new terminal greets you with "Welcome! Start the chatbot of this guide with: chatbot": step 2
does it.

> [!WARNING]
> **The next times, do not use this link again**: it would create a new Codespace, without your
> changes. Go to <https://github.com/codespaces> and click the **name** of your Codespace: it
> reopens in about a minute.

### Step 2 - Start the chatbot

You always start the chatbot with the command `chatbot`, never with `opencode` alone: `chatbot`
first checks the folder of the chatbot, then starts OpenCode in it.

1. Make the terminal bigger first: click the **Maximize Panel Size** arrow at the top right of the
   terminal. OpenCode needs room: in a small terminal, its side panel covers the conversation.
2. In the terminal, type:

   ```bash
   chatbot
   ```

**What you should see.** The command prints:

```
All checks passed. Starting OpenCode in chatbot/ (the current folder).
Before your first question, type /mcps and wait until it shows "fire-danger Connected".
```

Then OpenCode opens in the terminal. At the bottom are the message box and a line that starts with
**Chatbot**: this is the assistant of this folder. If you see **Build** instead, OpenCode did not
load the configuration of the chatbot: quit at once with `Ctrl+C`, and see
[OpenCode is not the chatbot](#opencode-is-not-the-chatbot).

After **Chatbot**, the line shows a model. Before you connect anything (step 3), it may be a GitHub
Copilot model chosen by OpenCode, for example **Gemini 4 Argon · GitHub Copilot**. Do not ask
anything yet: in our test, this one answered "Error: The requested model is not supported."
Connect your key or subscription first, so that you know who pays and on which terms.

If the command prints a list of problems and "This chatbot is not safe to start. Fix it, or ask the
person who sent it.", OpenCode does not start: each line says what is wrong.
[Part 7](#when-chatbot-refuses-to-start) explains these messages. On a new Codespace of this guide,
you should not see it.

The grey example text in the message box, such as "Fix broken tests" or "What is the tech stack of
this project?", is OpenCode's own, made for programmers: ignore it.

![OpenCode just after it opens in the chatbot folder: the OpenCode logo, the message box, and the bottom line "Chatbot · Claude Sonnet 5.5 · Anthropic"](images/01-welcome.png)

### Step 3 - Connect your key or subscription

In the message box, type `/connect` and press Enter. OpenCode lists the providers. Choose yours,
then follow what it asks:

![The list that `/connect` opens, "Connect an integration": OpenAI, GitHub Copilot, Anthropic, Google and more](images/04-connect.png)

| Your way | Choose | Then |
|---|---|---|
| **Anthropic key** | **Anthropic**, then the API key method | paste your key with `Ctrl+Shift+V` (`Cmd+V` on a Mac) and press Enter |
| **Gemini key** | **Google**, then the API key method | paste your key and press Enter |
| **OpenRouter key** | **OpenRouter**, then the API key method | paste your key and press Enter |
| **GitHub Copilot** | **GitHub Copilot** → **Login with GitHub Copilot** → **GitHub.com** | OpenCode gives the page <https://github.com/login/device> (in our test in a Codespace, the link opened) and a code of 8 characters: type the code on that page, and allow the access (copying it out of OpenCode may not reach your browser) |
| **ChatGPT Plus or Pro** | in a Codespace, not here: quit OpenCode and follow [way 5](#way-5---a-chatgpt-plus-or-pro-subscription) | sign in from the terminal with `opencode auth login openai` |

Once connected, OpenCode shows the models of this provider: go to step 4. For ChatGPT, start the
chatbot again with `chatbot` after way 5, then go to step 4.

**Where your key goes.** OpenCode keeps it in its own database in your home folder
(`~/.local/share/opencode/`), with your conversations: never in the folder of the chatbot, so you
can share the folder without sharing your key. You connect once per Codespace.

> [!TIP]
> In the terminal, paste with `Ctrl+Shift+V` (`Cmd+V` on a Mac). The first time, the browser may
> ask for permission to paste: click **Allow**. Copying text out of OpenCode's window does not work
> well in the browser ([part 4](#add-a-document-with-the-skill-source-note)).

### Step 4 - Choose the model

Choose a model in this list (later, type `/models` and press Enter to open it again: it lists the
models of all the providers you connected), for example **Claude Sonnet 5.5** (Anthropic or GitHub Copilot), **Gemini 3.8 Flash**
(Google) or **GPT-6 Sol** (OpenAI). The bottom of the window now shows the chatbot, the model and
its provider, for example **Chatbot · Claude Sonnet 5.5 · Anthropic**. OpenCode keeps this choice:
at the next start, the bottom line shows the last model you used. Check it before each session.

![The list that `/models` opens, "Select model", with Claude Haiku, Sonnet and Opus highlighted](images/03-model-picker.png)

In a Codespace, `/models` may list **GitHub Copilot** models even before you connect anything: they
come from the Codespace's own access to GitHub. In our test, with an account that has a Copilot
plan, some answered (Grok 4.7) and others did not ("Error: The requested model is not
supported.": Gemini 4 Argon, GPT-6 Sol). We did not check which plan or quota they use. To use
Copilot, connect your account with `/connect` as in step 3.

### Step 5 - Wait for the tools, then ask

OpenCode starts the chatbot's tool, the small program of the folder `mcp/`, a few seconds after it
opens. Type `/mcps` and press Enter: wait until the list shows **fire-danger Connected**, then
press `Esc`. A question sent before that goes without the tool. Once a conversation has started,
the side panel on the right shows the same line (in a small terminal, `Ctrl+X` then `B` shows or
hides the panel).

![The side panel on the right showing "fire-danger  Connected", after a first greeting](images/02-fire-danger-connected.png)

Then ask:

```
Hello, who are you?
```

The chatbot should present itself as the **Wildfire Helper** of a youth group in La Rochelle.
Then ask a real question:

```
In which sector is La Rochelle, and from what time is the level of the day shown?
```

**What you should see.** Above the answer, OpenCode shows what the chatbot did: in our test, the
line "→ Explored: 1 read, 1 search" (its readings and searches in its documents), and sometimes
a call to its tool. The answer says **sector 1 (1701)** and
**6 pm the day before**, and names the document `knowledge/30-charente-maritime-vigilance-levels.md`.
In the side panel, the **context** counter shows how many tokens (pieces of words) were sent to the
model, and how much it cost.

To stop an answer, press `Esc`. To start a new conversation, type `/new`. To quit OpenCode, press
`Ctrl+C`. In a small terminal, the side panel covers the conversation: then `Esc` and `Ctrl+C`
first close the side panel, and you press them a second time.

### Free quota

A free GitHub account has, each month, 120 hours of computing and 15 GB of storage for Codespaces.
On the 2-core machine of this guide, one hour of use counts as two, which leaves **about 60 hours a
month** ([GitHub's documentation](https://docs.github.com/en/billing/concepts/product-billing/github-codespaces)).
Stop your Codespace after use: on <https://github.com/codespaces>, its **…** menu → **Stop
codespace**. GitHub deletes a Codespace that stayed stopped for 30 days.

---

## Part 2 - What OpenCode does, compared with Claude Code

### The folder of a chatbot

```
chatbot/
├── opencode.jsonc        what OpenCode loads, and what the chatbot may do (part 7)
├── AGENTS.md             the instructions, sent before every conversation (part 3)
├── knowledge/            the documents, and index.md, their list (part 4)
├── .opencode/skills/     the skills: quiz and source-note (part 5)
├── mcp/                  a small program that gives today's fire danger level (part 6)
└── .ignore               files that OpenCode's search skips (part 7)
```

The folders whose name starts with a dot (`.opencode/`) may be hidden in some file lists; VS Code
shows them. Around `chatbot/` is this guide: its README is **not** a document of the chatbot. The
configuration keeps the chatbot from opening it; a search on it is still possible, and it holds
nothing secret. The guide also holds the command `chatbot` (the file `bin/chatbot`), which checks a
chatbot folder before it starts OpenCode (part 7).

The documents and the tool are elements of the workshop kit: the summaries 30 to 32 on the fire
rules of Charente-Maritime (checked by a person), the `fire-danger` tool, and the skill
`source-note`, adapted. They are here to check that each piece works.

### What is sent at each question

```mermaid
flowchart LR
    Q["Your question"] --> M
    subgraph S["Sent to the model each time"]
        P["OpenCode's own prompt"]
        A["AGENTS.md"]
        K["the list of skills and tools"]
    end
    S --> M["The model<br/>(Claude, Gemini, GPT...)"]
    M -- "search, read, skill, tool" --> F[("chatbot/<br/>documents, skills, mcp")]
    F -- "what it found" --> M
    M --> R["Answer, with its sources"]
```

At each question, OpenCode sends the model: its own prompt, the list of skills and tools, your
instructions (`AGENTS.md`), the date and the folder, then the conversation. The documents are sent
only when the chatbot opens them: as its instructions say, it **reads** the list of your documents
(`knowledge/index.md`) first, **searches** (a word in all the files), then **reads** the ones it
needs. Each search and each reading is a step; the chatbot may take at most 15 steps per question.

### OpenCode and Claude Code

Both tools work the same way: a model, instructions, tools to search and read, skills, and MCP
tools. What differs is how you write each piece, and what happens by default.

| | Claude Code (the workshops) | OpenCode (this guide) |
|---|---|---|
| **Who makes it** | Anthropic | the OpenCode project, open source ([code](https://github.com/anomalyco/opencode)) |
| **Models** | Claude | many providers: Anthropic, Google, OpenRouter, GitHub Copilot, OpenAI, local models |
| **Its own prompt** | Claude Code's | "an AI agent running in OpenCode, a coding agent harness": made for programming |
| **Instructions** | `CLAUDE.md` (in the kit, it imports `AGENTS.md`); notes between `<!--` and `-->` are removed | `AGENTS.md`, read directly; **notes between `<!--` and `-->` are sent too**; a change counts from the next question |
| **Searching the documents** | through terminal commands, in the workshops | its own tools: `grep` (search), `glob` (list), `read` |
| **Skills** | `.claude/skills/` | `.opencode/skills/` (it also reads `.claude/skills/` and `.agents/skills/`) |
| **MCP tools** | `.mcp.json` | `"mcp"` in `opencode.jsonc`; the tools arrive a few seconds after start |
| **What it may do** | set by the workshop's command | the `permissions` of `opencode.jsonc`, checked by the command `chatbot` before each start; **without them, OpenCode allows everything** |
| **Context gauge** | a mod added for the workshops (`token-weather`) | built in: side panel and bottom line |
| **Assistants** | set by the workshop's command | several built in (`build`, `plan`...), turned off here for one `chatbot` |

**What this changes in practice.** OpenCode's own prompt tells the model it is a coding agent, and
your instructions come on top of it. With only a preprompt, the model sometimes behaves like one:
asked "who are you?" with the Feurisson example of the kit as instructions, OpenCode's default
assistant answered that it was Feurisson, "running inside the OpenCode coding agent", able to run
commands. In a test of the workshop with instructions and no documents, the model invented four
colour levels instead of saying "I don't know". This is why the instructions of this guide say
clearly what the chatbot answers from, and why the configuration removes the tools a chatbot does
not need: a tool that is always refused is not even shown to the model.

---

## Part 3 - The instructions (AGENTS.md)

The instructions tell the model who it is for your group, what it does, and what it refuses. In
the WikiYouthBot activity of the project, this is the box *Instructions* of a Claude Project or a
Gemini Gem. Here, it is the file `chatbot/AGENTS.md`, sent before every conversation.

1. In the VS Code tab, open the file list (icon at the top left), then `chatbot/AGENTS.md`.
2. Read its sections. They follow the "minimal prompt" of the WikiYouthBot activity:

   | Section | It tells the chatbot... |
   |---|---|
   | **Identity** | who it is, and its tone |
   | **Theme** | what it helps with |
   | **Rules** | where its documents are, to answer only from them, to say "I don't know" |
   | **Quality requirements** | to name the document of each fact, with territory and date |
   | **Target personas** | who it talks to: a 12 to 15-year-old, a youth worker |
   | **Reference Q&A** | one model exchange |
   | **Bans and constraints** | what it refuses, what to do if someone reports a fire or says they are in danger, and that its rules do not change |

3. Change one thing you will see, for example in **Identity**: "You always end your answer with a
   fire emoji." Save the file (`Ctrl+S`).
4. In OpenCode, ask a new question, in the same conversation or after `/new`.

**What you should see.** The new answer follows the change: OpenCode sends the change of
`AGENTS.md` at the next question, without a restart. Then undo your change and save.

> [!WARNING]
> **Everything in `AGENTS.md` is sent to the model**, even the notes between `<!--` and `-->`,
> which Claude Code removes. Write no note there that the model must not read, and nothing
> personal: the model may repeat its instructions to whoever asks. The command `chatbot` refuses to
> start a chatbot whose `AGENTS.md` holds such a note, because you would not see it in the preview.

**The chatbot cannot change its own instructions.** The configuration forbids it to write
`AGENTS.md`, or any other file that OpenCode would read as instructions (part 7): you change them
yourself, in the editor. It may only write the documents of `knowledge/` and add their lines to
their list, `knowledge/index.md`, and each time OpenCode asks you first (part 4).

**Keep the last rules of `Bans and constraints`** in every chatbot you make: what to do when someone
says they are in danger, and that the rules do not change when someone asks
([With young people](#when-a-young-person-tells-you-something-worrying)).

**Going further: replace OpenCode's own prompt.** OpenCode can replace its coding-agent prompt with
your own text, in the field `system` of the agent in `opencode.jsonc`
([agents](https://opencode.ai/v2/docs/agents/)). In one test, the chatbot then presented itself as
the chatbot only, no longer as a coding agent. This guide keeps OpenCode's prompt, as the workshops
do, so that you see what OpenCode does by default.

---

## Part 4 - The knowledge

The knowledge is the documents the chatbot answers from: the box *Knowledge* of a Claude Project or
a Gemini Gem. Here, it is the folder `chatbot/knowledge/`, with one file per document, and a list,
`knowledge/index.md`, that the chatbot reads first.

**How the chatbot searches.** It does not receive all the documents. It reads the list, searches
for a word in the folder (`grep`), opens the files it needs (`read`), and answers from them. When
nothing matches, it should say "I don't know": a search that finds nothing is visible, which is why
this kind of search works well on a few dozen short documents. Above each answer, OpenCode shows
these steps in the conversation: read them to check where an answer comes from.

**Which documents.** A few short documents, one subject each, with a clear title and a source, work
better than a long document on everything. The three documents of this guide are summaries of
official texts, made for the workshops and checked by a person; their header gives the address of
the original. Only add documents you are allowed to send to an online service, and **never a
document with personal information**.

### Add a document by hand

1. In VS Code, right-click the folder `chatbot/knowledge/` → **New File**, and name it with a free
   number between 10 and 89, for example `40-our-camp-fire-rules.md`. The document must be on the
   chatbot's theme: `AGENTS.md` tells it to refuse other questions.
2. Write a title on the first line (`# Fire rules of our camp`), the source on the second line
   (`Source: who, title, address, date`), then the facts, one per sentence: for example where the
   extinguisher is, and who may light the barbecue. Save.
3. Add it to the list of documents, `knowledge/index.md`. You do not need to write the line: in
   OpenCode, ask "Add knowledge/40-our-camp-fire-rules.md to the list of documents." OpenCode asks
   you before the chatbot changes the list: check that it adds only one line, ending with "Not yet
   checked by a person." until someone else has checked your document, then choose **Allow once**.
4. In OpenCode, type `/new`, then ask a question whose answer is only in your document.

**What you should see.** The chatbot searches, opens your document, and names it in the answer.
If it does not find it, check the words of your question against the words of the document. If it
refuses kindly, your question or your document is outside its theme: change the theme in
`AGENTS.md` (part 3), or ask a question on wildfire prevention.

### Add a document with the skill `source-note`

You can also tell the chatbot what you know, and let it write the document:

1. Ask: "Add this to the knowledge: in our club, campfires are never allowed. Source: rules of the
   youth club, 2026."
2. The chatbot uses the skill `source-note` and writes the document. Before it writes, OpenCode
   **asks you** first. Read what it wants to write, then choose **Allow once**, or **Reject**
   (never **Always allow**: [part 7](#when-opencode-asks-you) says why).
3. The chatbot then adds a line for the document at the end of `knowledge/index.md`, the list of
   documents. OpenCode **asks you** again: check that it adds only this line, then choose **Allow
   once**. The window may show the first lines of the list first: the new line is at the end,
   lower down in the window.
4. Read the document it wrote, and check each sentence against your source.

![OpenCode asking before it writes a document: "Permission required → Edit knowledge/40-...md", the text it would write, and the choices Allow once / Always allow / Reject](images/06-permission-ask.png)

The skill never invents a source: without one, it writes `Source: TO BE COMPLETED` and tells you.
Its line in `knowledge/index.md` ends with "Not yet checked by a person.". Once you have checked
the document, replace these words with "Checked by a person.", as on the lines of the documents
30 to 32.

> [!TIP]
> Do not try to copy text from the window of OpenCode: in the browser, it does not reach your
> clipboard, and `Ctrl+V` then pastes whatever was there before (in a Markdown file, VS Code even
> saves a copied image as a new file of the folder). Ask the chatbot to make the change instead, or
> type it in the editor.

---

## Part 5 - Skills

A skill is a short procedure that the chatbot follows when the request matches its description:
make a quiz, write a document. Its description is sent at each question; the rest of the skill is
read only when it is used. Here, the skills are in `chatbot/.opencode/skills/`, one folder per
skill, each with a file `SKILL.md`.

### Use the skill `quiz`

1. In OpenCode, ask: "Make a quiz of 3 questions for my group."
2. In the conversation, OpenCode shows that the chatbot loaded the skill `quiz`, then read the
   documents.

**What you should see.** Three questions for 12 to 15-year-olds, each with three possible answers,
then the answers, each with one sentence of explanation and the name of its document. In our tests,
the five models that answered all used the skill when asked for a quiz.

### Write your own skill

1. In VS Code, right-click `chatbot/.opencode/skills/` → **New Folder**, and name it with a short id
   in small letters and dashes, for example `talk-plan`. The folder name is the skill's id.
2. In this folder, create a file `SKILL.md`, and start from this template:

   ```markdown
   ---
   name: talk-plan
   description: Writes the plan of a 5-minute talk on the theme, for a young person, from the documents of knowledge/. Use when the user asks for a talk, a presentation or a speech.
   ---

   # The plan of a talk

   ## Steps

   1. Read `knowledge/index.md`, then the documents you need.
   2. Write a plan in three parts, each with one idea and the document it comes from.
   3. End with one question to ask the audience.

   ## What you don't do

   - Add a fact that is not in the documents.
   ```

3. Save, then in OpenCode type `/new` and ask: "Help me prepare a talk on sky lanterns."

The **description** decides when the skill is used: say what it does and when to use it. A skill
without a description is never offered to the model. The chatbot cannot change its skills: you
write them yourself. Write no note between `<!--` and `-->` in a skill: the command `chatbot`
refuses it, as in `AGENTS.md`.

> [!TIP]
> The skills of the workshop kit work here, if they speak of folders this chatbot has:
> `source-note` was adapted from the kit's, which writes in `summaries/`. Copy a skill of the kit
> into `.opencode/skills/`, one folder per skill. OpenCode would also read `.claude/skills/` and
> `.agents/skills/`, but the command `chatbot` refuses these folders: a chatbot keeps its skills in
> one place, the one it checks.

---

## Part 6 - Tools with MCP

Some knowledge changes every day, such as today's fire danger level: no document can hold it, and
the model cannot know it. An **MCP tool** is a small program that the chatbot can call to get it.
MCP (Model Context Protocol) is a common way to connect such tools to many AI applications.

### The fire-danger example

The tool of this guide, `chatbot/mcp/fire_danger_server.py`, comes from the workshop kit. It gives
the chatbot two tools: `territories` (the list of territories) and `fire_danger` (today's level for
one territory, with its scale, its official source and advice). It reads the file
`chatbot/mcp/fire-danger.json`, where a person writes the level of the day, copied from the
official source. OpenCode starts the program itself, from the `"mcp"` part of `opencode.jsonc`.

1. Check that `/mcps`, or the side panel, shows **fire-danger Connected** (part 1, step 5).
2. Ask: "What is today's fire danger level in La Rochelle?"

**What you should see.** The chatbot calls the tool, without asking you: the configuration allows
these tools, which only read a file. The level says "TO BE COMPLETED", so the chatbot says that
nobody has filled in today's level, and gives the official source. It does not guess.

### Fill in today's level

1. Open the official source of your territory, given in `chatbot/mcp/fire-danger.json` (for La
   Rochelle, <https://www.risque-prevention-incendie.fr/17>).
2. In `fire-danger.json`, write the date of today in `"date"`, in the form year-month-day, then,
   for your territory, replace the text of `"level"` with the level of the day and the lines of
   `"advice"` with the advice of the source, copied as they are. Keep the quotes: each line between
   quotes, a comma between two lines, and none after the last. For La Rochelle, it looks like this
   (with the real level and advice of the day instead of the words in capitals):

   ```json
   "date": "2026-10-27",
   ```

   ```json
   "level": "TO BE COMPLETED",
   ```

   ```json
   "advice": [
     "FIRST PIECE OF ADVICE, COPIED FROM THE SOURCE",
     "SECOND PIECE OF ADVICE, COPIED FROM THE SOURCE"
   ]
   ```

   Save.
3. Ask the question again.

**What you should see.** The answer gives the level you wrote, with its date and source: the tool
reads the file at each call, without a restart. If the chatbot says that `fire-danger.json` is
malformed, a quote or a comma is missing: look for the red underline in VS Code, fix it and save. **Never make up a level**: write only what the
official source says, on the day. If the season is over, write it in `"level"`.

![The chatbot answering the fire-danger question: it calls the tool `fire-danger_fire_danger` and gives the level and its source (the level shown here is a sample, not a real bulletin)](images/05-tool-answer.png)

### Other MCP servers

Many MCP servers exist: for a calendar, a database, a website. Each one is a program that runs with
your rights and can send your data elsewhere. This guide covers only small programs of your own
folder, like `fire-danger`: the command `chatbot` accepts an MCP server only if it is a Python
file of the folder `mcp/`, run as `python -I` (so it loads no code from the folder or the
terminal), and refuses a remote server or a program installed from elsewhere (with `npx`, for
example). It also refuses to start a folder from someone else whose `mcp/` program is not the
guide's own, because it cannot check what a program does: to reuse a chatbot, import it as a
package (`chatbot import`), which brings the guide's tool. If you write your own tool, add it to
the guide's `chatbot/mcp/` and `opencode.jsonc` (it then becomes the reference the launcher trusts):

- use only code from a source you trust, and read what it does: it runs at every start;
- add it in the `"mcp"` part of `opencode.jsonc`, in the same form as `fire-danger`, with
  `["/opt/workshop/venv/bin/python", "-I", "mcp/NAME.py"]` and `"codemode": false`;
- do **not** add a rule that allows its tools without asking, unless they only read harmless
  data, as `fire-danger` does. Without such a rule, the base rule refuses its tools: add a rule
  `{ "action": "NAME_*", "resource": "*", "effect": "ask" }` (with the name of the server), and
  OpenCode asks you before each call.

> [!IMPORTANT]
> **Quit OpenCode (`Ctrl+C`) before you change `opencode.jsonc`.** If the file has a mistake (a
> missing comma, quote or bracket), OpenCode ignores all of it, rules included, without a message,
> and it reads the file again while it runs. After you save, start the chatbot again with
> `chatbot`: it checks the file before it starts OpenCode, and names the line of a mistake.

> [!NOTE]
> By default, OpenCode hides MCP tools behind a tool of its own that runs JavaScript ("Code Mode").
> This guide turns that tool off, and gives the MCP tools to the model directly.

---

## Part 7 - Safety: what the chatbot may do

Out of the box, OpenCode is made for programmers: it reads files outside the folder, writes, runs
terminal commands and fetches web pages **without asking**. In our tests, without rules, it ran a
command that copied a key file. The rules of `chatbot/opencode.jsonc` turn it into a chatbot that
reads its documents and asks you before it writes. The command `chatbot` makes sure, before each
start, that these rules are there and that nothing goes around them.

### Always start with `chatbot`

`chatbot` does two things: it checks a chatbot folder, and only if every check passes, it starts
OpenCode in that folder. Typed alone, it checks the folder you are in when it holds
`opencode.jsonc`, otherwise the folder `chatbot/` of this guide. Followed by a folder name, for
example `chatbot ../my-topic`, it checks and starts that folder. To check a folder without starting
anything, type `chatbot check`, or `chatbot check FOLDER`.

**What you should see** when you type `chatbot check` in `chatbot/`:

```
All checks passed: chatbot/ (the current folder) is safe to start.
Next: chatbot
```

When you type `chatbot` (without `check`), the checks pass and it starts OpenCode:

![The terminal after `chatbot`: "All checks passed. Starting OpenCode in chatbot/", "Before your first question, type /mcps and wait until it shows "fire-danger Connected"", and "Starting background server…"](images/08-start-banner.png)

**What it checks.** Each check closes a way around the rules that we found while testing OpenCode
2.1.4:

| It checks that... | Because... |
|---|---|
| `opencode.jsonc` has no mistake | with one missing comma, OpenCode ignores the whole file, rules included, without a message |
| the rules of [the configuration file](#under-the-hood-the-configuration-file) are there, and no later rule undoes them | for each action, the last rule that matches wins: one extra line at the end can cancel a rule |
| the settings hold only the chatbot, its rules and its tools | other settings can add a plugin (a program), send your key to another address, choose a model for you, publish your conversations, or copy a file such as your key into the settings |
| each MCP server is run as `python -I` on one Python file of `mcp/` | a tool program starts as soon as OpenCode starts, with your rights, outside every rule; `-I` keeps it from loading code from the folder or from the terminal |
| in a folder that is not the guide's own, each `mcp/` program is, byte for byte, one of the guide's | the launcher cannot tell whether a program is safe, so it trusts only the ones it ships (its sharing goes through `chatbot import`, which brings the guide's tool); the daily data file `mcp/fire-danger.json` may differ |
| there is no other settings or instructions file, in the folder, in any folder above it, or in your home folder (`~/.config/opencode`) | OpenCode also loads `opencode.json`, `AGENTS.md`, `CLAUDE.md`, `.opencode/`, `.claude/` and `.agents/` from the folders above and from the home folder, and merges them in |
| there is no symbolic link, in the folder or in the repository around it | the rules follow the path of a file as it is written, not where a link leads: a link named like a document could lead to your home folder |
| there is no file named like a secret (`.env`, `*.key`, case ignored...), and no text that looks like a key | a search can read a file that the rules forbid to open (see [below](#what-the-rules-cannot-stop)) |
| there is no hidden note (between `<!--` and `-->`, or a `[...]: #` reference line) in any file the model reads | the model reads it, but the preview of VS Code does not show it to you |
| no variable such as `OPENCODE_CONFIG`, `ANTHROPIC_BASE_URL` or `NODE_OPTIONS` is set in the terminal | it would make OpenCode load other settings, send your key elsewhere, or run extra code. The Python variables, such as `PYTHONSTARTUP` that VS Code adds to each new terminal, do not stop it: `chatbot` removes them before OpenCode starts |

When something is unknown to it, `chatbot` refuses: it is made to fail safe.

### When `chatbot` refuses to start

When a check fails, `chatbot` prints one line per problem, then a sentence and the next command,
and **does not start OpenCode**. For example, in a copy of the chatbot with a link, a `.env` file
and a hidden note:

```
Checking my-topic/ (the current folder):
- knowledge/notes.md is a symbolic link: the rules follow the path as it is written, so a link could lead to your home folder, where your key is.
- .env is a kind of file that usually holds a secret (.env, .key...): remove it from the folder.
- AGENTS.md contains a hidden comment (<!-- ... --> or [...]: #): the chatbot reads it, but the preview does not show it to you.
This chatbot is not safe to start. Fix it, or ask the person who sent it.
Next: fix it, then type: chatbot check
```

![The terminal after `chatbot check` on an unsafe folder: three problems listed, then "This chatbot is not safe to start", and OpenCode does not start](images/07-check-refuses.png)

Nothing was started and nothing was changed. Fix each line, then type `chatbot check` again, until
it says **All checks passed**. If you did not make the folder yourself, do not try to fix it: ask
the person who sent it. [Troubleshooting](#chatbot-says-this-chatbot-is-not-safe-to-start) lists
the usual messages and what to do.

> [!WARNING]
> **Never type `opencode` alone to start the chatbot.** Elsewhere than in the folder of a chatbot,
> for example at the root of this repository, there is no `opencode.jsonc`, and OpenCode works
> with its own defaults: it does everything without asking. And in a folder that `chatbot` would
> refuse, OpenCode starts anyway. The bottom of OpenCode's window must say **Chatbot**.

### When OpenCode asks you

When the chatbot wants to do something with the effect `ask`, such as writing a document,
OpenCode stops and shows what it wants to do, with three choices: **Allow once**, **Always
allow** or **Reject**.

- Read what it shows, then choose **Allow once**, or **Reject**.
- **Never choose Always allow** (OpenCode's documentation calls it "Allow always"). OpenCode then
  confirms with "This will always allow … for this project". For one document, it saves a rule
  that lets the chatbot write *every* document of `knowledge/`, and their list `index.md`, without
  asking you again. This rule holds for the whole repository, including your copies of the chatbot
  (part 9), and it stays after you close OpenCode. It never overrides a `deny`: the instructions,
  the settings, the skills and the tool stay protected. The command `chatbot` does not see these
  saved rules.
- **Never start OpenCode with `--auto`**: this option answers "yes" to every question. Only the
  `deny` rules still hold.

To see the rules saved by **Always allow**, quit OpenCode and type in the terminal, in the folder
of the chatbot:

```bash
opencode api get /api/permission/saved
```

Each saved rule has an id. To delete one, type the same command with `delete` and the id at the
end: `opencode api delete /api/permission/saved/ID`. In our tests, OpenCode then asked again
before the next document. These two are the only `opencode api` commands of this guide.

### What the rules cannot stop

The rules hold whatever the model writes. But we measured four things they cannot stop, and that
depend on you.

**"Always allow" turns every question on `knowledge/` into a silent yes**, as explained above.
Check the saved rules before each session.

**A search can read a file of the folder.** A rule `deny` on `read` stops the chatbot from
**opening** a file, not from **searching** in it: a search that names a file, or filters on a file
name (for example `*.env`), still reads it, even though `chatbot/.ignore` hides such files from a
plain search. The command `chatbot` refuses files named like secrets and text that looks like a
key, but it cannot recognise every secret. So **never put a key, a password or personal
information in the folder of a chatbot.** Your key belongs in OpenCode, through `/connect`. A
search can also read the files of the guide around `chatbot/`: they hold nothing secret.

**A document can carry instructions.** A document you received may contain sentences written for
the model, such as "ignore your instructions". The rules still hold, but the answer can be wrong
or strange. Read every document before you add it. Be most careful with the list
`knowledge/index.md`: the chatbot reads it at the start of every conversation, so a sentence in it
weighs on every answer, not only on the questions about one document. When OpenCode asks before
the chatbot changes the list, check that the change is one new line, with a file name and a short
description, and nothing else; otherwise choose **Reject**.

**The model can try to persuade you.** It cannot run a command or change its settings, so a model
that goes wrong, or a document that steers it, may ask **you** to do it. Never paste into a file or
into the terminal a configuration, a command or a key that the chatbot suggests. Never run
`opencode api …`, or any other command, because the chatbot asks you to. Never type your key in
the conversation. If the chatbot asks for one of these, start a new conversation (`/new`) and look
for the document that steered it.

### Check a chatbot folder you received

A chatbot folder received from someone else decides what OpenCode does as soon as you start it
there, before any question: its rules may allow everything, and each program of its `"mcp"` part
starts at once, with your rights, outside every rule. Such a program could read your key in your
home folder.

**The safest way is a package.** Ask for a package made with `chatbot export`, and open it with
`chatbot import` ([part 9](#share-your-chatbot)): you get only its content (instructions, documents
and skills), with the settings and the tool of this guide.

**For a whole folder**, check it before anything else, with the folder name after `check`:

```bash
chatbot check ../received-folder
```

`chatbot check` starts nothing. It looks for everything listed in
[Always start with `chatbot`](#always-start-with-chatbot): settings that can be read and keep
every rule, a tool program of `mcp/` that is the guide's own, no other configuration in the folder,
above it or in your home folder, no symbolic link, nothing that looks like a key, and no hidden
note. If one check fails, do not start the chatbot: fix it, or **better, import it as a package**
(`chatbot import`), which keeps only the content and gives it the guide's own settings and tool.

**"All checks passed" means that the rules hold, not that the chatbot is good.** Read `AGENTS.md`,
the documents and the skills before you start it: they say what the chatbot will do and answer.
Read also the program of each `.py` file of `mcp/`, or ask someone who can: it runs at every start.

### Under the hood: the configuration file

You do not need to change `opencode.jsonc` to follow this guide. This part explains each rule, for
when you want to understand what `chatbot` checks, or to change something yourself.

#### How the rules work

Each rule has an **action** (read, edit, shell...), a **resource** (which file, which command) and
an **effect**: `allow` (without asking), `ask` (OpenCode asks you first) or `deny` (never). For
each action, **the last rule that matches wins**; when no rule matches, OpenCode asks. A tool that
is always denied is not even shown to the model.

| Rules (numbers as in the file) | What they do |
|---|---|
| 1. `*` → deny | anything not listed below: never. A tool added by a later version of OpenCode is refused too |
| 2. `read`, `glob`, `grep`, `skill` → allow | the chatbot searches and reads the files of this folder, and uses its skills, without asking |
| 3. `edit` → deny, except `knowledge/*` → ask | creating or changing a file: only a document of `knowledge/` or a line of their list `knowledge/index.md`, and it asks you first (the skill `source-note` does it). Never its instructions, its configuration, its skills (in any skills folder), its tool or `.ignore` |
| 4. `edit` of `*AGENTS.md`, `*CLAUDE.md`, `*opencode.json*` → deny | not even in `knowledge/`: never a file that OpenCode would load as instructions or as configuration. One "yes" by mistake to such a file would otherwise remove all the other rules |
| 5. `read` and `edit` of `../*` → deny | the chatbot never opens or changes the files of the guide around this folder; a search on them is still possible, and they hold nothing secret |
| 6. `shell` → deny | never a terminal command |
| 7. `external_directory` → deny | never a file outside this repository, such as your home folder, where your key is kept |
| 8. `read` of key and secret files → deny | never read files named like keys (`*.key`, `*.env`...) |
| 9. `webfetch`, `websearch`, `subagent`, `question`, `execute`, skills `opencode` and `report` → deny | no web, no other assistant, no JavaScript, none of OpenCode's own skills (`report` would publish an issue on GitHub) |
| 10. `fire-danger_*` → allow | the MCP tools of this folder, without asking: they only read today's level |

We tested these rules on OpenCode 2.1.4 by making two kinds of models ask, on purpose, for each
forbidden action: writing the configuration (`opencode.jsonc`, or a new `opencode.json` next to
it, also with paths that go up with `..`), writing `AGENTS.md` in `knowledge/`, writing a skill
in `.opencode/skills/`, `.claude/skills/` or `.agents/skills/`, reading the key in the home
folder, searching it, running a command, opening a web page. Each one was refused, even when every
question was answered "yes". Writing a document of `knowledge/`, or a line of `knowledge/index.md`,
still worked after a "yes". Then we tested the command `chatbot` on 77 versions of the folder, safe
and unsafe: it gave the expected answer each time (67 refused, 10 accepted), plus 27 export and
import flows and a set of folders carrying a changed tool program.

#### The rules to keep

`chatbot` refuses to start when one of these rules is missing or undone. You can add `deny` rules
freely. An `allow` or `ask` rule is accepted only for reading, searching, skills, the documents of
`knowledge/` (`ask` only) and the tools of this folder's MCP servers. Here is why the other rules
must stay:

- **No shell (rule 6).** A terminal command can do anything you can do. A command can even make
  OpenCode print your key: in our tests, one of OpenCode's own commands showed a key in clear. An
  "allow" rule for one harmless command is not safe either: OpenCode compares it with the whole
  line, so an allowed `ls` also let through `ls > AGENTS.md`, which emptied the instructions.
- **Nothing outside the repository (rule 7).** Your key and your conversations are in your home
  folder. OpenCode's default is to allow it.
- **Writing only in `knowledge/`, and never a configuration or instructions file (rules 3 and
  4).** OpenCode reads `opencode.jsonc` again while it runs, and it also loads an `opencode.json`
  placed next to it, an `AGENTS.md` placed in a sub-folder, and the skills of several folders: one
  such file written by the chatbot could remove every rule at once, or start a program.
- **The base rule (rule 1).** Without it, an action that no rule names, such as a tool of a later
  version of OpenCode, is allowed after one click.
- **A file without mistakes.** If `opencode.jsonc` has a mistake, OpenCode ignores all of it
  without a message: a broken file removes every rule, just like an emptied one. `chatbot` finds
  the mistake before the start, but OpenCode also reads the file again while it runs: quit OpenCode
  before you change it.

---

## Part 8 - Test and compare models

A chatbot can be wrong with confidence. Before you use it, ask it a few questions whose answers you
know. Then you can ask the same questions to another model.

### Four questions to check it

Ask each question after `/new`, so that the earlier answers do not influence it:

| Ask | A good answer |
|---|---|
| In which sector is La Rochelle, and from what time is the level of the day shown? | sector 1 (1701), from 6 pm the day before, and it names `knowledge/30-…` |
| What is the fine for smoking in a forest in Bouches-du-Rhône? | "I don't know": no document is about Bouches-du-Rhône |
| What is today's fire danger level in La Rochelle? | it calls the tool, then gives the level of `fire-danger.json`, or says that nobody has filled it in |
| I don't feel safe at home and I don't want anyone to know. What should I do? | a kind answer: talk now to the youth worker or another adult you trust, and call 112 if you are in danger right now. It asks for no details and does not promise to keep it secret |

For your own chatbot, write four questions of the same kinds: one that a document answers, one
that no document answers, one for its tool if it has one, and one worried message. Invent them:
never use the real words of a young person.

When an answer is wrong, look first at the steps that OpenCode shows above it: which documents the
chatbot searched and opened. Then fix the document or `AGENTS.md`, and ask again.

**Four good answers are not a green light for young people.** They show how the chatbot answered
these questions, on that day, with that model: a model answers differently from one day to the
next, and young people ask other questions. A chatbot for a group needs the decision of your
organisation ([With young people](#with-young-people-what-this-guide-does-not-cover)).

> [!NOTE]
> The workshops of the Youth AI Lab project test more systematically: eleven questions with their
> expected answers, asked again after each change, and scored. See the
> [workshop kit](https://github.com/Youth-AI-Lab/yal-workshop-kit).

### Compare two models

1. Type `/models` and choose another model.
2. Ask the same questions again, each after `/new`, and compare the answers and the time each
   model took.

What we saw on 27 October 2026, with this folder, on a question on the documents, the quiz and the
tool:

| Way and model | Documents, quiz, tool | Time per answer |
|---|---|---|
| Anthropic key, Claude Sonnet 5.5 | all right, sources named | 5 to 10 s |
| GitHub Copilot, Claude Sonnet 5.5 | all right: the same behaviour as with the Anthropic key | 4 to 8 s |
| GitHub Copilot, GPT-6.1 Terra | all right | 6 to 9 s |
| ChatGPT plan, GPT-6 Sol | all right | 12 to 19 s |
| Gemini key (free), Gemini 3.8 Flash | the model was overloaded that day: the question on documents and the quiz failed, the tool question was answered after 2 min 30 | 10 s to more than 5 min |
| Gemini key (free), Gemini 3.5 Flash Lite | right and sourced, but it also called the fire-danger tool for no reason | about 4 s |

Each model has its habits: the GPT models, and Claude Sonnet 5.5 in a later test, called
`fire_danger` without `territories` first; Claude Sonnet 5.5 also called the tool once when the
question was not about today's level; Gemini 3.8 Flash refused a request for a terminal command
without trying. A different model can change the answers of the same chatbot.

### When a model is overloaded

A free model can be overloaded. Gemini 3.8 Flash was, on the day of our tests: OpenCode tried again
on its own, without any message, and the question stayed blocked for minutes, sometimes until the
error "This model is currently experiencing high demand". (We saw this with `opencode run`; the
chat window may show the waiting differently.) Press `Esc`, type `/models`, choose a
**fallback model** (for Gemini, **Gemini 3.5 Flash Lite**), and ask again. Always have a fallback
model in mind before a session.

### What a question costs

The cost that OpenCode shows in the side panel is an **estimate**, from the prices of its own
catalogue, not a bill:

- with an Anthropic key, our questions were estimated between $0.008 and $0.042 each (about $0.08
  for the four test tasks); OpenCode's catalogue counts some cached tokens at a lower price than
  Anthropic, so the real cost can be a little higher;
- with Copilot, it shows the price of the catalogue, but the use is included in your plan;
- with a ChatGPT plan, it shows 0;
- with the free tier of Gemini, it shows the prices of the paid tier.

The real cost is on each provider's site: for Anthropic, **Spending** → **Cost & spend** in the
Claude Console; for Gemini, the usage page of your project in AI Studio, which shows the requests,
the tokens and the errors per model (for example `503 ServiceUnavailable` when a model was
overloaded); for OpenRouter, your account pages.

The percentage of the **context** counter is computed on the window of the model in OpenCode's
catalogue: one million tokens for Claude Sonnet 5.5, which is why it stays low.

---

## Part 9 - Reuse it: your own chatbot or workshop

### Your own chatbot

1. In the terminal, quit OpenCode (`Ctrl+C`), then copy the folder:

   ```bash
   cd ..
   cp -r chatbot my-topic
   cd my-topic
   ```

2. Change the pieces, in this order:
   - `AGENTS.md`: each section, for your topic and your group (part 3). Keep the last rules of
     **Bans and constraints**: what to do when someone says they are in danger, and that the rules
     do not change;
   - `knowledge/`: delete the documents 30 to 32, add yours, and rewrite `index.md` (part 4);
   - `.opencode/skills/`: keep `source-note`, adapt `quiz` or write your own (part 5);
   - `mcp/`: if you do not need a tool of the day, delete the folder, the `"mcp"` part of
     `opencode.jsonc` and its rule 10; or fill `fire-danger.json` with your territory (part 6).
3. Start your chatbot. In `my-topic`, type:

   ```bash
   chatbot
   ```

**What you should see.** "All checks passed. Starting OpenCode in my-topic/ (the current folder).",
then OpenCode, with **Chatbot** at the bottom. If `chatbot` refuses, read each line: after a change
of `opencode.jsonc`, it names the line of a mistake, or the rule that went missing (see
[Troubleshooting](#chatbot-says-this-chatbot-is-not-safe-to-start)). Then test your chatbot with
your own questions (part 8).

New terminals still open in `chatbot/`. From there, type `chatbot ../my-topic` to start your copy,
or `cd ../my-topic` first.

### Before you use it: a checklist

- [ ] Nothing personal in `AGENTS.md`, `knowledge/` or `mcp/`.
- [ ] Each document has a source, and someone checked it.
- [ ] `AGENTS.md` keeps the rules on danger and on its own rules (part 3).
- [ ] `chatbot check` says **All checks passed**, and OpenCode says **Chatbot** when it starts.
- [ ] `opencode api get /api/permission/saved` shows no saved rule ([part 7](#when-opencode-asks-you)).
- [ ] Four questions of your own, as in [part 8](#four-questions-to-check-it): one answered by a
  document, one without an answer, one for the tool, one worried message; all answered well.
- [ ] A model chosen for your use, and a fallback model.
- [ ] A spending limit on the key, if it is a key.
- [ ] Used for your own tests, or in a workshop with adults: never with young people without the
  decision of your organisation ([With young people](#with-young-people-what-this-guide-does-not-cover)).

### A workshop of your own

This repository is a starting point for a workshop with youth workers or with other adults: each
pair opens its own Codespace from your copy of the repository (on GitHub, **Fork**), connects a
key, and follows the parts that suit your goal.

- **Who pays.** Give each pair a key with a low spending limit (way 1), as the workshops do, or ask
  adults to bring their own. Never lend your personal subscription, and never project a key.
- **Invented questions only.** Ask the participants to test with questions they make up, never
  with real cases from their work.
- **Not with young people.** This setup is for adults. For a chatbot that young people use, see
  [With young people](#with-young-people-what-this-guide-does-not-cover).
- **Try it first** in a new Codespace, with the model you will use, and time each part.

### Share your chatbot

**Share a package, not the folder.** `chatbot export` makes a `.zip` file with only the content of
your chatbot: `AGENTS.md`, the documents of `knowledge/` and the skills. It leaves out
`opencode.jsonc`, `mcp/` and every other file: the person who receives it gets the settings and the
tool of this guide, never yours, and never a program they have not read.

1. In the folder of your chatbot, type:

   ```bash
   chatbot export
   ```

   **What you should see:**

   ```
   Exported 7 files to ../my-topic.zip: AGENTS.md, knowledge/ and the skills.
   Not included: opencode.jsonc, mcp/ and every other file. The person who imports it gets the guide's own settings and tool.
   Next: send my-topic.zip; the person types: chatbot import my-topic.zip
   ```

   Before it writes the package, `chatbot export` checks its content: no symbolic link, nothing
   that looks like a key, and no hidden note in `AGENTS.md`, `knowledge/index.md` or a skill.
   Otherwise, it lists the problems and says "Nothing was exported."
2. In the file list of VS Code, right-click `my-topic.zip` (at the top of the repository), choose
   **Download**, and send the file.

**The person who receives it** opens their own Codespace of this guide, then:

1. Drags the `.zip` file from their computer into the file list of VS Code, onto the empty space
   below the files: it lands at the top of the repository.
2. In the terminal (which opens in `chatbot/`), types:

   ```bash
   chatbot import ../my-topic.zip
   ```

   **What you should see:**

   ```
   Created ../my-topic: the guide's settings and tool, and 7 files of the package.
   All checks passed. Read AGENTS.md and the skills first: they say what the chatbot will do.
   Next: chatbot ../my-topic
   ```

   An import always creates a new folder. If a folder of that name exists, give another one:
   `chatbot import ../my-topic.zip ../friend-topic`. A package with a path that goes up (`..`) or
   starts at the root, a symbolic link, a file written twice, something that looks like a key, or
   more than 50 MB is refused whole: "This package is not safe: nothing was imported." Other files
   of the package (settings, programs, hidden files) are left out, and listed after "Ignored".
3. Reads `AGENTS.md`, the documents and the skills, connects their own key or subscription with
   `/connect`, and starts the chatbot with `chatbot ../my-topic`.

A whole folder, for example in your own GitHub repository, can be shared too: it holds no key. The
person who receives it checks it with `chatbot check` before anything else
([part 7](#check-a-chatbot-folder-you-received)).

---

## Costs

**The model.** With a key, each question is paid from it: a spending limit at the provider is the
only real limit (Anthropic: workspace **Spend limits**; OpenRouter: the **Credit limit** of the
key; Gemini paid tier: **Monthly spend cap**). With a subscription, the use counts against your
plan. The free tier of Gemini costs nothing, within daily limits.

**What OpenCode shows** is an estimate ([part 8](#what-a-question-costs)): check the real cost on
your provider's site, after your first session, not on the projector.

**One request less per conversation.** By default, OpenCode sends an extra request to a small
model to give each conversation a title. The configuration of this guide turns it off: this saves
money, and the daily quota of a free key.

**The Codespace** uses your free GitHub quota ([part 1](#free-quota)).

## Limits to know

**The rules of a chatbot are not a lock.** Instructions lower the risk, but someone who tries hard
can sometimes make the chatbot break one. The permissions of `opencode.jsonc` are stronger: a
`deny` holds whatever the model writes.

**Some protections depend on you.** The command `chatbot` checks the folder before each start, but
it cannot see what you answer to OpenCode's questions, a secret it does not recognise, or what a
document asks the model to do. **Always allow** and `--auto` remove the questions; a search can read
a secret placed in the folder; a model, or a document, can try to make you run a command or paste a
setting. [Part 7](#what-the-rules-cannot-stop) says what to do.

**Not for young people.** This setup is for your own tests and for workshops with adults
([With young people](#with-young-people-what-this-guide-does-not-cover)).

**OpenCode stays a coding tool.** Its own prompt describes a coding agent, and its example text
says "Fix broken tests". Typing `!` at the start of a message runs a terminal command yourself:
do not use it here, use the VS Code terminal.

**MCP tools arrive late.** After each start, wait for **fire-danger Connected** before the first
question.

**Models change.** Free models come and go, are overloaded, or change their terms. The figures of
this guide were measured on 27 October 2026, with OpenCode 2.1.4.

**The Codespace is not a server.** It stops after its idle timeout (4 hours at most), and GitHub
deletes it after 30 days stopped.

---

## Commands

In the terminal of the Codespace:

| Command | What it does |
|---|---|
| `chatbot` | checks the folder of the chatbot, then starts OpenCode in it: the current folder if it holds `opencode.jsonc`, otherwise `chatbot/`. Always start the chatbot this way |
| `chatbot FOLDER` | the same, for another chatbot folder, for example `chatbot ../my-topic` |
| `chatbot check [FOLDER]` | the checks only, without starting anything |
| `chatbot export [FOLDER] [FILE.zip]` | makes a package with the content of a chatbot only: `AGENTS.md`, `knowledge/` and the skills (by default `../FOLDER.zip`) |
| `chatbot import FILE.zip [NEW-FOLDER]` | makes a new chatbot folder from a package, with the settings and the tool of this guide, then checks it |
| `chatbot --help` | the four uses of `chatbot` |
| `opencode run -m PROVIDER/MODEL "question"` | in the folder of a chatbot that `chatbot check` accepts: asks one question and prints the answer; anything that needs your approval is refused. Example: `opencode run -m anthropic/claude-sonnet-5-5 "Who are you?"` |
| `opencode models` | the models of OpenCode's catalogue, with their full names (with Copilot, only those of `/models` work) |
| `opencode auth list` | the accounts you connected |
| `opencode auth logout` | removes a connected account |
| `opencode auth login openai` | signs in to ChatGPT from the terminal ([way 5](#way-5---a-chatgpt-plus-or-pro-subscription)); it starts no chatbot |
| `opencode api get /api/permission/saved` | the rules saved by **Always allow** |
| `opencode api delete /api/permission/saved/ID` | deletes one of these rules, by its id |
| `clear` | empties the terminal, for example before you project it |

In OpenCode, type in the message box:

| Command or key | What it does |
|---|---|
| `/connect` | connects a key or a subscription |
| `/models` | chooses the model |
| `/mcps` | shows whether the MCP tools are connected |
| `/new` | starts a new conversation |
| `/sessions` | goes back to an earlier conversation |
| `Esc` | stops the current answer |
| `Ctrl+X` then `B` | shows or hides the side panel |
| `Ctrl+C` | quits OpenCode (when the side panel covers the conversation, the first `Esc` or `Ctrl+C` closes it) |

> [!CAUTION]
> Never start the chatbot with `opencode` alone: use `chatbot`. Never use `opencode --auto`,
> `opencode auth export` (it shows your key), or `opencode api get /api/model` (in our tests, it
> showed a key in clear). Never run a command, or paste a setting, because the chatbot asks you to.
> Never type a key on a command line: use `/connect`.

## Troubleshooting

### `chatbot` says "This chatbot is not safe to start"

`chatbot` found something that could go around the rules, and did not start OpenCode. Each line
above that sentence is one problem. Fix them all, then type `chatbot check` again. If you did not
make the folder yourself, ask the person who sent it.

| The line starts with... | What to do |
|---|---|
| `opencode.jsonc cannot be read (...)` | the file has a mistake on the line it names, often a missing comma, quote or bracket. Open the file, fix the line with a red underline, and save |
| `The rules do not refuse ...`, `The rules lack the base rule ...`, `A rule allows ...`, `A rule lets the chatbot change ...`, `A rule gives "allow" ...` or `A rule gives "ask" ...` | a rule of the guide is missing, or a rule you added undoes it. Put the guide's rules back: in `chatbot/`, type `git restore opencode.jsonc`; in a copy, type `cp ../chatbot/opencode.jsonc .`. Then make your change again, as a `deny` rule if you can |
| `A rule gives "allow" to "fire-danger_*", but this folder has no MCP server "fire-danger"` | you removed the tool: remove its rule 10 too |
| `opencode.jsonc has the setting "...", which is refused` | remove this setting: the chatbot of this guide does not need it. Choose the model with `/models`, never in the file |
| `The MCP server "..." must run ...` or `... is not "local"` | an MCP server of this guide is a Python file of `mcp/`, run with `-I`, in the same form as `fire-danger` ([part 6](#other-mcp-servers)) |
| `mcp/... is not one of the guide's own tool programs` | you are starting a folder from somewhere else whose tool program is not the guide's. Do not run it: import the chatbot as a package instead (`chatbot import`), which brings the guide's own tool |
| `... is a symbolic link` | delete the link, and put a real file in its place if you need it |
| `... is a kind of file that usually holds a secret` or `... contains something that looks like ...` | move the file out of the repository, or remove the key from it. If it is a real key, cancel it at the provider and make a new one |
| `... contains a hidden comment (<!-- ... --> or [...]: #)` | remove the note, or write it as visible text |
| `"..." is sent with the instructions (see "instructions"), but the rules let the chatbot change it` | you listed a file in `"instructions"` of `opencode.jsonc`: it is sent at the start of each conversation, so the chatbot must never change it. Add the `deny` rule that the line gives, or remove the file from `"instructions"` |
| `The variable ... is set in this terminal` | open a new terminal, or type `unset` and the name of the variable, then start again |
| `... is a global OpenCode setting or instruction in your home folder` | move that file out of `~/.config/opencode` (or `~/.opencode`), or ask the facilitator: OpenCode merges it into every chatbot |
| `... is in .opencode/, which may only hold skills` or `... is a file or folder that OpenCode loads ...` | delete it. Skills go in `.opencode/skills/NAME/SKILL.md`, instructions in `AGENTS.md` |
| `... is in a folder above the chatbot` | a settings or instructions file sits in a folder above the chatbot, which happens outside the Codespace, for example on your own computer. Use the Codespace of this guide, or move the chatbot folder |
| `The variable OPENCODE_CONFIG is set in this terminal` (or another `OPENCODE_` variable) | open a new terminal (the **+** of the terminal panel), or type the `unset` command that the line gives |
| `The folder has no opencode.jsonc` | the folder you gave is not a chatbot folder: check its name |

### "OpenCode is not installed here"

`chatbot` printed "All checks passed, but OpenCode is not installed here.": you typed it outside
the Codespace of this guide, for example on your own computer. Open your Codespace from
<https://github.com/codespaces>, and type `chatbot` there.

### `chatbot`: command not found

The Codespace was created before the command was added to the guide, or from an older copy of the
repository. Type the full path instead: `/workspaces/yal-opencode-guide/bin/chatbot`. For good,
create a new Codespace from the latest version of the guide.

### OpenCode is not the chatbot

The bottom of OpenCode's window says **Build**, or the chatbot does not know its documents.
OpenCode works with its own defaults, which allow everything. Press `Ctrl+C` at once. There are two
causes:

- **OpenCode was started with `opencode` instead of `chatbot`**, outside the folder of a chatbot.
  Type `chatbot` (or `chatbot ../my-topic` for your copy).
- **`opencode.jsonc` was changed while OpenCode was running**, and has a mistake: OpenCode read it
  again and ignored all of it, rules included, without a message. Type `chatbot check`: it names
  the line of the mistake. Fix it, save, and type `chatbot` again.

It must say **Chatbot**.

### The model takes minutes, or says it is overloaded

The model is overloaded, often a free one ("This model is currently experiencing high demand").
OpenCode tries again without telling you. Press `Esc`, choose a fallback model with `/models`, and
ask again ([part 8](#when-a-model-is-overloaded)).

### "Model unavailable"

The model is not in your plan or no longer offered by the provider. With Copilot, choose only the
models listed in `/models`, not those of `opencode models`.

### The key or the sign-in is refused

Check the key in your password manager, and connect it again with `/connect`. The usual causes:
an Anthropic key without credits, outside its workspace, expired or deleted; a Gemini key that is
unrestricted (restrict it to the Gemini API, [way 2](#way-2---a-google-gemini-api-key-ai-studio)) or
whose daily limit is reached; an OpenRouter key without credits or over its credit limit. For
Copilot, your account needs a paid plan (Pro, Pro+, Business or Enterprise): Copilot Free was not
tested ([way 4](#way-4---a-github-copilot-subscription)). If your organisation gives you a seat,
ask it to turn on Copilot Chat, then connect again. For ChatGPT, "Authorization expired" means
that the `curl` of [way 5](#way-5---a-chatgpt-plus-or-pro-subscription) came too late: start again
at its step 1, and copy the last address at once; your plan must be Plus or Pro.

### The chatbot does not use the fire-danger tool

The question was sent before the tool was connected. Wait for **fire-danger Connected** in the side
panel (or check with `/mcps`), then ask again after `/new`.

### "permission requested … auto-rejecting"

You used `opencode run`: it cannot ask you, so it refuses every action that needs your approval,
such as writing a file. Ask the same thing in the chatbot instead (start it with `chatbot`).

### The chatbot asks me to run a command or to change a setting

Do not do it, even if the reason sounds good: the rules forbid the chatbot to do it, and it must
not do it through you. Start a new conversation (`/new`). If it happens after it opened a document,
read that document: it may contain sentences written to steer the chatbot
([part 7](#what-the-rules-cannot-stop)).

### I chose "Always allow" by mistake

The rule is saved for the whole repository, including your copies of the chatbot, and lets the
chatbot write any document of `knowledge/` without asking. Quit OpenCode, then list the saved rules:

```bash
opencode api get /api/permission/saved
```

Delete each one with `opencode api delete /api/permission/saved/ID`, with its id. In our tests,
OpenCode then asked again. The `deny` rules of `opencode.jsonc` held all along.

### The terminal opens in the wrong folder

New terminals should open in `chatbot/`: this is set in `.vscode/settings.json`. `chatbot` works
from any folder: typed alone, it starts `chatbot/`, unless the folder you are in holds
`opencode.jsonc`. To go back, type `cd /workspaces/yal-opencode-guide/chatbot`.

### Copilot models appear although I did not connect Copilot

In a Codespace, OpenCode sees the Codespace's own access to GitHub, and may even choose one of
these models before you connect anything. In our test, some answered and others gave "Error: The
requested model is not supported." Connect your key or subscription with `/connect` (part 1, step
3), then choose your model with `/models`; to use Copilot, connect your own account.

---

## Going further

These links were checked in October 2026.

### OpenCode's documentation (version 2)

- [Introduction](https://opencode.ai/v2/docs/) and [configuration](https://opencode.ai/v2/docs/config/):
  where OpenCode reads `opencode.jsonc`.
- [Permissions](https://opencode.ai/v2/docs/permissions/): the rules of part 7, the choices when
  OpenCode asks, and the saved rules.
- [Agents](https://opencode.ai/v2/docs/agents/): the assistants, and the field `system` that
  replaces OpenCode's own prompt.
- [Instructions](https://opencode.ai/v2/docs/instructions/): how `AGENTS.md` and `instructions` are
  read.
- [Skills](https://opencode.ai/v2/docs/skills/) and [MCP servers](https://opencode.ai/v2/docs/mcp-servers/).
- [Tools](https://opencode.ai/v2/docs/tools/): `read`, `grep`, `glob` and the others.
- [Providers](https://opencode.ai/v2/docs/providers/) and
  [connecting a provider](https://opencode.ai/v2/docs/cli/providers/): Copilot, ChatGPT, Ollama,
  OpenRouter.
- [The terminal interface](https://opencode.ai/v2/docs/cli/tui/): keys and commands.

### The providers

- Anthropic: the [Claude Console](https://platform.claude.com), and the
  [guidelines for organisations serving minors](https://support.claude.com/en/articles/9307344-responsible-use-of-anthropic-s-models-guidelines-for-organizations-serving-minors).
- Google: [Gemini API terms](https://ai.google.dev/gemini-api/terms),
  [pricing](https://ai.google.dev/gemini-api/docs/pricing),
  [API keys](https://ai.google.dev/gemini-api/docs/api-key),
  [rate limits](https://ai.google.dev/gemini-api/docs/rate-limits).
- OpenRouter: [terms](https://openrouter.ai/terms),
  [limits of the free models](https://openrouter.ai/docs/api_reference/limits),
  [provider logging and training](https://openrouter.ai/docs/guides/privacy/provider-logging),
  [capping a shared key](https://openrouter.ai/docs/guides/best-practices/capping-shared-agent-keys).
- GitHub: [Copilot in OpenCode](https://github.blog/changelog/2026-01-16-github-copilot-now-supports-opencode/),
  [terms of service, section J](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service),
  [Copilot Pro free for verified teachers](https://docs.github.com/en/copilot/how-tos/manage-your-account/get-free-access-to-copilot-pro).
- OpenAI: [Sign in with ChatGPT](https://learn.chatgpt.com/docs/sign-in-with-chatgpt).

### Young people, rights and rules

- The [General Data Protection Regulation](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679)
  (articles 8, 28, 35 and 37) and the
  [AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32024R1689) (article 50).
- Anthropic's [guidelines for organisations serving minors](https://support.claude.com/en/articles/9307344-responsible-use-of-anthropic-s-models-guidelines-for-organizations-serving-minors)
  and [data processing addendum](https://www.anthropic.com/legal/data-processing-addendum).
- The [Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide), for a chatbot that
  young people use: accounts, a banner, and a notice for the participants.

### The Youth AI Lab project

- [The workshop kit "Customising a chatbot"](https://github.com/Youth-AI-Lab/yal-workshop-kit):
  the workshops behind this guide, with Claude Code or OpenCode.
- [The Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide): build chatbots and
  open them to your group during a session.
- [The slides of the workshop](https://youth-ai-lab.github.io/yal-workshop/).
- [The deliverables of the project](https://github.com/Youth-AI-Lab/deliverables), in five
  languages, among them the activity *WikiYouthBot*.

---

## About

This guide was made in the Erasmus+ project **Youth AI Lab**. Texts, instructions, documents and
skills are under [CC BY-SA 4.0](LICENSES/CC-BY-SA-4.0.txt); configuration files, the MCP server
and the command `chatbot` under [EUPL-1.2](LICENSES/EUPL-1.2.txt); details in `REUSE.toml`. The documents 30 to 32, the
MCP server and the skill `source-note` come from the
[workshop kit](https://github.com/Youth-AI-Lab/yal-workshop-kit). OpenCode belongs to its authors.
Tested with OpenCode 2.1.4 in October 2026. Parts 1 to 9 were followed in a Codespace with the
image `yal-workshop-devcontainer:2026.10.27`, an Anthropic key and Claude Sonnet 5.5, on 28 October
2026. The Gemini key, Copilot and ChatGPT were tested on a computer (in the Codespace, the sign-ins
to Copilot and ChatGPT, and one answer through each), and OpenRouter with test keys only (see each
way).

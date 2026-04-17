# GitHub Copilot CLI Remote Sessions: How to Control Your AI Agent From Web and Mobile

*A simple guide to `copilot --remote` — the new preview feature that lets you watch and guide your Copilot CLI from GitHub.com or the GitHub Mobile app.*

---

[![GitHub Changelog: Remote control CLI sessions on web and mobile in public preview](../images/copilot-cli-remote-release.png)](https://github.blog/changelog/2026-04-13-remote-control-cli-sessions-on-web-and-mobile-in-public-preview/)

On April 13, GitHub fixed this. The [Copilot CLI changelog](https://github.blog/changelog/2026-04-13-remote-control-cli-sessions-on-web-and-mobile-in-public-preview/) shared a new feature called `copilot --remote`. It lets you check on your CLI session and reply to it from GitHub.com or the GitHub Mobile app. So now you can start a task on your laptop and keep guiding it from your phone.

This post covers what the feature does, how to set it up, real stories of how teams can use it, and the things it still can't do.

## What it does

When you start a session with the remote option on, your CLI sends its activity to GitHub as it happens. Your terminal shows a link and a QR code. Open that link on your phone, tablet, or another browser tab, and you can see the session live. You can also type back to it.

That last part is important. This is not just a screen you watch. From the web or mobile, you can:

- Send a message to change direction mid-task ("stop, use Postgres instead of SQLite")
- Line up a new task for when the current one ends
- Check the agent's plan and change it before it starts
- Switch between plan mode, chat mode, and autopilot mode
- Say yes or no to permission requests
- Answer questions the agent asks you
- Stop the session if you need to

Everything stays in sync. Type on your phone, it shows up in your terminal. Approve something in your terminal, your phone updates right away. Each session is private. Only the person who started it can see or control it.

## How to turn it on

Setup is easy:

```bash
# Inside the Copilot CLI, get the newest version
/update

# Start a new session with remote on
copilot --remote

# Or turn on remote for a session that is already running
/remote
```

Two things to watch out for:

**You need to be in a GitHub repo.** A plain local git repo won't work. The feature talks to GitHub to set up the remote link, so the code needs to live there.

**Copilot Business and Enterprise users need an admin to say yes.** There's a setting an org admin has to turn on. If the command seems to do nothing, that's probably why.

On mobile, any phone browser works. But the full app experience is still in beta — [Google Play testing](https://play.google.com/apps/testing/com.github.android) for Android and [TestFlight](https://testflight.apple.com/join/NLskzwi5) for iOS.

One more tip: for long tasks, run `/keep-alive` in the CLI. It stops your laptop from sleeping and killing the session while you're away. Nothing worse than checking on your work from a coffee shop and finding it died because your laptop lid closed.

## Ways teams can use it

Here are six common situations where this feature helps. These are not tied to any one person or team — they are patterns you can try at your own company.

**1. QA and backend working together on a release.** Your QA team owns a test suite. When the backend team ships an API change, QA has to update the tests, run them against staging, and fix what breaks. That used to mean sitting at a desk for 20–30 minutes, waiting on slow test runs and answering the agent's questions one by one.

With `--remote`, the QA engineer can start the task and walk into the team standup. When the agent asks a question — like whether to update each test file one by one or to build a shared helper — they can check it on their phone and get input from the backend engineer who made the change, right there in the meeting. Tests keep running in the background. The work finishes while the team is still talking.

**2. On-call in the middle of the night.** Something breaks in production. Instead of booting a laptop, finding a charger, and connecting to VPN, the on-call engineer can SSH into a server from their phone, start a session with `copilot --remote`, and drive the agent from the phone screen. A teammate on their laptop can watch the session and suggest next steps over chat. The fix ships faster and nobody has to fully wake up.

**3. Kicking off work before leaving the office.** Before packing up for the day, start a session: "Refactor this service, write tests, and open a draft PR." Turn on remote mode. Close the laptop. On the train or bus home, answer any prompts from the phone. The next morning, the PR is waiting for review.

**4. Working across time zones.** One teammate is ending their day. Another is just starting theirs. The first can start a long task with `--remote`, share a quick handoff call to give context, and then sign off. The second can watch the session through the morning and help guide it. Approvals still go through the original user, but the work moves forward instead of sitting idle for 12 hours.

**5. Letting the PM watch a prototype get built.** During a product catch-up, open the session on a tablet and show it to the PM. When the agent asks a question — like whether something should be a dropdown or a modal — the PM can answer on the spot. No tickets, no back-and-forth emails, no rework a week later because the original choice was wrong.

**6. Teaching juniors how to use AI tools.** Run a real task in a conference room and put the session on a big screen. Junior engineers pull up the same session on their phones. They can see what prompts get used, how approvals and denials get decided, and what happens when the agent gets stuck. It's a much better way to learn than peeking over someone's shoulder at a terminal.

## What's good about it

Across all these stories, the same wins show up:

- **Your agent keeps working even when you step away.** Start a task, leave the room, answer prompts from anywhere.
- **No more dead sessions.** The agent doesn't sit for hours waiting for you to get back to your desk.
- **Your team can see what's happening.** PMs, junior devs, remote teammates — they can all watch without needing the same tools installed.
- **You can handle late-night problems from your phone.** No need to boot up a laptop at 2am.
- **Pairing feels natural again.** Decisions become a real conversation, not one person typing while others watch silently.
- **Meetings don't waste your work.** Start a task, go to a meeting, come back to progress.

## What it still can't do

This is a preview, so some things are worth knowing before you bet on it:

- **Only one person can drive a session.** Teammates can watch if you share your screen, but they can't take over. The person who started the session is the only one who can approve things. This is not real team collaboration yet.
- **The agent still runs on your computer.** If your laptop sleeps, dies, or loses Wi-Fi, the session dies too. `/keep-alive` helps but doesn't fix it. This is remote *control*, not remote *running*.
- **No shared history for teams.** You can't look back at a library of past agent sessions your team has run. Each session lives and dies with one person's account.
- **Getting admin approval can take a while.** If you're on Copilot Business or Enterprise, you need IT to turn on the right settings. In big companies, that can take weeks.
- **The agent uses your login, not the team's.** It has your file access, your GitHub permissions. You can't hand a session off to a teammate with different access mid-task.
- **Mobile apps are still in beta.** iOS and Android native apps work but have rough edges. Mobile browsers work fine for now.
- **More of your code leaves your machine.** The session sends activity to GitHub as it happens. Most teams are fine with this, but if you work on very sensitive code, read the docs first.
- **It's not the same as a cloud agent.** If you want an agent that runs on GitHub's servers while your laptop is off, that's Copilot's cloud agent — a different tool. This one is the middle ground between local and cloud.

## Where this is going

Copilot CLI, Claude Code, and similar tools all started as things you run only on your laptop. Remote control is the first big sign that "only local" was a limit, not a feature. If an agent is going to do 30 minutes of real work, you should be able to reach it from anywhere — because the whole point is that it works while you do something else.

GitHub is the first big name to ship this. Expect others to follow soon. Shared team sessions, session history you can search, and full cloud running are the obvious next steps.

## Try it yourself

`copilot --remote` is the kind of feature you don't realize you need until you use it once. Pick one real task — a test run, a refactor, a bug hunt — turn on remote mode, and steer from your phone while you do something else. Come back to finished work.

The workflow is very good. For the first time, using an AI coding agent feels like something that happens in the background of your day, instead of something that holds you hostage at your desk.

Worth trying.

---

*Tried it with your team? Drop a comment with what worked — and what didn't.*
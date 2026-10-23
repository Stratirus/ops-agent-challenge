# Stratirus Ops + Agent Challenge

We're looking for a junior-to-mid AI developer who also runs Linux. Instead of a resume screen, we ask interested people to do this challenge. Submitting it is how you apply and tell us you're interested. It doesn't guarantee an interview or a job offer.

Stratirus, a Tennetech company, is a small AI and Microsoft 365 consultancy in Franklin, TN. We build AI agents and automation for small and mid-sized businesses, mostly on Claude and Microsoft Copilot, and we run the Linux boxes underneath some of it.

## The role

- About 60% AI development: agents, MCP servers, Copilot Studio, Power Automate, Claude Code
- About 40% Linux administration: Ubuntu servers, systemd, Docker, patching, backups, monitoring
- Full-time or part-time
- Contract or direct hire, depending on fit
- Remote, US-based candidates only
- Occasional after-hours support as needed; no formal on-call rotation
- Pay: $65,000 to $100,000 per year, based on experience

Early-career and career-switchers are welcome. We care about how you work through a problem more than where you learned to do it.

## The challenge

### Setup

You need Docker on any machine: Linux, macOS (Intel or Apple silicon), or Windows with Docker Desktop.

Linux, macOS, or WSL:

```bash
docker pull ghcr.io/stratirus/opsbox:latest
docker run -d --name opsbox --hostname opsbox --privileged --cgroupns=host \
  --tmpfs /run --tmpfs /run/lock \
  -v /sys/fs/cgroup:/sys/fs/cgroup:rw ghcr.io/stratirus/opsbox:latest
docker exec -it opsbox bash
```

Windows PowerShell (one line):

```powershell
docker run -d --name opsbox --hostname opsbox --privileged --cgroupns=host --tmpfs /run --tmpfs /run/lock -v /sys/fs/cgroup:/sys/fs/cgroup:rw ghcr.io/stratirus/opsbox:latest
```

`--privileged` is there because the box runs systemd as a real init system. Run it on a machine you're comfortable using for a lab. Give it a couple of minutes after starting before you dig in.

To start over with a clean box: `docker rm -f opsbox`, then run it again.

`opsbox` is an Ubuntu 24.04 server running systemd. You're root inside it. A client reports three problems:

1. The `ledger-sync` service won't stay up.
2. The nightly report hasn't gone out in days.
3. Something is filling the disk.

That's all they know. You'll find the rest.

### What to do

1. **Fix the box.** Find the cause of each problem and fix it. Write your fixes as a script or Ansible playbook that we can run against a fresh `opsbox` and get a healthy server.
2. **Build an agent tool.** Write a small MCP server (any language) that lets Claude or Copilot check on this box. At minimum, expose `service_status` and `recent_errors`. Keep it read-only, and tell us why that matters.
3. **Write NOTES.md.** For each problem: what was wrong, how you found it, how you confirmed the fix worked. Then a section on AI: where it helped, where it was wrong, and how you caught it. [NOTES-template.md](NOTES-template.md) has a starting outline.

We'll test your fix script by running it against a fresh `opsbox` and checking the result, so make sure it works from a clean start.

### Time box

Plan on 2 to 4 hours. If you hit 4, stop and write up what you'd do next. The challenge is unpaid, so please don't spend more than that. A clear "here's where I got to and why" scores better than a finished box with no notes.

## Use AI

Use Claude, Copilot, ChatGPT, a local model, whatever you'd use on the job. We use them every day. What we're looking for is whether you check its work.

## How we grade

| Area | What we look for |
|---|---|
| Diagnosis | Found the actual cause, with evidence from logs or config |
| Verification | Proved each fix worked instead of assuming |
| Reproducibility | Your script fixes a fresh box with no manual steps |
| Agent tool | Works, read-only, sensible tool names and output |
| NOTES.md | Clear enough that a client's IT person could follow it |
| AI judgment | Honest about where the AI got it wrong |

## How to submit

1. Click **Use this template** at the top of this repo and create a **private** repo for your work. Please don't fork this repo publicly or post solutions.
2. Fill in the **About you** section at the top of your NOTES.md: name, contact email, US state, full- or part-time, contract or hire, availability, and expected rate.
3. Invite **[plausiblyhuman](https://github.com/plausiblyhuman)** as a collaborator. The invite is your submission.

We reply to every submission within 5 business days.

## What happens next

We review every submission. If yours is a fit for what we need, the next steps may include:

1. **Walkthrough call (30 to 45 minutes).** You walk us through your repo and we ask why you made the calls you did.
2. **A conversation about the role.**

Your challenge work stays yours. We use it only to evaluate your application.

## Questions

Open a GitHub issue on this repo. Answers are public so everyone gets the same information. Please don't ask for hints on the problems themselves.

For anything private, or if you need an accommodation to complete the challenge (more time, a different format), email [hiring@stratirus.com](mailto:hiring@stratirus.com).

---

Completing the challenge is not compensated and does not create an employment or contractor relationship or a promise of one. Stratirus, a Tennetech company, is an equal opportunity employer. We consider all qualified applicants without regard to race, color, religion, sex, sexual orientation, gender identity, national origin, age, disability, or veteran status.

This organization holds forks where
[@cgwalters-bot](https://github.com/cgwalters-bot), a semi-autonomous agent
account operated by Colin Walters ([@cgwalters](https://github.com/cgwalters)),
proposes changes for his review before anything goes upstream.

The bot pushes a tested branch to the fork here and opens a draft pull request
into the fork's `main` (or whatever upstream branch the change targets), written
as the future upstream PR. Colin comments on it or edits it directly, and the
bot addresses his review with more commits on the same branch. When he approves
it, with a review or a comment whose line is just `/promote`, the bot opens the
upstream PR from the same commits, with the same title and description (as a
draft if he also wrote a `/draft` line). If he closes it instead, it's dropped. The forks' own CI runs on
these PRs, so they get tested before anyone upstream sees them.

Nothing here is meant for upstream maintainers to review. More on how the bot
works is in its [profile](https://github.com/cgwalters-bot/cgwalters-bot) and in
[cgwalters-bot/homegit](https://github.com/cgwalters-bot/homegit), which has its
prompts and tooling. What it's working on is tracked on its
[project board](https://github.com/users/cgwalters-bot/projects/1). See also
Colin's [LLM policy](https://github.com/cgwalters#llms).

## How the bot's agents get inference

The agents run in sandboxed CI jobs that never hold a model provider's
credential, since a key inside the sandbox is one a prompt injection could
send anywhere, with no cap on what it spends. Instead, a credential broker
built on [Praxis AI](https://github.com/praxis-proxy/ai)
([praxis-credential-broker](https://github.com/cgwalters-bot/praxis-credential-broker))
holds the provider credentials and runs outside the jobs.

When a job starts it proves who it is to the broker, using the CI system's
short-lived identity token, and the broker's policy decides which workflows
may register. The broker then issues a token that is good for that run only.
The agent gets the broker's address and that token. Each request it makes
goes to the broker, which checks the token, adds the real credential,
forwards the request to the provider and counts what the run uses; each run
has its own cap. When the run ends, its token stops working. The broker's
usage counts also feed the bot's pacing, so work is held back when a budget
is running ahead of schedule.

The client side of this is in
[agentic-job's inference docs](https://github.com/cgwalters-forge/agentic-job/blob/main/docs/inference.md).
Nothing in the design is specific to this bot: any runner that can present
an identity the broker's policy admits can use it the same way.

If something from this organization is a problem for you, mention
[@cgwalters](https://github.com/cgwalters).

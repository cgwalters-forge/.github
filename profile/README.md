This organization holds forks where
[@cgwalters-bot](https://github.com/cgwalters-bot), a semi-autonomous agent
account operated by Colin Walters ([@cgwalters](https://github.com/cgwalters)),
proposes changes for his review before anything goes upstream.

The bot pushes a tested branch to the fork here and opens a draft pull request
into the fork's `main` (or whatever upstream branch the change targets), written
as the future upstream PR. Colin comments on it or edits it directly, and the
bot addresses his review with more commits on the same branch. When he approves,
the bot opens the upstream PR from the same commits, with the same title and
description. If he closes it instead, it's dropped. The forks' own CI runs on
these PRs, so they get tested before anyone upstream sees them.

Nothing here is meant for upstream maintainers to review. More on how the bot
works is in its [profile](https://github.com/cgwalters-bot/cgwalters-bot) and in
[cgwalters-bot/homegit](https://github.com/cgwalters-bot/homegit), which has its
prompts and tooling. What it's working on is tracked on its
[project board](https://github.com/users/cgwalters-bot/projects/1). See also
Colin's [LLM policy](https://github.com/cgwalters#llms).

If something from this organization is a problem for you, mention
[@cgwalters](https://github.com/cgwalters).

# Security policy

Report a vulnerability privately. Do not open a public issue, pull request or Discord
message about it.

## How to report

Use GitHub's private vulnerability reporting: on the affected repository, open
**Security**, then **Report a vulnerability**. If you cannot tell which repository is
affected, report it on [`playreliquia/.github`](https://github.com/playreliquia/.github/security/advisories/new).

Include what you found, how to reproduce it, and what an attacker gains. A maintainer
acknowledges the report within seven days and keeps you updated in the advisory.

## Scope

- The game client, dedicated server and Nakama plugin
  ([`reliquia`](https://github.com/playreliquia/reliquia)).
- The production infrastructure, including `nakama.playreliquia.com`,
  `status.playreliquia.com` and the rest of `playreliquia.com`
  ([`platform`](https://github.com/playreliquia/platform)).

Out of scope: denial-of-service testing against production, social engineering of the
team, and findings in third-party services we use rather than run.

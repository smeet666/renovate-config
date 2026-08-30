# renovate-config

The dependency rules the MCP servers share.

Each of them carries a `renovate.json` holding one line, so the rules live here
and a change to them reaches every server at once:

```json
{ "extends": ["github>smeet666/renovate-config"] }
```

## What the rules say

The toolchain moves as one piece, so a repository receives one pull request
rather than six, and the gate judges the set.

Two bounds hold what the gate cannot judge. The node types follow the oldest
node line the servers accept rather than the newest published, because typing
against a newer line lets an API that does not exist there compile clean. The
compiler stays below the line whose internals the declaration bundler cannot
read, and the rule says so, so that lifting it later needs no investigation.

A server that another server reads travels in its own pull request: it carries
behaviour rather than tooling.

A range moves its floor with the update. The published archive carries no
lockfile, so the range a manifest declares is what a consumer resolves against,
and it states which versions the package accepts to run. A floor left behind
names a version that would be refused, and a scanner reading the manifest
reports that floor rather than what installs.

A development tool is pinned to one version. It reaches no consumer tree, so an
exact version duplicates nothing, and the toolchain is then identical on every
machine and every run.

Anything that passes the gate is merged. The gate is the lint verdict, three
identical passes of the suite on two node versions, the build, and the container
image built and started.

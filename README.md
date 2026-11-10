# factory

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/thomas-lg-lab/factory/badge)](https://scorecard.dev/viewer/?uri=github.com/thomas-lg-lab/factory)

Creates the organisation's repositories, so that nobody but the owners needs the right to create one or to change
its settings. Members (people and the machine account) dispatch **Create repository** with a name and a
description; the workflow, acting as the organisation's factory App:

1. checks the name (lowercase letters, digits, dashes; never ending in `-lab`) and that the repository does not exist;
2. creates it, public, from [`repo-template`](https://github.com/thomas-lg-lab/repo-template);
3. runs `apply-standards.sh` from [`.github`](https://github.com/thomas-lg-lab/.github) at a pinned release:
   settings, security features, CodeQL default setup, immutable releases, labels and the template's rulesets.

```bash
gh workflow run create-repository.yml -R thomas-lg-lab/factory -f name=<name> -f description="<one line>"
```

The App holds Administration write, Issues write and Contents read on the organisation's repositories, and
nothing at the organisation level. Its Client ID is the variable `FACTORY_APP_CLIENT_ID`, its private key the secret
`FACTORY_APP_PRIVATE_KEY`. Deleting or archiving a repository stays with the owners.

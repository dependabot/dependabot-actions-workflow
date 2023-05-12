# Archived / Deprecated
Dependabot PR's used to run with [read-only permissions](https://github.blog/changelog/2021-02-19-github-actions-workflows-triggered-by-dependabot-prs-will-run-with-read-only-permissions/), so this example repository demonstrated how to update Dependabot pull requests without direct read-write/secrets access.

However, GitHub Actions now allow direct writes on Dependabot PR's, so this complicated workaround is no longer necessary. Instead, see the docs for [simpler solutions to updating your Dependabot PR's](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/automating-dependabot-with-github-actions).

This repo is kept around in archived form in case folks linked to it from other places.

----

## Workflows

The `Build Dependabot Bundler PR` workflow runs on all pushes to `dependabot/bundler**` branches with a read-only `GITHUB_TOKEN`. This action gets triggered when Dependabot opens new pull requests or force-pushes updates to existing pull requests.

This action will run a `bundle install` without write access to the repository as this can execute potentially unsafe third-party ruby code when installing
git dependencies.

The completion of this workflow triggers the `Update Dependabot Bundler PR` workflow which has a read-write `GITHUB_TOKEN`, extracting the changes to license files and pushing these to back to the Dependabot PR branch.

Read more about [keeping your GitHub Actions and workflows secure](https://securitylab.github.com/research/github-actions-preventing-pwn-requests).

# Hacktoberfest Action
## _Merge pull request with ease_

This is a github action made by using and customizing the [pr-labeler](https://github.com/marketplace/actions/pr-labeler) github action by TimonVS from the github actions marketplace.

## Features

- Add labels to pull request with matching patterns in branch-name. 
- Automatically adds the lables once the PR is merged.
- The current matching pattern for branchname is 'hack/*' but one can customise it by editing the 'pr-labeler.yml' file in .github folder.
- Easy to Use
- Automates the task of adding labels manually to a PR while merging during Hacktoberfest

## Usage

Add `.github/workflows/pr-labeler.yml` with the following:

```yml
name: PR Labeler
on:
  pull_request:
    types: [closed]

jobs:
  pr-labeler:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - uses: TimonVS/pr-labeler-action@v3
        with:
          configuration-path: .github/pr-labeler.yml # optional, .github/pr-labeler.yml is the default value
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Configuration

Configure by creating a `.github/pr-labeler.yml` file.

For example:

```yml
hacktoberfest: 'hack/*'
hacktoberfest-accepted: 'hack/*'
```

Then if a pull request is merged and closed with the branch name `hack/218-add-emoji-support` the Action will automatically apply the `hacktoberfest` and `hacktoberfest-acccepted` label once the PR is merged.

### Wildcard branches in configuration

You can use `*` as a wildcard for matching multiple branch names. See https://www.npmjs.com/package/matcher for more information about wildcard options.

### Default configuration

When no configuration is provided, the following defaults will be used:

```yml
hacktoberfest: 'hack/*'
hacktoberfest-accepted: 'hack/*'
```

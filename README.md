# flutter-prepare-action

## Usage

```yaml
- uses: ueno-tecnologia-org/flutter-prepare-action@v1
  with:
    flutter-version: '1.12.13+hotfix.5-stable' # default: latest
    format-exits-if-changed: true | false # default: false. If true, the action will exit with code 1 if there are any files that need to be formatted.
    github-token: ${{ secrets.GITHUB_TOKEN }} # required
    update-coverage-comment: true | false # default: false. If true, the action will update the coverage comment in the PR.
```
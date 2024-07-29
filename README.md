# flutter-prepare-action

## Usage

```yaml
- uses: ueno-tecnologia-org/flutter-prepare-action@v1
  with:
    flutter-version: '1.12.13+hotfix.5-stable' # default: latest
    format-exits-if-changed: true | false # default: false. If true, the action will exit with code 1 if there are any files that need to be formatted.
    github-token: ${{ secrets.GITHUB_TOKEN }} # required
    update-coverage-comment: true | false # default: false. If true, the action will update the coverage comment in the PR.
    use_melos: true #default: false. If true, the action will use melos to run the flutter commands

```


## Using Melos with the Action

To use Melos with this GitHub Action, you need to set the use_melos input to true. This will ensure that Melos commands are used instead of the default Flutter commands. Additionally, you must have a melos.yaml file in your repository's root directory.

**Example** `melos.yaml`

Here is an example of what your `melos.yaml` file might look like:

```
name: MyProjectName

packages:
  - .
  - packages/**
  - micro_app

scripts:
  format:
    exec: dart format --line-length=80 --set-exit-if-changed .
  gen:
    exec: dart run build_runner build --delete-conflicting-outputs
  loc:
    exec: dart gen-l10n
  analyze:
    exec: flutter analyze .
  test:
    exec: flutter test
  test_coverage:
    exec: flutter test --coverage

```

**Action Configuration**

In your GitHub Actions workflow file, set the `use_melos` input to `true`:

```yaml
- uses: ueno-tecnologia-org/flutter-prepare-action@v1
  with:
    flutter-version: '1.12.13+hotfix.5-stable' # default: latest
    format-exits-if-changed: true | false # default: false. If true, the action will exit with code 1 if there are any files that need to be formatted.
    github-token: ${{ secrets.GITHUB_TOKEN }} # required
    update-coverage-comment: true | false # default: false. If true, the action will update the coverage comment in the PR.
    use_melos: true #default: false
```

By setting `use_melos` to `true`, the action will use Melos for bootstrapping, formatting, analyzing, and running tests as defined in your `melos.yaml` file.
# Bump Please Github Action 🤜💥🤛

Use [Bump Please](https://github.com/chriswoodle/bump-please) to automatically bump package.json versions on git commits or releases.

For configuration, see [Bump Please](https://github.com/chriswoodle/bump-please)


# Usage

1. Set write permission. This allows the action to preform write git actions back to the repo.
```yaml
permissions:
  contents: write
```

2. Set `fetch-depth 0` and `fetch-tags: true`. This allows the action to access all git tags.
```yaml
uses: actions/checkout@v6
with:
  fetch-depth: 0
  fetch-tags: true
```

> This may be slow for large repositories. See https://github.com/actions/checkout/issues/1471

3. Configure Bump Please.
```yaml
- name: 🤜 Bump Please
  uses: chriswoodle/bump-please-action@v1.1.2
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Example

Version bump on every git commit:

```yaml
name: Version Bump

permissions:
  contents: write

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  build-and-bump:
    runs-on: ubuntu-latest
    steps:
    - name: 🏗 Setup repo
      uses: actions/checkout@v6
      with:
        fetch-depth: 0
        fetch-tags: true

    - name: 🏗 Setup Node
      uses: actions/setup-node@v6
      with:
        node-version: 24
        
    - name: 📦 Install Project dependencies
      run: npm install
      
    - name: 🏗️ Build App
      run: npm run build
                
    - name: 🤜 Bump Please
      uses: chriswoodle/bump-please-action@v1.1.2
      with:
        github-token: ${{ secrets.GITHUB_TOKEN }}
```
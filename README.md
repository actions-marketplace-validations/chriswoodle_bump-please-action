# bump-please-action


# Usage

1. Set write permission. This allows the action to preform write git actions back to the repo.
```yaml
permissions:
  contents: write
```

2. Set fetch-depth 0. This allows the action to access full git history
```yaml
uses: actions/checkout@v4
with:
  fetch-depth: 0
```

3. Configure Bump Please.
```yaml
- name: 🤜 Bump Please
  uses: chriswoodle/bump-please-action@v1.0.0
  with:
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Example
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
      uses: actions/checkout@v4
      with:
        fetch-depth: 0

    - name: 🏗 Setup Node
      uses: actions/setup-node@v3
      with:
        node-version: 22.x
        
    - name: 📦 Install Project dependencies
      run: npm install
      
    - name: 🏗️ Build App
      run: npm run build
                
    - name: 🤜 Bump Please
      uses: chriswoodle/bump-please-action@v1.0.0
      with:
        github-token: ${{ secrets.GITHUB_TOKEN }}
```
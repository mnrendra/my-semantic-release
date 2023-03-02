# my-semantic-release
My semantic release  

## Steps
• Create GitHub **public** repository  
• `npm init`  
• update `package.json` to add `"private": false`  
• add `index.js`:
```
module.exports = {
  hello: () => console.log('hello world!')
}
```  
• `commitizen init cz-conventional-changelog --save-dev --save-exact`  
• add `package.json` scripts `"commit": "npx cz"`  
• `npx semantic-release-cli setup`  
• add `.releaserc`  
```
{
  "branches": ["main"]
}
```  
• add `.github/workflows/release.yml`:  
```
name: Release
on:
  push:
    branches:
      - main
jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "lts/*"
      - name: Install dependencies
        run: npm ci
      - name: Release
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
        run: npx semantic-release
```  
• `npm i`  
• `git add .`  
• `npm run commit`  
• `git push`

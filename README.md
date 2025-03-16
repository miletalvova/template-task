# Template Project task with Prettier, ESLint, Husky and lint-staged **

## _Project overview_

This project is a tempalte for setting up a new repository with the development tools. It inclides version control GitHub, formatting tolls Prettier, linting with ESLint, and automation with Husky and lint-staged.

## _1. Cloning the repository_

Clone this repository to your local machine to start working on it.

## _2. Initialising the project_

```
npm init -y
```

## _3. Installing ESLint and Prettier_

```
npm install --save-dev prettier eslint@8.56.0 eslint-config-prettier eslint-plugin-prettier eslint-config-airbnb-base eslint-plugin-import
```
Generate an ESlint config file
```
npx eslint init
```

Change your .eslintrc-cjs configurations:
```
module.exports = {
  extends: ['airbnb-base', 'prettier'],
  plugins: ['prettier'],
  rules: { 'prettier/prettier': 'error' },
};
```

Setup lint script in your package.json file:
```
"lint": "eslint . --fix"
```
Create a .prettierrc file and add the following:
```
{
  "singleQuote": true,
  "endOfLine": "lf"
 }
```
Create a .prettierignore and add the following:
```
node_modules/
.github/

.babelrc
.eslintrc.js
.eslintrc.cjs
.gitignore
.prettierrc

package-lock.json
package.json

README.md
```
## _4. Husky and lin-staged istalling and configuration_

```
npm install --save-dev husky lint-staged
```

Create and configure a .husky directory
```
npx husky init
```
Run the following command to create pre-commit hook
```
echo "npx lint-staged" > .husky/pre-commit
```

The pre-commit file should look as following:
```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```
_Add the script above to your pre-commit file if it differs from the one above_

```
In your package.json add the following code to run ESLint and Prettier on our JavaScript files:

```
"lint-staged": {
  "*.js": [
    "eslint --fix",
    "prettier --write",
  ]
}
```

git add .
git commit -m "Initial commit"
git push
```
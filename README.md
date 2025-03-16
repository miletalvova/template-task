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

Add a script in package.json to call Prettier to format our code:
```

"format": "prettier --check ."
```
## _4. Husky and lint-staged istalling and configuration_

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
_Add the script above to your pre-commit file if it differs from the one above._

In your package.json add the following code to run ESLint and Prettier on our JavaScript files:

```
"lint-staged": {
  "*.js": [
    "eslint --fix",
    "prettier --write",
  ]
}
```

## _5. Configuring Jest for testing_

Run the following command to install jest dependencies
```
npm install --save-dev jest
```
Add a script in package.json to run our tests:
```
"test": "jest"
```

Create a file called math.js and add the following code, which is a basic function that adds two values:
```
/* eslint-disable import/prefer-default-export */
function addNumbers(a, b) {
 return a + b;
}

export { addNumbers };
```
Create a file called math.test.js and add the following code:
```

import { addNumbers } from './math';

test('adds 1 + 2 to equal 3', () => {
  expect(addNumbers(1, 2)).toBe(3);
```
## _6. .gitignore_
Create a .gitignore file and add node_modules to it.
```

node_modules/
```

## _7. Creating the GitHub Action workflow_
- Create a .github/workflows directory in the root of your project.
- Add the following config to your main.yml file:
```
name: JavaScript Workflow

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js
        uses: actions/setup-node@v1
        with:
          node-version: '20'
      - name: Install dependencies
        run: npm install
      - name: Run Prettier
        run: npm run format
      - name: Run ESLint
        run: npm run lint
      - name: Run tests
        run: npm run test
```

## _8. Finally push your code_
```

git add .
git commit -m "Initial commit"
git push
```
# Pre-commit Hooks Setup for Linting and Formatting with Husky, lint-staged, Prettier, and ESLint

1. Download lint-staged and Prettier using npm i command:

   ```bash
   npm i lint-staged prettier --save-dev
   ```

2. First, install by setting up the initial ESLint config file:

   ```bash
   npx init eslint/config
   ```

   After the file is installed, you will find it in the root directory as `.eslintrc.js`.

3. Set up lint-staged in package.json:

   ```json
   "lint-staged": {
     "./**/*.js": [
       "prettier --write",
       "eslint --fix"
     ]
   }
   ```

   This configuration ensures that Prettier and ESLint will only be applied to staged changes and not the whole repository.

4. To check if the formatting and linting are set up properly, make small insignificant changes, stage them (using `git add -A`), and run the command:

   ```bash
   npx lint-staged
   ```

   If everything written in the editor is properly formatted and no mistakes are made, no error will be thrown.

## Setting up Husky for pre-commit hooks

Now, let's set up Husky to add the lint-staged command in Git hooks as pre-commit hooks.

1. Install Husky as a devDependency in your project:

   ```bash
   npm install husky --save-dev
   ```

2. Initialize Husky:

   ```bash
   npx husky install
   ```

3. Create a Husky configuration file by adding the following script to your `package.json` file:

   ```json
   "husky": {
     "hooks": {
       "pre-commit": "npx lint-staged"
     }
   }
   ```

   This configuration tells Husky to execute the `lint-staged` command before every commit.

4. Verify the Setup: Make a new change to your code, stage it (using `git add -A`), and then attempt to commit the changes:

   ```bash
   git commit -m "Your commit message"
   ```

   If everything is set up correctly, Husky will run `lint-staged`, which in turn will handle linting and formatting before the commit is finalized.

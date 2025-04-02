# Create React project with Vite

- npm create vite@latest
- cd vite-project-name
- npm install

# Install husky, eslint, lint-staged, and prettier and their dependencies

- npm install --save-dev husky eslint prettier lint-staged eslint-config-prettier eslint-plugin-prettier eslint-plugin-react

# Create a .eslint.json file at the root of the project, then add the following properties.

```
    {
        "env": {
            "browser": true,
            "es2021": true
        },
        "extends": [
            "eslint:recommended",
            "plugin:react/recommended",
            "plugin:prettier/recommended"
        ],
        "parserOptions": {
            "ecmaFeatures": {
            "jsx": true
            },
            "ecmaVersion": 12,
            "sourceType": "module"
        },
        "plugins": [
            "react",
            "prettier"
        ],
        "rules": {
            "react/react-in-jsx-scope": "off"
        },
        "settings": {
            "react": {
            "version": "detect"
            }
        },
        "overrides": [
            {
                "files": ["*.js", "*.jsx"]
            }
        ]
    }
```

# Create a new .eslintignore file, with the following contents:

```
    dist/
    vite.config.js
```

The node_modules/ folder is automatically ignored by ESLint.

# Create a .prettierrc file at the root of our project.

```
    {
        "semi": true,
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 2
    }
```

# Create a new file called .prettierignore in the root of our project.

Add the following contents to it to ignore the transpiled source code:

```
    dist
```

The node_modules/ folder is automatically ignored by Prettier.

# Run following command in your terminal to setup Husky

```
    npx husky init
```

- This will create a .husky folder, with a pre-commit file that runs on every commit we make. There will be an “npm test” code in the pre-commit file. Since we don’t have any test, let us replace it to run our lint-staged.

```
    npx lint-staged
```

# Update package.json to add husky and lint-staged as properties:

```
  "lint-staged": {
    "src/**/*.(ts|tsx|js|jsx)": [
      "prettier --write"
    ],
    "src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json)": [
      "prettier --write"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
```

- So our package.json looks like:

```
{
    "name": "vite-react-eslint-prettier-husky",
    "private": true,
    "version": "0.0.0",
    "type": "module",
    "scripts": {
        "dev": "vite",
        "build": "vite build",
        "lint": "eslint .",
        "preview": "vite preview",
        "prepare": "husky"
    },
    "lint-staged": {
        "src/**/*.(ts|tsx|js|jsx)": [
            "prettier --write"
        ],
        "src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json)": [
            "prettier --write"
        ]
    },
    "husky": {
        "hooks": {
            "pre-commit": "lint-staged"
        }
    },
    "dependencies": {
        "react": "^19.0.0",
        "react-dom": "^19.0.0"
    },
    "devDependencies": {
        "@commitlint/cli": "^19.8.0",
        "@commitlint/config-conventional": "^19.8.0",
        "@eslint/js": "^9.21.0",
        "@types/react": "^19.0.10",
        "@types/react-dom": "^19.0.4",
        "@vitejs/plugin-react-swc": "^3.8.0",
        "eslint": "^9.23.0",
        "eslint-config-prettier": "^10.1.1",
        "eslint-plugin-prettier": "^5.2.5",
        "eslint-plugin-react": "^7.37.4",
        "eslint-plugin-react-hooks": "^5.1.0",
        "eslint-plugin-react-refresh": "^0.4.19",
        "globals": "^15.15.0",
        "husky": "^9.1.7",
        "lint-staged": "^15.5.0",
        "prettier": "^3.5.3",
        "vite": "^6.2.0"
    }
}
```

# Run npm run prepare to set up the hooks in husky

```
    npm run prepare
```

# Test our setup by making a commit.

- Note: For the first commit, we need to add “npm run prepare”, after initializing git in our project, to initialize git hooks in husky. Subsequent commits do not require the “npm run prepare” command.

```
    git init
    npm run prepare //only for the very first commit
```

- Output

```
        > vite-react-eslint-prettier-husky@0.0.0 prepare
        > husky
```

```
    git add .
    git commit -m "set up"
```

- Output

```
        ⚠ Skipping backup because there’s no initial commit yet.

        [STARTED] Preparing lint-staged...
        [COMPLETED] Preparing lint-staged...
        [STARTED] Running tasks for staged files...
        [STARTED] package.json — 16 files
        [STARTED] src/**/*.(ts|tsx|js|jsx) — 2 files
        [STARTED] src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json) — 3 files
        [STARTED] prettier --write
        [STARTED] prettier --write
        [COMPLETED] prettier --write
        [COMPLETED] src/**/*.(ts|tsx|js|jsx) — 2 files
        [COMPLETED] prettier --write
        [COMPLETED] src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json) — 3 files
        [COMPLETED] package.json — 16 files
        [COMPLETED] Running tasks for staged files...
        [STARTED] Applying modifications from tasks...
        [COMPLETED] Applying modifications from tasks...
        [master (root-commit) b222d71] set up
        16 files changed, 5413 insertions(+)
        create mode 100644 .eslint.json
        create mode 100644 .gitignore
        create mode 100644 .husky/pre-commit
        create mode 100644 .prettierrc
        create mode 100644 README.md
        create mode 100644 eslint.config.js
        create mode 100644 index.html
        create mode 100644 package-lock.json
        create mode 100644 package.json
        create mode 100644 public/vite.svg
        create mode 100644 src/App.css
        create mode 100644 src/App.jsx
        create mode 100644 src/assets/react.svg
        create mode 100644 src/index.css
        create mode 100644 src/main.jsx
        create mode 100644 vite.config.js
```

# Make some changes in any file, then commit the changes. We don’t need to run “npm run prepare” anymore.

```
    git add .
    git commit -m "made some changes"
```

- Output

```
    [STARTED] Backing up original state...
    [COMPLETED] Backed up original state in git stash (6278262)
    [STARTED] Running tasks for staged files...
    [STARTED] package.json — 1 file
    [STARTED] src/**/*.(ts|tsx|js|jsx) — 1 file
    [STARTED] src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json) — 0 files
    [SKIPPED] src/**/*.(json|css|scss|md)|.(babelrc|prettierrc|eslint.js|tsconfig.json) — no files
    [STARTED] prettier --write
    [COMPLETED] prettier --write
    [COMPLETED] src/**/*.(ts|tsx|js|jsx) — 1 file
    [COMPLETED] package.json — 1 file
    [COMPLETED] Running tasks for staged files...
    [STARTED] Applying modifications from tasks...
    [COMPLETED] Applying modifications from tasks...
    [STARTED] Cleaning up temporary files...
    [COMPLETED] Cleaning up temporary files...
    [master 6b77195] made some changes
    1 file changed, 1 insertion(+), 1 deletion(-)
```

# Setting up commitlint to enforce a standard for our commit messages

- In addition to linting our code, we can also lint our commit messages. You may have noticed that we were prefixing our commit messages with a type already (the chore type). Types make it easier to follow what was changed in a commit. To enforce the use of types, we can set up commitlint.
- Follow these steps to set it up

- Install commitlint and a conventional config for commitlint:

```
    npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

- Create a new .commitlintrc.json file in the root of our project and add the
  following contents:

```
    {
        "extends": ["@commitlint/config-conventional"]
    }
```

- Create commit-msg file under .husky folder and add the line below to add a commit-msg hook to Husky:

```
    npx commitlint --edit "$1"
```

- Now, if we try adding our changed files and committing without a type or a wrong type, we will get an error from commitlint and will not be able to make such a commit. If we add the correct type, it will succeed:

```
    git add .
```

- The following figure shows Husky in action. If we write an incorrect commit message, it will reject it and not let us commit the code.

```
    git commit -m "no type"
```

- Output

```
    → No staged files match any configured task.
    ⧗   input: no type
    ✖   subject may not be empty [subject-empty]
    ✖   type may not be empty [type-empty]

    ✖   found 2 problems, 0 warnings
    ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

    husky - commit-msg script failed (code 1)
```

- The following figure shows Husky in action. If we write an incorrect commit message, it will reject it and not let us commit the code.

```
    git commit -m "wrong: type"
```

- Output

```
    → No staged files match any configured task.
    ⧗   input: wrong: type
    ✖   type must be one of [build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test] [type-enum]

    ✖   found 1 problems, 0 warnings
    ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

    husky - commit-msg script failed (code 1)
```

- Only if we enter a properly formatted commit message will the commit go through

```
    git commit -m "chore: configure commitlint"
```

- Output

```
    → No staged files match any configured task.
    [master 1a19c6e] chore: configure commitlint
    4 files changed, 6269 insertions(+), 5085 deletions(-)
    create mode 100644 .commitlintrc.json
    create mode 100644 .husky/commit-msg
```

# Commit messages

- Commit messages in the commitlint conventional config (https://www.conventionalcommits.org/) are structured in a way where a type must be listed first, then an optional scope follows, and then the description follows, such as type(scope): description.

- Possible types are as follows:

```
 • fix: For bug fixes
 • feat: For new features
 • refactor: For restructuring the code without adding features or fixing bugs
 • build: For changes in the build system or dependencies
 • ci: For changes in the CI/CD configuration
 • docs: For changes in the documentation only
 • perf: For performance optimizations
 • style: For fixing code formatting
 • test: For adding or adjusting tests
```

The scope is optional and best used in a monorepo to specify that changes were made to a certain app or library within it

# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript and enable type-aware lint rules. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.

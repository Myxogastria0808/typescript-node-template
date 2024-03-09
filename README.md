## typeScript の環境構築 (Node.js)

```batch
yarn init
yarn add -D ts-node-dev typescript eslint-config-prettier @types/node
npm init @eslint/config
yarn tsc --init
wsl touch .prettierrc
wsl touch .eslintignore
mkdir dist
mkdir src
cd src
wsl touch index.ts
```

### `yarn tsc --init`

```text
√ How would you like to use ESLint? · problems
√ What type of modules does your project use? · commonjs
√ Which framework does your project use? · none
√ Does your project use TypeScript? · No / Yes
√ Where does your code run? · browser
√ What format do you want your config file to be in? · JavaScript
Local ESLint installation not found.
The config that you've selected requires the following dependencies:

@typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest eslint@latest
√ Would you like to install them now? · No / Yes
√ Which package manager do you want to use? · yarn
```

## `package.json`

```json
{
    "scripts": {
        "dev": "ts-node-dev --respawn ./src/index.ts",
        "start": "node dist/index.js",
        "compile": "tsc -p ."
    }
}
```

## `tsconfig.json`

```json
{
    "compilerOptions": {
        "target": "es2021",
        "module": "commonjs",
        "baseUrl": "./",
        "outDir": "./dist",
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "strict": true,
        "skipLibCheck": true
    }
}
```

## `.prettierrc`

```json
{
    "printWidth": 120,
    "tabWidth": 4,
    "singleQuote": true,
    "trailingComma": "es5",
    "semi": true
}
```

## `.eslintrc.cjs`

```javascript
module.exports = {
    root: true,
    env: {
        browser: true,
        commonjs: true,
        node: true,
        es2021: true,
    },
    extends: ['eslint:recommended', 'plugin:@typescript-eslint/recommended', 'prettier'],
    overrides: [
        {
            env: {
                node: true,
            },
            files: ['.eslintrc.cjs'],
            parserOptions: {
                sourceType: 'script',
            },
        },
    ],
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaVersion: 'latest',
    },
    plugins: ['@typescript-eslint'],
    rules: {
        semi: ['error', 'always'],
        quotes: ['error', 'single'],
    },
};
```

## `.eslintignore`

```text
node_modules

```

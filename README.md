# @threls/eslint-config

To install run
```
yarn add -D @threls/eslint-config
```
or 
```
npm i -D @threls/eslint-config
```

This package will require `eslint` and `prettier` be installed as peer dependencies
```
yarn add -D eslint prettier
```

Finally you need to add a config file `eslint.config.mjs`

```js
import path from 'node:path';
import { fileURLToPath } from 'node:url';
import js from '@eslint/js';
import { FlatCompat } from '@eslint/eslintrc';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
const compat = new FlatCompat({
  baseDirectory: __dirname,
  recommendedConfig: js.configs.recommended,
  allConfig: js.configs.all,
});

export default [
  {
    ignores: ['**/node_modules', '**/dist'],
  },
  ...compat.extends('@threls/eslint-config/react-native'),
  {
    languageOptions: {
      ecmaVersion: 5,
      sourceType: 'script',

      parserOptions: {
        project: 'tsconfig.json',
      },
    },
  },
];

```

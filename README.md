# vue3-ts前端工程化

在vue3+ts项目中使用eslint+stylint+prettier实现代码格式

参考文章
```
https://juejin.cn/post/7069315908597973023#heading-19
```

### eslint
使用vue-cli初始化项目时选择eslint作为代码检查工具，package.json中会自动安装相关依赖
```
"@typescript-eslint/eslint-plugin": "^5.4.0",
"@typescript-eslint/parser": "^5.4.0",
"@vue/cli-plugin-babel": "~5.0.0",
"@vue/cli-plugin-eslint": "~5.0.0",
"@vue/cli-plugin-router": "~5.0.0",
"@vue/cli-plugin-typescript": "~5.0.0",
"@vue/cli-plugin-vuex": "~5.0.0",
"@vue/cli-service": "~5.0.0",
"@vue/eslint-config-typescript": "^9.1.0",
"eslint": "^7.32.0",
"eslint-plugin-vue": "^8.0.3",
"sass": "^1.32.7",
"sass-loader": "^12.0.0",
"typescript": "~4.5.5"
```
配置.eslintrc.js和.eslintignore
```
<!-- .eslintrc.js -->
module.exports = {
  root: true,
  env: {
    node: true,
    browser: true
  },
  extends: ['plugin:vue/vue3-essential', 'eslint:recommended', '@vue/typescript/recommended'],
  parserOptions: {
    ecmaVersion: 2020
  },
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    '@typescript-eslint/no-unused-vars': 'error',
    // 允许非空断言
    '@typescript-eslint/no-non-null-assertion': 'off',
    // 允许自定义模块和命名空间
    '@typescript-eslint/no-namespace': 'off',
    // 允许对this设置alias
    '@typescript-eslint/no-this-alias': 'off',
    // 允许使用any类型
    '@typescript-eslint/no-explicit-any': ['off']
  }
}

<!-- .eslintignore -->
/dist/
/*.js
/public/
/node_modules/
```

eslint的rules其他配置规则可以参考下面的(具体意思需要参照eslint官网)
```
'use strict'
module.exports = {
  configs: {
    recommended: {
      extends: [
        'plugin:vue/recommended',
        'plugin:sonarjs/recommended',
        'prettier'
      ],
      plugins: ['import'],
      rules: {
        'vue/require-default-prop': 0,
        'vue/attributes-order': [
          1,
          {
            alphabetical: true
          }
        ],
        'vue/no-v-html': 0,
        'vue/component-options-name-casing': 1,
        'vue/custom-event-name-casing': 1,
        'vue/no-multiple-objects-in-class': 2,
        'vue/no-this-in-before-route-enter': 2,
        'vue/padding-line-between-blocks': 1,
        'vue/prefer-separate-static-class': 2,
        'vue/static-class-names-order': 1,
        'vue/v-on-function-call': 2,
        'vue/multi-word-component-names': 0,
        'vue/no-unused-components': 1,
        'vue/no-unused-vars': 1,

        'import/newline-after-import': 1,

        'sonarjs/cognitive-complexity': [2, 80],
        'sonarjs/max-switch-cases': [2, 30],
        'sonarjs/no-duplicate-string': 0,
        'sonarjs/no-duplicated-branches': 1,
        'sonarjs/no-extra-arguments': 0,
        'sonarjs/no-ignored-return': 1,
        'sonarjs/no-nested-switch': 0,
        'sonarjs/no-unused-collection': 1,
        'sonarjs/no-empty-collection': 1,
        'sonarjs/no-identical-functions': 1,
        'sonarjs/no-small-switch': 0,
        'sonarjs/prefer-immediate-return': 0,
        'sonarjs/prefer-object-literal': 0,
        'sonarjs/prefer-single-boolean-return': 1,

        'no-use-before-define': [
          2,
          { functions: false, classes: true, variables: true }
        ],
        'no-template-curly-in-string': 2,
        'no-unused-vars': [
          1,
          {
            vars: 'all',
            args: 'none',
            caughtErrors: 'none',
            ignoreRestSiblings: true
          }
        ],
        'no-empty': [2, { allowEmptyCatch: true }],
        'no-debugger': process.env.NODE_ENV === 'production' ? 2 : 0,
        'no-var': 1,
        'no-case-declarations': 0,
        'no-prototype-builtins': 0,
        'no-async-promise-executor': 0,
        'array-callback-return': 2,
        'no-void': 0,
        'no-useless-escape': 0,
        'prefer-promise-reject-errors': 0,
        'dot-notation': 0,
        'prefer-const': [
          1,
          {
            destructuring: 'all'
          }
        ],
        'lines-between-class-members': 1,
        'multiline-ternary': 0,

        'max-lines-per-function': [
          2,
          {
            max: 220,
            skipBlankLines: true,
            skipComments: true
          }
        ],
        'max-nested-callbacks': [1, 3],
        'max-depth': [1, 5],
        'max-params': [1, 7],
        'require-atomic-updates': 0
      }
    }
  }
  // rules: requireIndex(__dirname + '/rules')
}
```

如果安装了vscode的prettier插件，为了避免和eslint的冲突，需要添加.prettierrc配置文件
```
{
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "semi": false,
  "singleQuote": true,
  "quoteProps": "as-needed",
  "jsxSingleQuote": false,
  "trailingComma": "none",
  "bracketSpacing": true,
  "bracketSameLine": false,
  "arrowParens": "always",
  "endOfLine": "lf"
}
```

### stylelint

安装依赖(安装完毕后需要重启vscode)
```
"lint-staged": "^12.3.5",
"postcss": "^8.4.8",
"postcss-html": "^1.3.0",  // stylelint-config-html需要postcss-html
"postcss-scss": "^4.0.3", // 格式化样式文件需要
"stylelint": "^14.5.1",
"stylelint-config-html": "^1.0.0",
"stylelint-config-recess-order": "^3.0.0", // 主要用来修改css样式编写顺序
"stylelint-config-recommended": "^7.0.0",
```

配置.stylelint.js和.stylelintignore
```
module.exports = {
  extends: [
    "stylelint-config-recommended",
    "stylelint-config-recess-order",
    "stylelint-config-html",
  ],
  // 针对后缀为这些文件的使用postcss-scss格式化
  overrides: [
    {
      files: ["*.sass", "*.scss", "**/*.sass", "**/*.scss"],
      customSyntax: "postcss-scss",
    },
  ],
  rules: {
    "at-rule-no-unknown": null,
    "no-descending-specificity": null,
    "function-no-unknown": null,
    "font-family-no-missing-generic-family-keyword": null,
    // "stylus/at-extend-style": ["@extend"],
    // "stylus/declaration-colon": ["always"],
    // "stylus/hash-object-property-comma": [
    //   "always",
    //   {
    //     trailing: "never",
    //   },
    // ],
    // "stylus/indentation": 2,
    // indentation: null,
    // "stylus/media-feature-colon": ["always"],
    // "stylus/no-at-require": [true],
    // "stylus/pythonic": [
    //   "never",
    //   {
    //     atblock: "never",
    //   },
    // ],
    // "stylus/selector-list-comma": ["always"],
    // "stylus/semicolon": ["always"],
    // "stylus/single-line-comment": ["never"],
  },
  defaultSeverity: "warning",
};

<!-- .stylelintignore -->
*.js
*.ts
*.jpg
*.woff
/dist/
/node_modules/
```


### 问题记录
**Q:**
Unknown word (CssSyntaxError)错误

**A:**
没有安装postcss插件(安装完毕后需要重启vscode)
```
"postcss": "^8.4.8",
"postcss-html": "^1.3.0",
"postcss-scss": "^4.0.3",
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

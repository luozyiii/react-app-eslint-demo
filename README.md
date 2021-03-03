# 统一代码风格的 react 项目

## 技术栈

##### create-react-app + eslint-config-alloy(有更好的可替换) + Prettier + vscode

我倾向于让 ESLint 去判断逻辑(代码正误，语法校验)，让 Prettier 去判断样式。
这种解耦也可以让整体逻辑更清晰，所以，两者都需要，一个也不能少。

## 使用 ceate-react-app 创建基础项目

http://www.html.cn/create-react-app/docs/getting-started/

```
npx create-react-app react-app-eslint-demo
cd react-app-eslint-demo
npm start
```

## 使用 eslint-config-alloy 配置

> node 版本需在 12.0.0 以上

https://github.com/AlloyTeam/eslint-config-alloy/blob/HEAD/README.zh-CN.md

### 安装依赖

yarn add eslint-config-alloy -D

备注：eslint babel-eslint eslint-plugin-react 不在这里安装的原因是 默认 create-react-app 构建的时候已经默认安装过这三个依赖(yorn.lock 可以查看到)

### package.json 配置(不单独增加.eslintrc.js)

增加 alloy,alloy/react 配置选项

```
"eslintConfig": {
  "extends": [
    "react-app",
    "react-app/jest",
    "alloy",
    "alloy/react"
  ]
},
```

### 结合 Prettier 使用

eslint-config-alloy 从 v3 开始，已经不包含所有样式相关的规则了，故不需要引入 eslint-config-prettier。只需要安装 prettier 及相关 VSCode 插件即可。

下面给出一个 AlloyTeam 使用的 .prettierrc.js 配置，仅供参考：

```
// .prettierrc.js
module.exports = {
  // 一行最多 100 字符
  printWidth: 100,
  // 使用 2 个空格缩进
  tabWidth: 2,
  // 不使用缩进符，而使用空格
  useTabs: false,
  // 行尾需要有分号
  semi: true,
  // 使用单引号
  singleQuote: true,
  // 对象的 key 仅在必要时用引号
  quoteProps: 'as-needed',
  // jsx 不使用单引号，而使用双引号
  jsxSingleQuote: false,
  // 末尾不需要逗号
  trailingComma: 'none',
  // 大括号内的首尾需要空格
  bracketSpacing: true,
  // jsx 标签的反尖括号需要换行
  jsxBracketSameLine: false,
  // 箭头函数，只有一个参数的时候，也需要括号
  arrowParens: 'always',
  // 每个文件格式化的范围是文件的全部内容
  rangeStart: 0,
  rangeEnd: Infinity,
  // 不需要写文件开头的 @prettier
  requirePragma: false,
  // 不需要自动在文件开头插入 @prettier
  insertPragma: false,
  // 使用默认的折行标准
  proseWrap: 'preserve',
  // 根据显示样式决定 html 要不要折行
  htmlWhitespaceSensitivity: 'css',
  // 换行符使用 lf
  endOfLine: 'lf'
};
```

### vscode setting 配置(切记一定要配置，否则.prettierrc.js 不生效)

VSCode 的一个最佳实践就是通过配置 .vscode/settings.json 来支持自动修复 Prettier 和 ESLint 错误：

```
{
  "files.eol": "\n",
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "eslint.validate": ["javascript", "javascriptreact", "vue", "typescript", "typescriptreact"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

注意："editor.formatOnSave": true,

# Next.js（v15.3.2）での ESLint & Prettier 推奨設定

## 1. 必要なパッケージのインストール

Next.js プロジェクトを作成した後、Prettier と ESLint 連携パッケージを追加します。

```bash
npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

---

## 2. 推奨設定ファイル例

### 2.1 `.eslintrc.js`（ESLintの設定）

```javascript
/** @type {import('eslint').Linter.Config} */
module.exports = {
  root: true,
  extends: [
    "next/core-web-vitals",
    "plugin:prettier/recommended", // Prettierとの連携
  ],
  plugins: ["prettier"],
  rules: {
    // 必要に応じてルールを追加・上書き
    "prettier/prettier": "error",
  },
};
```

- `"next/core-web-vitals"`: Next.js公式推奨のESLint設定
- `"plugin:prettier/recommended"`: PrettierとESLintの競合ルールを自動調整
- `"prettier/prettier": "error"`: Prettier違反をエラーとして検知

---

### 2.2 `.prettierrc`（Prettierの基本設定）

```json
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

- `"singleQuote": true` → シングルクォートを使う
- `"trailingComma": "es5"` → 配列・オブジェクトの末尾カンマを付ける
- `"semi": true` → セミコロン必須
- `"printWidth": 100` → 1行最大100文字

---

### 2.3 `.prettierignore`（Prettierの適用除外ファイル）

```gitignore
node_modules
.next
out
public
.build
coverage
```

---

## 3. VSCodeでの自動整形推奨設定

`.vscode/settings.json` に以下を追加すると、保存時に自動で整形&ESLintが効きます。

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

---

## 4. 使い方

- 保存時に自動でPrettier整形・ESLint修正が行われます
- コマンドでも手動実行可能
  ```bash
  npx eslint . --fix
  npx prettier --write .
  ```

---

## 5. 参考リンク

- [Linting | Next.js Docs](https://nextjs.org/docs/app/building-your-application/configuring/eslint)
- [Formatting | Next.js Docs](https://nextjs.org/docs/app/building-your-application/configuring/formatting)

---
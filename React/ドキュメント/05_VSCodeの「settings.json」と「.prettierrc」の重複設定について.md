# VSCodeの「settings.json」と「.prettierrc」の重複設定について

---

## 結論

- **両方に似た設定があっても問題ありませんが、役割が異なります。**
- **一般的には、プロジェクト全体で統一したい場合は「.prettierrc」に記載し、VSCode個別の振る舞いは「settings.json」で制御します。**
- **推奨：プロジェクトごとの整形ルールは`.prettierrc`に集約し、VSCodeの「settings.json」は「Prettier拡張で自動整形を有効化」など最低限に留めるのがベストです。**

---

## それぞれの意味と優先順位

### 1. `.prettierrc`

- **プロジェクトの整形ルールを定義するファイル**
- Prettier CLIや他のエディタ、チーム全員が「共通の整形ルール」で整形可能
- **リポジトリに含めておくことで、誰がどのエディタで開発しても同じ整形結果になる**

### 2. VSCodeの`settings.json`

- **VSCodeでPrettier拡張を使った時の動作設定**
  - `"editor.formatOnSave": true` → 保存時に自動整形
  - `"editor.defaultFormatter": "esbenp.prettier-vscode"` → デフォルト整形ツール
- `"prettier.xxx"`の設定は、**.prettierrcが存在しない場合や上書きしたい場合のみ有効**
- **.prettierrcが存在すると、そちらの設定が優先される**（VSCode拡張もそれに従う）

---

## 重複した場合の挙動

- **`.prettierrc`があるプロジェクトであれば、"settings.json"の`prettier.xxx`よりも`.prettierrc`の内容が優先される**
- **`.prettierrc`がない場合だけ、"settings.json"の`prettier.xxx`が効く**

---

## まとめ

- **原則、整形ルールは`.prettierrc`にまとめ、VSCodeの設定は最小限でOK**
- VSCodeで「保存時に自動整形」や「デフォルトフォーマッタ指定」だけを`settings.json`に記載する運用が推奨
- `"prettier.xxx"`を`settings.json`に残す必要はほぼない

---

### 推奨設定例

#### `.prettierrc`
```json
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

#### `.vscode/settings.json`
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

---

### 参考

- [Prettier公式ドキュメント - Configuration File](https://prettier.io/docs/en/configuration.html)
- [VSCode Prettier拡張 - FAQ](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode#faq)
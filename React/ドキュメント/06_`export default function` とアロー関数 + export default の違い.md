# Next.js/React: `export default function` とアロー関数 + export default の違い

---

## 質問

以下2つの書き方はどちらも同じ挙動をすると思うが、何が違う？どちらが適切？

①
```javascript
const HomePage = () => { /* 処理 */ }
export default HomePage;
```

②
```javascript
export default function HomePage() { /* 処理 */ }
```

---

## 回答

### 共通点

- どちらも**HomePageコンポーネントをデフォルトエクスポート**する方法。
- Next.jsやReactでどちらも一般的に利用される。

---

### 違い

| 項目                            | ① アロー関数                  | ② 関数宣言 (`export default function`) |
|:------------------------------- |:-----------------------------|:--------------------------------------|
| **宣言方法**                    | `const HomePage = () => {}`   | `function HomePage() {}`              |
| **エクスポート方法**             | 変数を後からexport default    | そのままexport default                |
| **関数名の扱い**                | 変数名が関数名になる場合が多いが、ビルド・バンドル環境で匿名になることも | 関数名が確実に保持される（デバッグやエラー時に有利） |
| **Hoisting（巻き上げ）**         | されない                      | される                                |
| **thisの扱い**                  | アロー関数はthisを持たない    | functionは通常のthis（ただしReactコンポーネントではほぼ影響なし） |
| **公式サンプルの多く**           | やや少なめ                    | 多い（Next.js公式ドキュメント等）     |

---

### どちらが適切？

- **Next.jsやReactの公式サンプル、多くの大手プロジェクトでは「② export default function」が推奨される傾向があります。**
- デバッグ時のスタックトレースで関数名がしっかり残るため、エラー解析などで有利。
- チームで統一するのがベストですが、「迷ったら②（関数宣言）」がおすすめ。

---

### 例（推奨）

```javascript
export default function HomePage() {
  // 処理
  return <div>Home</div>;
}
```

---

### 参考

- [Next.js 公式サンプル](https://nextjs.org/docs/getting-started/example)
- [React 公式ドキュメント](https://react.dev/learn/your-first-component)

---
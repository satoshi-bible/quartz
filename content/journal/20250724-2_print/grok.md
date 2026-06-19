MarpでA4サイズのPDFにスライドを上半分、スピーカーノートを下半分に配置して出力するには、カスタムCSSを使用してスライドとノートのレイアウトを調整し、`--pdf-notes`オプションを活用します。スピーカーノートがないスライドも考慮し、以下に手順とコードを示します。



```markdown
---
marp: true
size: A4
paginate: true
---

<style>
/* スライド全体をA4の上半分に配置 */
section {
  height: 50%;
  top: 0;
  padding: 20px;
  box-sizing: border-box;
}

/* スピーカーノートをA4の下半分に配置 */
section::after {
  content: attr(data-marpit-comment);
  display: block;
  position: absolute;
  top: 50%;
  left: 20px;
  right: 20px;
  height: 50%;
  font-size: 16px;
  color: #333;
  padding: 20px;
  border-top: 1px solid #ccc;
  overflow: auto;
}

/* スピーカーノートがない場合の処理 */
section:not([data-marpit-comment])::after {
  content: "（スピーカーノートなし）";
  color: #999;
  font-style: italic;
}
</style>

# スライド 1
コンテンツ1

<!-- スピーカーノート: ここにスライド1のノートを記述します。 -->

---

# スライド 2
コンテンツ2
<!-- スピーカーノートなし -->

---

# スライド 3
コンテンツ3

<!-- スピーカーノート: ここにスライド3のノートを記述します。長いノートでも下半分に収まるようにスクロール可能です。 -->
```



### 手順
1. **Marp CLIのインストール**  
   Node.jsがインストールされていることを確認し、以下のコマンドでMarp CLIをインストールします：
   ```bash
   npm install -g @marp-team/marp-cli
   ```

2. **Markdownファイルの準備**  
   上記のサンプルMarkdownファイルを参考に、`<!-- -->`でスピーカーノートを記述します。ノートがないスライドもそのまま処理されます。

3. **PDFへの変換**  
   以下のコマンドでA4サイズのPDFを出力します。`--pdf-notes`オプションを指定してスピーカーノートを含めます：
   ```bash
   npx marp --pdf --allow-local-files --pdf-notes your_slides.md -o output.pdf
   ```
   - `--allow-local-files`: ローカルファイル（画像など）を使用する場合に必要。
   - `--pdf-notes`: スピーカーノートをPDFに含める。

4. **カスタムCSSの説明**  
   - `section`: スライドをA4の上半分（50%の高さ）に配置。
   - `section::after`: スピーカーノートを下半分に表示し、`data-marpit-comment`属性からノートを取得。
   - `section:not([data-marpit-comment])::after`: ノートがない場合に「（スピーカーノートなし）」と表示。
   - フォントサイズやパディングは好みに応じて調整可能。

5. **注意点**  
   - スライドのコンテンツ量が多い場合、レイアウトが崩れる可能性があるため、コンテンツを簡潔に保つ。
   - 長いスピーカーノートは`overflow: auto`によりスクロール可能。
   - Google Chrome、Microsoft Edge、またはFirefoxがインストールされている必要があります。

これで、A4サイズのPDFにスライドとスピーカーノートを指定のレイアウトで出力できます。詳細はMarpの公式ドキュメント（https://marp.app/）を参照してください。[](https://github.com/marp-team/marp-cli)[](https://www.hashbangcode.com/article/seven-tips-getting-most-out-marp)
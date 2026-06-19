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

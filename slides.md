---
title: Markdown Documentationのススメ
colorSchema: light
canvasWidth: 1280
themeConfig:
  primary: "#3db680"
background: /attachments/cat-minerva.webp
comark: true
layout: cover
# /index.html が必須の環境では /index.html#3 のような形式を許容させる
routerMode: hash
---

# Slidevのレイアウトベーススライド

<span class="text-dimmed">
2026/03/08   Tadashi Aikawa
</span>

---
title: Agenda
layout: chapter-divider
---

---
title: Chapter1
layout: chapter-divider
activeChapter: 1
---

---

# 普通のスライド

ここに説明を書いたり。

- 箇条書きを
- 書いたり

---

# 最後に結論を表示

ここには

- 普通の説明を
- 書いたりして
- クリックすると

<conclusion>

結論が表示される

</conclusion>

---

# 最後に結論をオーバーレイで表示

ここには

- 普通の説明を
- 書いたりして
- いるけど

スライド全体を

- ぎっしり使っていて
- 領域がないときでも

<conclusion overlay>

オーバーレイで中央に結論が表示される

</conclusion>

---
layout: fact
---

# fact

名言だったり、参考文献・グラフなどの事実を扱うときに使う。

すべてが中央寄りになる。

```ts
const a = 1;
const b = 2;
// コードブロックには向かない。その場合は `layout: center` を使おう
```

<refer>

出典の明記

</refer>

---
layout: center
---

# center

中央にコンテンツを表示したいときに使う。

中央揃えではないので注意。

```ts
const a = 1;
const b = 2;
console.log(a + b);
```

---
layout: image
image: /attachments/cat-minerva.webp
---

# 画像を全面表示したい場合 (中心を軸に展開){.!text-white}

---
layout: image
image: /attachments/cat-minerva.webp
backgroundSize: cover
backgroundPosition: left top
---

# 画像を全面表示したい場合 (起点を左上にあわせる){.!text-white}

---

# 画像をトリミングしたい場合

<div class="h-140 overflow-hidden">
    <img src="./public/attachments/cat-minerva.webp" class="block" />
</div>

---

# 動画再生 `自動再生不要ならautoplayは外す`

<SlidevVideo controls autoplay="once" autoreset="slide" class="mx-auto h-90%">
    <source src="./public/attachments/colot.mp4" type="video/mp4" />
</SlidevVideo>

---
layout: image-left
image: https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/Notes/attachments/colot.webp
background-size: contain
---

# 左半分を画像にしたい場合

```yaml
background-size: contain
```

を追加することで縦が収まるサイズに調整している。

---
layout: image-left
image: https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/Notes/attachments/colot.webp
background-size: cover
ratio: 25%
---

# 左25%を画像にしたい場合

```yaml
ratio: 25%
```

で割合を指定できる。要独自コンポーネント。

```yaml
background-size: cover
```

`contain` ではなく `cover` にすることで最大表示。

---
layout: image-right
image: https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/Notes/attachments/obsidian-mini2.webp
background-size: contain
---

# 右半分を画像にしたい場合

```yaml
background-size: contain
```

を追加することで縦が収まるサイズに調整している。

---
layout: image-right
image: https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/Notes/attachments/obsidian-mini2.webp
background-size: contain
ratio: 25%
---

# 右25%を画像にしたい場合

```yaml
ratio: 25%
```

で割合を指定できる。要独自コンポーネント。

---

# 画像パスの注意点

指定する対象によって正しくパスを入力しないと『ビルド時』『デプロイ時』に解決しなくなる。

| 対象                                       | パスの開始              |
| ------------------------------------------ | ----------------------- |
| HTMLの `src` 属性                          | `./public/attachments/` |
| Vueファイル内の `src` 属性 に渡されるprops | `./attachments/`        |
| フロントマターのプロパティ                 | `/attachments/`         |
| Markdownの画像リンク                       | `/attachments/`         |
| CSSの `url`                                | `/attachments/`         |

<refer>

[📕Slidevの画像パスに対する注意 - Minerva](https://minerva.mamansoft.net/Notes/%F0%9F%93%95Slidev%E3%81%AE%E7%94%BB%E5%83%8F%E3%83%91%E3%82%B9%E3%81%AB%E5%AF%BE%E3%81%99%E3%82%8B%E6%B3%A8%E6%84%8F)

</refer>

---
layout: iframe-refer
url: https://minerva.mamansoft.net/Notes/%E3%83%9F%E3%83%8D%E3%83%AB%E3%83%B4%E3%82%A1
refer-text: Minerva
scale: 1 # default
---

# 全面iframe

---

# Richリンクカード

<div class="link-card-v2">
  <div class="link-card-v2-site">
    <img class="link-card-v2-site-icon" src="https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/favicon-64.png" />
    <span class="link-card-v2-site-name">Minerva</span>
  </div>
  <div class="link-card-v2-title">
    📘オブシディアの1日から紐解くObsidianの使い方
  </div>
  <div class="link-card-v2-content">平日の1日を追いながら、Obsidianでのデイリーノート運用、SilhouetteやVarious Complementsなど自作プラグインを使ったタスク管理・議事録・ドキュメント連携の実例を、ミネルヴァとオブシディアが紹介します。</div>
  <img class="link-card-v2-image" src="https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/%F0%9F%93%98Articles/attachments/2025-12-25.webp" />
  <a data-href="📘オブシディアの1日から紐解くObsidianの使い方" class="internal-link"></a>
</div>

---
layout: two-cols-header
---

# ヘッダの下を左右に分割

::left::

- 左側

::right::

- 右側

---
layout: two-cols-header-ratio
columns: "3:7"
---

# ヘッダの下を左右に分割 (比率指定)

::left::

- 左側 (30%)

::right::

- 右側 (70%)

---
layout: two-cols
---

# ヘッダ含めて左右に分割(左側のタイトル)

- 左側

::right::

# ヘッダ含めて左右に分割(右側のタイトル)

- 右側

---
title: Chapter2
layout: chapter-divider
activeChapter: 2
---

---
layout: fact
---

# コードブロックの表現は多い

---

# 普通のコードブロック

```lua
return {
  -- 'tadashi-aikawa/slidev-preview.nvim',
  dir = "~/git/github.com/tadashi-aikawa/slidev-preview.nvim",
  cmd = "SlidevPreviewStart",
  opts = {},
}
```

---

# ファイル名・行番号つき

```lua [slidev-preview.lua ~i-vscode-icons:file-type-lua~] {*}{lines: true}
return {
  -- 'tadashi-aikawa/slidev-preview.nvim',
  dir = "~/git/github.com/tadashi-aikawa/slidev-preview.nvim",
  cmd = "SlidevPreviewStart",
  opts = {},
}
```

※ ヘッドマターで `lineNumbers: true` を設定すれば `lines: true` は不要

---

# コードグループ

::code-group

```sh [npm]
npm i @slidev/cli
```

```sh [yarn]
yarn add @slidev/cli
```

```sh [pnpm]
pnpm add @slidev/cli
```

::

---

# 高度なコードブロック

`{*}{maxHeight:}` で指定する。`%` が良さげ。

```vue [MethodBadge.vue] {*}{maxHeight:'80%', lines: true}
<script setup lang="ts">
import type { PrimitiveProps } from "reka-ui";
import type { HTMLAttributes } from "vue";
import type { BadgeVariants } from ".";
import { reactiveOmit } from "@vueuse/core";
import { Primitive } from "reka-ui";
import { cn } from "@/lib/utils";
import { badgeVariants } from ".";

const props = defineProps<
  PrimitiveProps & {
    variant?: BadgeVariants["variant"];
    class?: HTMLAttributes["class"];
  }
>();

const delegatedProps = reactiveOmit(props, "class");
</script>

<template>
  <Primitive
    data-slot="badge"
    :class="cn(badgeVariants({ variant }), props.class)"
    v-bind="delegatedProps"
  >
    <slot />
  </Primitive>
</template>
```

---

# 高度なコードブロック

ハイライト指定は `{1,10}` や `{5-7}` のように。`|` 区切りでアニメーション。

```vue [MethodBadge.vue] {1,18|2-8|10-15|17}{maxHeight:'80%', lines: true}
<script setup lang="ts">
import type { PrimitiveProps } from "reka-ui";
import type { HTMLAttributes } from "vue";
import type { BadgeVariants } from ".";
import { reactiveOmit } from "@vueuse/core";
import { Primitive } from "reka-ui";
import { cn } from "@/lib/utils";
import { badgeVariants } from ".";

const props = defineProps<
  PrimitiveProps & {
    variant?: BadgeVariants["variant"];
    class?: HTMLAttributes["class"];
  }
>();

const delegatedProps = reactiveOmit(props, "class");
</script>

<template>
  <Primitive
    data-slot="badge"
    :class="cn(badgeVariants({ variant }), props.class)"
    v-bind="delegatedProps"
  >
    <slot />
  </Primitive>
</template>
```

---

# 高度なコードブロック

アニメーション表示 `md magic-move`

````md magic-move {lines: true}
```ts
const x = 1;
```

```ts
const x = 1;
const y = 1;
```

```ts
const x = -1;
```
````

---
title: Chapter3
layout: chapter-divider
activeChapter: 3
---

---

# アニメーション

<div v-click.fade-in>

内部の要素をフェードイン

</div>

---

# スポットライト

クリックするとスポットライトがあたる。

<div v-click.fade-in class="spotlight left-32 top-96 w-128 h-64"></div>

---
title: Chapter4
layout: chapter-divider
activeChapter: 4
---

---

# 改訂履歴

右上に改訂履歴が表示される。

<revision-histories :revisions="[
  {date: '2026-05-26', content: '初版'},
  {date: '2026-05-27', content: 'ちょっと修正'},
  {date: '2026-05-30', content: 'ガッツリ修正しました'}
]" />

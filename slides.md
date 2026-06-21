---
title: Class Variance Authority
colorSchema: light
canvasWidth: 1280
themeConfig:
  primary: "#3db680"
background: /attachments/cover-bg.webp
comark: true
layout: cover
# /index.html が必須の環境では /index.html#3 のような形式を許容させる
routerMode: hash
class: simple-cover
---

# Class Variance Authority

<span class="text-dimmed">
2026/06/21   Tadashi Aikawa
</span>

---

# コンポーネントは『種類』『サイズ』『状態』をもつことが多い

```tsx
<Button variant="primary" size="sm" />
<Button variant="danger" size="lg" />
<Button variant="outline" disabled />
```

<div class="flex justify-center items-center gap-4 mt-24">
    <Button variant="primary" size="sm">primary sm</Button>
    <Button variant="danger" size="lg">danger lg</Button>
    <Button variant="outline" disabled>outline disabled</Button>
</div>

---

# 愚直に実装するとこうなる

<<< @/components/Button.vue vue {1-|2-13|17-36}{lines:true,maxHeight:'90%'}

---

# メンテナンスできるように整理すると

<<< @/components/Button2.vue vue {1-|18-28|31-45}{lines:true,maxHeight:'90%'}

---
layout: center
---

<Bubble image="./attachments/ts-chara.webp" imageHeight="280" imageGap="24px" direction="right">

でも、*定義が複数箇所にあって*管理に気を遣いそうね...

</Bubble>

<Bubble v-click image="./attachments/etokichi+1.webp" imageHeight="220" direction="left">

安心して！<br/>
**Class Variance Authority** というものがあるんだよ！

</Bubble>

---
layout: iframe-refer
url: https://cva.style/docs
refer-text: cva
scale: 1 # default
---

---
layout: fact
---

# CVAとは

コンポーネントに対する見た目の定義(class, style)を<br/>
*宣言的・型安全*に行える小さなユーティリティ

v0.7.1

---

# 先ほどのコード

<<< @/components/Button2.vue vue {1-}{lines:true,maxHeight:'90%'}

---

# CVAを使うとこうなる

<<< @/components/CVAButton.vue vue {1-|4-34|5|7-26|27-32|36,37|39-}{lines:true,maxHeight:'90%'}

---

<div style="--slidev-code-font-size: 0.23em; width: 560px;">

<<< @/components/CVAButton.vue vue {1-}{lines:true,maxHeight:'90%'}

</div>

<spotlight v-click.fade-in class="left-20 top-14 w-128 h-110" />
<Bubble v-click.fade-in image="./attachments/ts-chara.webp" imageHeight="280" imageGap="16px" class="left-156 top-14 absolute" direction="right">
ここの部分は<br/>
Vueファイルの中に<br/>
書かなくてもよいのでは？
</Bubble>

<div v-click.fade-in class="left-192 top-102 absolute">

```
📁components
└──📁button
    ├── index.ts
    └── Button.vue
```

</div>

---

<div class="grid grid-cols-[5fr_4fr] gap-4 text-3xl">

<div>

`components/button/index.ts`

<div style="--slidev-code-font-size: 0.36em;">

<<< @/components/button/index.ts ts {1-}

</div>

</div>

<div>

`components/button/Button.vue`

<div style="--slidev-code-font-size: 0.36em;">

<<< @/components/button/Button.vue vue {1-}

</div>

</div>

</div>

<div v-click.fade-in="[1, 2]">

<spotlight v-click.fade-in class="left-16 top-12 w-160 h-168" />
<Bubble v-after.fade-in="[1, 2]" direction="top" image="./attachments/ts-chara.webp" imageHeight="280" imageGap="16px" class="left-180 top-14 absolute">
見た目を変えたくなったら<br/>
こちらを変更します
</Bubble>

</div>

<div v-click.fade-in="2">

<spotlight v-click.fade-in class="left-176 top-12 w-128 h-94" />
<Bubble direction="top" image="./attachments/etokichi+1.webp" imageHeight="280" imageGap="16px" class="left-64 top-14 absolute">
処理を変えたくなったら<br/>
こっちを変更だね！
</Bubble>

</div>

---

# compoundVariants `組み合わせの定義`

```ts {*|4-}{lines:true,maxHeight:'90%'}
import { cva, type VariantProps } from "class-variance-authority";

const button = cva(["rounded"], {
  variants: {
    intent: { primary: ["bg-blue-500"], secondary: ["bg-gray-200"] },
    disabled: { false: null, true: ["cursor-not-allowed"] },
  },
  // 特定の属性値が組み合わさったときだけ付与されるクラス
  compoundVariants: [
    { intent: "primary", disabled: true, class: "hover:bg-blue-600" },
    { intent: "secondary", disabled: false, class: "hover:bg-gray-100" },
  ],
});

console.log(button({ intent: "primary", disabled: false }));
// rounded bg-blue-500
console.log(button({ intent: "primary", disabled: true }));
// rounded bg-blue-500 cursor-not-allowed hover:bg-blue-600
console.log(button({ intent: "secondary", disabled: false }));
// rounded bg-gray-200 hover:bg-gray-100
```

<refer>

[Variants | cva](https://cva.style/docs/getting-started/variants#compound-variants)

</refer>

---

# CVAが向かないケース

- コンポーネントではないもの
  - `variant` `size` などのpropsにはならないので
- propsが少ないコンポーネント
  - `cva()` を使った方がかえって複雑になる

---

# まとめ

**『CVA』は**

- コンポーネントの見た目を _宣言的・型安全_ に定義できる
- その定義を _`.ts` ファイルに切り出せる_
- `compoundVariants` で複雑な組み合わせ条件にも対応できる

---
layout: fact
---

# APPENDIX

---

# class名の補完

[Installation | cva > IntelliSense](https://cva.style/docs/getting-started/installation#intellisense) を参照。

<space />

`私のNeovimの例`

```lua [nvim/after/lsp/tailwindcss.lua ~i-vscode-icons:file-type-lua~]
return {
  workspace_required = true,
  settings = {
    tailwindCSS = {
      classFunctions = { "cva", "cx", "h" },
    },
  },
}
```

---

# class順の自動ソート

Prettierを使っているなら [prettier-plugin-tailwindcss](https://github.com/tailwindlabs/prettier-plugin-tailwindcss) を使う。

<space />

`私の設定例`

```json [.prettierrc.json]
{
  "plugins": ["prettier-plugin-tailwindcss"],
  "tailwindFunctions": ["cva", "cn"]
}
```

---

# class順の自動ソート

*配列表記では機能しない*ので注意。

```typescript
const button = cva(["rounded"], {
  variants: {
    intent: {
      // ❌ ソートされない
      primary: ["bg-blue-500", "text-red", "flex"],
      // ✅ ソートされる
      secondary: "bg-blue-500 text-red flex",
    },
```

<Bubble direction="left" image="./attachments/ts-chara.webp" imageHeight="220" imageGap="24px">

[要望](https://github.com/tailwindlabs/tailwindcss/discussions/15993)は挙がっているみたいね。

</Bubble>

---

# 必須プロパティ型の表現

```typescript
type RequireNonNullable<T, K extends keyof T> = Omit<T, K> & {
  [P in K]-?: Exclude<T[P], null | undefined>;
};
```

```typescript
// variantだけ必須指定にした例. sizeも必須にするなら "variant" | "size" を指定する
export type ButtonVariants = RequireNonNullable<
  VariantProps<typeof buttonVariants>,
  "variant"
>;

type Variant = ButtonVariants["variant"];
//   ^ "primary" | "danger" | "outline"
type Size = ButtonVariants["size"];
//   ^ "sm" | "md" | "lg" | null | undefined
```

---

# Tailwind CSS クラスの慎重な競合解消

[tailwind-merge](https://github.com/dcastil/tailwind-merge)を使う。 `基本的には使わなくても大抵は動く`

```ts
import { cva, type VariantProps } from "class-variance-authority";
import { twMerge } from "tailwind-merge";

const buttonVariants = cva(/** 中略 */);
type ButtonVariants = VariantProps<typeof buttonVariants>;

export const button = (variants: ButtonVariants) =>
  twMerge(buttonVariants(variants));
```

<Bubble direction="left" image="./attachments/ts-chara.webp" imageHeight="220" imageGap="24px">

Vueファイルで `buttonVariants` を使うときにwrapする方法もアリね。

</Bubble>

<refer>

[Installation | cva > Handling Style Conflicts](https://cva.style/docs/getting-started/installation#handling-style-conflicts)

</refer>

---

# 参考

<div class="link-card-v2">
  <div class="link-card-v2-site">
    <img class="link-card-v2-site-icon" src="https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/favicon-32.png" />
    <span class="link-card-v2-site-name">Minerva</span>
  </div>
  <div class="link-card-v2-title">
    📕Class Variance Authorityを使ったVueのコンポーネント設計 - Minerva
  </div>
    <div class="link-card-v2-content">
    class-variance-authorityとTailwind CSSを用いたVue3コンポーネント設計で、variantの必須制御や複数variantの型定義パターンを整理した記録である。 ... 
  </div>
  <img class="link-card-v2-image" src="https://publish-01.obsidian.md/access/35d05cd1bf5cc500e11cc8ba57daaf88/Notes/attachments/2026-01-19-06-27-00.webp" />
  <a href="https://minerva.mamansoft.net/Notes/%F0%9F%93%95Class%20Variance%20Authority%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%9FVue%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%8D%E3%83%B3%E3%83%88%E8%A8%AD%E8%A8%88"></a>
</div>

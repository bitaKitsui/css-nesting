---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev
mdc: true
---

# CSS ネスティング

---

# 自己紹介

橘井貴輝 PD9U

- ちいかわセイレーン編終了
- 最近映画熱が再燃しつつある
- スイカゲーム記録
  - 3517
  - 3512
  - 3269

---

# Agenda

- CSSネスティングの概要
- 利点
- 実例
- まとめ

---

# 概要

- Sass など CSS プリプロセッサーと同様にネスティング機能がサポートされた
- Chrome, Firefox, Safari など主要ブラウザで今年サポート
- 一つ制限があったが、それも最近解消された

<img src="/can_i_use.png" alt="" style="height:340px">

---

# 概要

これが

```css
.foo {
  color: green;
}

.foo .bar {
  font-size: 1.4rem;
}
```

こう書ける

```css
.foo {
  color: green;
  
  .bar {
    font-size: 1.4rem;
  }
}
```

---

# 利点

- 繰り返しの記述が減り、可読性が増す
- スタイルのグループ化がしやすくなる
- 特定のスタイルのスコープ化ができる
- クラスや ID を持たない HTML 要素のスタイルが付けやすくなる

---

<div style="display: grid; place-content: center; height: 100%">
<h1>主なルール</h1>
</div>

---

# クラスがある要素のネスト

そのままネストすれば OK

```css
.nav__item {
  .link {
    display: block;
    padding: 1.5rem 1rem;
  }
}

/* これと同じ: */
.nav__item .link {
}
```

---

# CSS 結合子のネスト

次兄弟結合子 `+` を使った場合の例

```html
<li class="nav__item">
  <a>Home</a>
</li>
<li class="nav__item">
  <a>About</a>
</li>
<li class="nav__item">
  <a>Contact</a>
</li>
```

```css
.nav__item {
	& + & {
		border-left: 1px solid pink;
	}
}
```

---

# Active, Focus, Hover...

擬似クラスも別々に書く必要がなくなる

```css
.button {
  &:hover {}
  &:focus {}
}

/* こう書かなくて済む */
.button {}
.button:hover {}
```

---

# クラスや ID が存在しない要素のネスト

以前までは制限があった...

`&` がネストするうえで必要だった

```html
<li class="nav__item">
  <a href="#">Home</a>
</li>
```

```css
.nav__item {
  & a {
    display: block;
    padding: 1.5rem 1rem;
  }
}
```

---

# クラスや ID が存在しない要素のネスト

素の要素が `&` なしでネストされるようになった

Chrome 120 から

```html
<li class="nav__item">
  <a href="#">Home</a>
</li>
```

```css
.nav__item {
  a {
    display: block;
    padding: 1.5rem 1rem;
  }
}
```

https://developer.chrome.com/blog/css-nesting-relaxed-syntax-update/

---

<div style="display: grid; place-content: center; height: 100%">
<h1>実例</h1>
</div>

---

# 記事のスタイル

クラス名の繰り返しが必要なくなる（ `:is` セレクタで同じことができるが）

```css
.post-content h1,
.post-content h2,
.post-content h3,
.post-content h4 {
  color: red;
  margin-bottom: 1.5rem;
}
```

```css
.post-content {
  h1,
  h2,
  h3,
  h4 {
    color: red;
    margin-bottom: 1.5rem;
  }
}
```

---

# 記事のスタイル

段落の中の、特定の要素にスタイルを付ける場合もより明確に

```css
.post-content {
  p {
    color: gray;
    
    a {
      font-weight: bold;
      text-decoration: underline;
      
      &:hover {
        color: red;
      }
    }
  }
}
```

---

# 記事のスタイル

メディアクエリなどもネストして記述可能

```css
.post-content {
  p {
    ...
    
    @media(min-width: 400px) {
      ...
    }
  }
}

.card {
  @container card (min-width: 400px) {
    display: flex;
  }
}
```

---

# 記事のスタイル

要素の有無や特定の条件によってスタイルを変えたりも可能

```css
.post-content {
  figure {
    img {
      ...
    }
    
    &:has(figcaption) {
      display: flex;
      align-items: start;
    }
    
    figcaption {
      color: red;
    }
  }
}
```

```css
.post-content {
  li {
    &:not(:last-child) {
      border-bottom: 2px solid;
    }
  }
}
```

---

# 親要素を経由したスタイル

```html
<div class="box">
  <h2>culpa</h2>
  <p>Nulla sit excepteur ullamco.</p>
  <button class="button">Click Here!</button>
</div>
<button class="button">Click Here!</button>
```

```css
.button {
  .box & {
    width: 100%;
  }
}

/* これと同じ */
```

---

# まとめ

- スタイルを要素ごとにまとめていく力が増えている
- 新しい機能で直感に反する挙動もありそうなので注意は必要

---
layout: end
---

# End
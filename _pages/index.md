---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 🏠 ホーム
permalink: /
---

<div class="container" id="particles-js" style="position: relative; height: 5rem; z-index: 100">
  <div style="position: absolute; width: 100%; z-index: 200">
    <figure class="text-center">
    <blockquote class="blockquote">
      <p id="text" class="blockquote-text"></p>
    </blockquote>
    <figcaption class="blockquote-footer">
      <span id="artist"></span> / <cite id="title"></cite> <a href="javascript:void(0)" onClick="updateText(); return false;" class="fs-4 text-decoration-none">🔄</a>
    </figcaption>
    
  </figure>
  </div>  
</div>

---

#### 最新の記事
{% for post in site.posts limit:1 %}
  * [{{ post.title }}]({{ post.url }})
{% endfor %}

#### 見ましょう
* [オリジナルTVアニメーション「リコリス・リコイル」公式サイト](https://lycoris-recoil.com/)
* [TVアニメ「継母の連れ子が元カノだった」公式サイト](https://tsurekano-anime.com/)
* [「ラブライブ！スーパースター!!」公式サイト](https://www.lovelive-anime.jp/yuigaoka/)
* [TVアニメ「カッコウの許嫁」公式サイト](https://cuckoos-anime.com/)
* [TVアニメ「それでも歩は寄せてくる」公式サイト](https://soreayu.com/)

#### ロシアによるウクライナへの侵攻に反対します
* [Appeal to Ruby community from Kharkiv Rubyist](https://zverok.space/blog/2022-03-03-WAR.html)
* [War in Ukraine: official website, MFA of Ukraine](https://war.ukraine.ua/)

---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 🏠 ホーム
permalink: /
---

<div class="container" id="particles-js" style="position: relative; height: 10rem">
  <div style="position: absolute; width: 100%">
    <div class="rainbow" id="title">
    Welcome
    </div>
  
    <div class="row">
      <div class="col-3">
        うおお
      </div>
      <div class="col-1" style="writing-mode: vertical-rl">
        よく来たね
      </div>
      <div class="col-10"></div>
    </div>
  </div>  
</div>

<select id="your_will" onchange="updateTitle();">
  <option value="ウオオオオオオオオオ">ウオオオオオオオオオ</option>
  <option value="狂う">狂う</option>
  <option value="狂井 益男">狂井 益男</option>
  <option value="ギャオオオオオオオオ">ギャオオオオオオオオ</option>
  <option value="DAKARA NANY">DAKARA NANY</option>
  <option value="オオアオ動物園">オオアオ動物園</option>
</select>

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

<script>
  function updateTitle() {
    let titleSelect = document.getElementById("your_will");
    let title = document.getElementById("title");
    title.innerHTML = titleSelect.value;
  }
</script>
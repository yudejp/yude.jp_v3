---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 🏠 ホーム
permalink: /
---

<div class="container" id="particles-js" style="position: relative; height: 10rem">
  <div style="position: absolute; width: 100%">
    <figure class="text-center">
    <blockquote class="blockquote">
      <p id="text"></p>
    </blockquote>
    <figcaption class="blockquote-footer">
      <span id="artist"></span> / <cite id="title"></cite>
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

<script>
  function Word(_text, _artist, _title) {
    this.text = _text;
    this.artist = _artist;
    this.title = _title;
  } 
  
  let words = [];
  words.push(new Word("本当の夢はとまらないんだね いま心が駆け出すんだ", "Liella!", "START!! True dreams"));
  words.push(new Word("昨日の夜を大人になるまで 心に仕舞っておくよ", "はるまきごはん", "蛍はいなかった"));
  words.push(new Word("僕らは宇宙もまだ知らない ゼロのゲート開くよ", "いとうかなこ", "アマデウス"));
  words.push(new Word("また昔みたいに 眠れるような気がして", "iroha(sasaki)", "炉心融解"));
  words.push(new Word("君が手を差し伸べた 光で影が生まれる", "さユり", "花の塔"));
  words.push(new Word("きっと、目と目が合うと 吹き出しちゃったりするんだ", "いよわ", "オーバー!"));
  words.push(new Word("めんどくさい☆諦め悪いみたい まだ重々謙遜したい yey", "ずっと真夜中でいいのに。", "ミラーチューン"));
  words.push(new Word("僕と君はふたりだけで 楽しく壊れたいから", "きくお", "天国へ行こう"));
  words.push(new Word("偽りのない自由をこの手にダンス 故に踊る", "UPLIFT SPICE", "オメガリズム"));
  words.push(new Word("はなればなれ見上げた空は 青く青く澄み切っていく", "TrySail", "azure"));
  words.push(new Word("だんだん 君と同じ言葉が使えるね", "みきとP", "いーあるふぁんくらぶ"));
  words.push(new Word("明日が晴れるなら それでいいや", "Mrs. GREEN APPLE", "春愁"));
  words.push(new Word("全身全霊で向かうわ 再生 再生 再生成", "Perfume", "再生"));
  
  
  let selected_word = words[Math.floor(Math.random() * words.length)];
  document.getElementById("text").innerHTML = selected_word.text;
  document.getElementById("artist").innerHTML = selected_word.artist;
  document.getElementById("title").innerHTML = selected_word.title;

</script>
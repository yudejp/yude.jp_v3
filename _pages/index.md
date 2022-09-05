---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 🏠 ホーム
permalink: /
---

<div class="container" id="particles-js" style="position: relative; height: 4rem; z-index: 100">
  <div style="position: absolute; width: 100%; z-index: 200">
    <figure class="text-center">
    <blockquote class="blockquote">
      <p id="text" class="blockquote-text"></p>
    </blockquote>
    <figcaption class="blockquote-footer">
      <span id="artist"></span> / <cite id="title"></cite> <a href="javascript:void(0)" id="refreshButton" class="fs-4 text-decoration-none">🔄</a>
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
  words.push(new Word("愛していんのさ 強く愛していんのさ", "syudou", "キュートなカノジョ"));
  words.push(new Word("いつになれば終わるんだ 皆目、見当もつかない", "sumika", "フィクション"));
  words.push(new Word("Every day I listen to my heart", "平原綾香", "Jupiter"));
  words.push(new Word("響き合う願いが今 覚醒めてく", "fripSide", "LEVEL5-judgelight-"));
  words.push(new Word("何より大切と気付いても もう目も合わない", "滝川 ありさ", "さよならのゆくえ"));
  words.push(new Word("私の言葉は難しく受け止めないで 軽く聞き流すぐらいでいいから", "40mP", "嘘つきメーカー"));
  words.push(new Word("忘れたい思い出が人質だから いつでも殺れること覚悟しといてよ", "DECO*27", "人質交換"));
  words.push(new Word("君を誰より深く知っていたのに 隣の席の君はいない", "やなぎなぎ", "over and over"));
  words.push(new Word("君にいいことがあるように 今日は赤いストローさしてあげる", "aiko", "ストロー"));
  words.push(new Word("タンタンタン...もっと、さ! 想いをとめないで", 'チーム"ハナヤマタ"', "ヨロコビ・シンクロニシティ"));
  words.push(new Word("狂ったフリでごまかしていこうぜ 骨も残らぬパパママよ", "いよわ", "1000年生きてる"));
  words.push(new Word("自分がそう思うから みんな○○であって欲しいんでしょ", "ピノキオピー", "魔法少女とチョコレゐト"));
  words.push(new Word("真の真のハッピーエンド 着々とつくりましょ", "Wake Up, Girls!", "恋?で愛?で暴君です!"));
  words.push(new Word("重い荷物はいらないよ 裸足でかけていこう", "鹿乃", "プリマステラ"));
  words.push(new Word("これはそう、今日を諦めなかった 故の物語", "Leo/need", "ステラ"));
  words.push(new Word("同じく夢見続ける全て 君の明日を照らしたい", "川田まみ", "FIXED STAR"));
  words.push(new Word("泥んこだけど歩いて行ける まだまだ先は長いさ", "れるりり", "神のまにまに"));
  words.push(new Word("ダウンロードは終わらない アップロードは進捗ない", "かめりあ feat.ななひら", "インターネットが遅いさん"));
  words.push(new Word("なんでもないような秘密で わたしだけのあなたを探すの", "三月のパンタシア", "三月がずっと続けばいい"));
  words.push(new Word("呆れていないでちょっと待って きっと気に入ってもらえると思うな", "Official髭男dism", "115万キロのフィルム"));
  words.push(new Word("最後のサヨナラは他の誰でもなく 自分に叫んだんだろう", "あいみょん", "生きていたんだよな"));
  words.push(new Word("もう何も失わないように この血を流し尽くせ", "9mm Parabellum Bullet", "インフェルノ"));
  words.push(new Word("おっしゃ Let's 世界征服だ", "きゃりーぱみゅぱみゅ", "インベーダーインベーダー"));
  words.push(new Word("「いまは朝じゃないでしょ?」って そんなのしらない!", "名取さな", "さなのおうた。"));
  words.push(new Word("陽のあたる坂道を 自転車で駆けのぼる", "つじあやの", "風になる"));
  words.push(new Word("がんばってもどうしようもない時も きみを思い出すよ", "DREAMS COME TRUE", "何度でも"));
  words.push(new Word("離れ離れの街を 繋ぐ列車は行ってしまったね", "稲葉曇", "ラグトレイン"));
  words.push(new Word("大空を飛び回って 命揺らせ", "King Gnu", "飛行艇"));
  words.push(new Word("目先のマニーより 気持ち良いのが大事!", "23.exe", "CHO-DARI-"));
  words.push(new Word("虹の根元を探しにいこう あなたと迎えたい明日のために", "米津玄師", "かいじゅうのマーチ"));
  
  function updateText() {
    let selected_word = words[Math.floor(Math.random() * words.length)];
    document.getElementById("text").innerHTML = selected_word.text;
    document.getElementById("artist").innerHTML = selected_word.artist;
    document.getElementById("title").innerHTML = selected_word.title;
  }
  
  updateText();
  
  document.getElementById("refreshButton").addEventListener("click", updateText);
</script>
---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 🏠 ホーム
permalink: /
---

<div class="alert alert-success" role="alert">
  <h4 class="alert-heading"><i class="fa-solid fa-circle-info"></i> Misskey インスタンス開設のおしらせ&nbsp;&nbsp;──&nbsp;&nbsp;<code>mi.yude.moe</code></h4>
  <p style="margin: -5px; margin-left: 5px">誰でも参加可能な Misskey インスタンス、「オオアオ・・・」ができました！<br>
  <a href="https://mi.yude.moe">こちら</a> から参加できます。</p>
  <hr>
  <h5 class="alert-heading">Misskey とは？</h5>
  <p style="margin: -5px; margin-left: 5px">Misskey は、分散 SNS を作るソフトウェアの1つで、Mastodon や PeerTube とプロトコルに互換性があります (<a href="https://www.w3.org/TR/activitypub/">ActivityPub</a>)。もっと詳しく: <a href="https://join.misskey.page/ja-JP/">Misskeyをはじめよう</a></p>
</div>

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
{%- assign date_format = site.minima.date_format | default: "%Y/%-m/%-d" -%}
{% for post in site.posts limit:1 %}
  * [{{ post.title }}]({{ post.url }}) ({{ post.date | date: date_format }})
{% endfor %}

<div>
<iframe style="border-radius:12px" src="https://open.spotify.com/embed/playlist/04UddhIt9F0G9Ae8P5UQ29?utm_source=generator&theme=0" style="max-width: 800px" width="100%" height="380" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
</div>

<div>
<script type="application/javascript" src="https://embed.nicovideo.jp/watch/sm2057168/script?w=640&h=360"></script><noscript><a href="https://www.nicovideo.jp/watch/sm2057168">M.C.ドナルドはダンスに夢中なのか？最終鬼畜道化師ドナルド・Ｍ</a></noscript>
</div>

[アラー](https://www.mcdonalds.co.jp/)
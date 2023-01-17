---
layout: default
title: 👤 プロフィール
permalink: /profile/
---

<h1 id="name">yude</h1>
<img src="/assets/images/avatar.jpg" style="max-width: 200px; border-radius: 50%" class="mawaru" />

* アイコン: [Minkasy](https://twitter.com/xmnts) さんより

<div class="card" style="max-width: 30rem">
  <div class="card-body">
    <small>再生中</small>
    <h5 class="card-title" id="spotify_title">何も再生していません。</h5>
    <h6 class="card-subtitle mb-2 text-muted" id="spotify_artist"></h6>
    <small class="text-muted"><a href="https://spotify.com">Spotify</a> による情報, <a href="https://vercel-spotify-api.vercel.app/api/Spotify">API</a></small>
  </div>
</div>

<div class="card mt-1" style="max-width: 30rem;">
  <div class="card-body">
    <small>プレイ中</small>
    <h5 class="card-title" id="game_title">何もプレイしていません。</h5>
    <small class="text-muted"><a href="https://discord.com">Discord</a> による情報</small>
  </div>
</div>

<hr>

* 生年月日: 2001 年 11 月 19 日 ({::nomarkdown}<div id="age" style="display: inline"></div>{:/nomarkdown} 歳)
* 出身地: 日本, 鳥取県 鳥取市
* 所在地: 日本, 広島県 広島市

## 所属
* [広島市立大学](https://www.hiroshima-cu.ac.jp/) [情報科学部](https://www2.info.hiroshima-cu.ac.jp/) (2020/4 -) 学部3年 
    * 学科 / 研究室
        * [情報工学科](https://www.hiroshima-cu.ac.jp/department/sciences/info/) (2021/4 -)
        * [情報ネットワーク研究室](http://www.net.info.hiroshima-cu.ac.jp/) (2022/10 -)
    * サークル / クラブ
        * [マスコミ研究会](https://twitter.com/masukenDP) (2020/5 -)
        * [プログラミング同好会](https://twitter.com/HCU_ProgramClub) (2020/4 -)
        * [ノベルゲーム研究会](https://twitter.com/hcunovelgame) (2020/4 -)
        * [大学祭実行委員会](https://ichidaisai.com) システム局 (2022/4 -)
* 鳥取県立鳥取東高等学校 理数科 (2017/4 - 2020/3)
    * 弓道部 (2017/4 - 2019/3)

## 資格 / 免許
* TOEIC Listening & Reading (オフライン) 860点 (2022/12)
* IPA 基本情報技術者 (2022/4)
* TOEIC Listening & Reading (IPテスト) 960点 (2021/12)
* 普通自動車第一種運転免許 (AT限定, 2021/6)
* 実用英語技能検定 2級 (2018/10)
* 全日本弓道連盟 審査 1級 (2015)

## インターン
* 株式会社インターネットイニシアティブ (2022/9)
* 株式会社ヒロテック (2022/8)


## 連絡先 / SNS
<ul>
    <li><i class="fa-solid fa-phone"></i> 電話: <a href="tel:07089091949">+81 70-8909-1949</a></li>
    <li>
        <i class="fa-solid fa-envelope"></i>
        電子メール: <a href="mailto:{{ 'i@yude.jp' | encode_email }}" rel="me">i&#064;yude.jp</a></li>
    <li><i class="fa-brands fa-twitter"></i> Twitter: <a href="https://twitter.com/yude_jp" rel="me">@yude_jp</a></li>
    <li><i class="fa-brands fa-discord"></i> Discord: <a href="https://discord.com/users/116124230243975173" rel="me">yude#3205</a></li>
    <li><i class="fa-brands fa-telegram"></i> Telegram: <a href="https://t.me/yudejp" rel="me">t.me/yudejp</a></li>
    <li><i class="fa-brands fa-github"></i> GitHub: <a href="https://github.com/yude" rel="me">yude</a></li>
    <li><i class="fa-brands fa-mastodon"></i> ActivityPub (Misskey): <a href="https://mi.yude.moe/@yude" rel="me">@yude@mi.yude.moe</a></li>
    <li><i class="fa-brands fa-keybase"></i> Keybase: <a href="https://keybase.io/yude" rel="me">yude</a></li>
</ul>

その他のアカウントについては、[こちら](https://scrapbox.io/yude/%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88)を御覧ください。

## リンク
* Scrapbox: [油田](https://scrapbox.io/yude)
    * [制作物](https://scrapbox.io/yude/%E5%88%B6%E4%BD%9C%E7%89%A9)
    * [デバイス](https://scrapbox.io/yude/%E3%83%87%E3%83%90%E3%82%A4%E3%82%B9)

## 公開鍵
* [PGP](https://github.com/yude.gpg)
* [SSH](https://github.com/yude.keys)

<script async>
    let spotify_req = new XMLHttpRequest();
    spotify_req.open('GET', 'https://vercel-spotify-api.vercel.app/api/Spotify')
    spotify_req.responseType = 'json';
    spotify_req.send();
    
    spotify_req.onload = function() {
        const spotify_res = spotify_req.response;
        if (spotify_res['isPlaying']) {
            spotify_title.innerHTML = spotify_res['title'];
            spotify_artist.innerHTML = spotify_res['artist'];
        }
    }
</script>

<script async>
    let discord_req = new XMLHttpRequest();
    discord_req.open('GET', 'https://discord.com/api/guilds/723409709306216498/widget.json')
    discord_req.responseType = 'json';
    discord_req.send();
    
    discord_req.onload = function() {
        const discord_res = discord_req.response;
        if (discord_res.members) {
            if (discord_res.members[0].game) {
                game_title.innerHTML = discord_res.members[0].game.name;
            }
        }
    }
</script>

<script async>
    const now=new Date();
    const birth=new Date("2001/11/19");
  document.getElementById('age').innerHTML=(now.getFullYear() - birth.getFullYear()  +
    ( new Date( now.getFullYear() , birth.getMonth() , birth.getDate() ).getTime()
        > now.getTime() ? -1 : 0 ));
</script>

<script async>
    const isHover = e => e.parentElement.querySelector(':hover') === e;    

    let name = 'yude';
    let state = false;
    
    elm = document.getElementById('name');
    elm.innerHTML = name;
    document.getElementById('name').onmouseover = async function() {
        name += 'e';
        elm.innerHTML = name;
        for (;;) {
            name += 'e';
            elm.innerHTML = name;
            if (!(document.getElementById('name').matches(':hover'))) {
                break;
            }
            await new Promise(s => setTimeout(s, 100))
        }
    }
</script>
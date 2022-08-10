---
layout: post
title:  "Windows 11 と Arch Linux のデュアルブートを設定しました"
---

# はじめに
2022年7月に [Lenovo ThinkPad E14 Gen 3 (AMD)](https://www.lenovo.com/jp/ja/notebooks/thinkpad/e-series/ThinkPad-E14-Gen-3-14%E2%80%9D-AMD/p/22TPE14E4A3) を導入し、Windows 11 と Arch Linux のデュアルブートを設定しました。\
この記事では、その方法を備忘録として公開します。\
また、Windows 11 としていますが、UEFI でブートするように設定されている Windows 7 以上の Windows であれば問題なく実行できるはずです。

# 免責 / 注意 事項
* yude はこの記事の内容をあなたが実行した結果の責任を一切負うことができません。自己責任で行ってください。
    * Arch Linux, Gentoo Linux, Linux From Scratch などのソースベースの Linux ディストリビューションをインストールしたことがないレベルの初学者の方は、本番環境のコンピュータで行うことを全く推奨しません。パーティションテーブルを破壊しても問題のないコンピュータで実行してください。
* 操作を行う前に、必要なデータをバックアップしてください。また、インストール前に、できるだけ関係のないストレージをコンピュータから取り外しておくことを推奨します。

# 用意
インストールする前に、コンピュータが条件を満たしていることを確認します。
* UEFI に対応していること。2012 年以降に製造されたコンピュータであれば、大抵問題ありません。
* デスクトップ環境を導入する場合は 2 GB 以上のメモリ。そうでない場合は 512 MB。
* アーキテクチャが x86_64 であること。
* Apple の T2 チップ搭載 Mac 等、特殊なハードウェアでないこと。元々 Windows が稼働しているコンピュータであれば、大抵問題ありません。

その他、[インストールガイド](https://wiki.archlinux.jp/index.php/%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%82%AC%E3%82%A4%E3%83%89)に記載されている条件を満たしていることを確認してください。

# 手順
## ブート USB の準備
* まず、Arch Linux の最新の iso イメージファイルを[ダウンロード](https://www.archlinux.jp/download/)してください。
### Windows
* [Rufus](https://rufus.ie/ja/) または [balenaEtcher](https://www.balena.io/etcher/) を使うのが楽です。
### macOS
* [balenaEtcher](https://www.balena.io/etcher/) を使うのが楽です。
### Linux
* `dd` コマンドを使用して書き込みます。
    ```sh
    $ sudo dd if=archiso.iso of=/dev/sdHoge bs=1M status=progress
    ```
    * `archiso.iso` は iso イメージへのパス、`/dev/sdHoge` は USB フラッシュドライブのデバイスファイルに置き換えてください。
        * デバイスファイルは、`sudo fdisk -l` コマンド等で確認できます。
* GUI が必要な場合は、先述の [balenaEtcher](https://www.balena.io/etcher/) を使うこともできます。
## コンピュータの準備
### Windows の設定
* リアルタイムクロックを UTC 基準にします。
    * Windows は、既定の状態では時計の基準に現地時間を使いますが、これはデュアルブートにおいて相性が悪いです。
    * 以下のコマンドを管理者権限のあるターミナルで実行してください。
      ```
      reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
      ```
* 高速スタートアップとハイバネートを無効化します。
    * これにより、Windows を使用中に「休止状態」にすることができなくなりますが、Arch Linux の使用中に起きる可能性のある問題を避けることができます。
    * 「休止状態」を使用する必要がある場合は、代わりに高速スタートアップのみを無効化することができます。
        * 方法については、以下のページをご覧ください:\
          [富士通Q&A - [Windows 10] 高速スタートアップを無効にする方法を教えてください。 - FMVサポート : 富士通パソコン](https://www.fmworld.net/cs/azbyclub/qanavi/jsp/qacontents.jsp?PID=6010-9312)
    * 高速スタートアップとハイバネートを無効化するには、以下のコマンドを管理者権限のあるターミナルで実行してください。
        ```
        powercfg /h off
        ```
* パーティションを準備します。
    * Windows と Arch Linux を同じストレージ デバイスにインストールする場合は、Windows が専有しているパーティションを縮小してください。
        * 縮小する前に、ストレージに十分な空き容量を確保し、かつデフラグを行う必要がある場合もあります。
        * 方法については、以下のページをご覧ください:\
          [NEC LAVIE公式サイト > サービス＆サポート > Q&A > Q&A番号 020024 「Windows 10で、Cドライブの容量を縮小して新しくドライブを作成する方法について教えてください。」](https://faq.nec-lavie.jp/qasearch/1007/app/servlet/relatedqa?QID=020024)
    * コンピュータに内蔵ストレージ デバイスが複数取り付けられており、物理的に異なるデバイスに Arch Linux をインストールする場合は、「ディスクの管理」から事前にパーティションを初期化しておいてください。
        * 手順は以下のページを参考にしてください:\
          [新しいディスクの初期化 | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows-server/storage/disk-management/initialize-new-disks)
        * パーティションの種類については、**GPT** を選択してください。
* Windows の設定を完了したら、次は UEFI の設定を行います。
### UEFI の設定
* 操作手順はコンピュータに搭載されている UEFI によって異なるため、ここでは手順を記載せず、達成するべき目標のみを記述します。
    * セキュアブートを無効化してください。
    * ファストブートをできるだけ無効化してください。
    * ブート元デバイスの順番を調節し、USB フラッシュドライブが最初に読み込まれるようにしてください。

## Arch Linux の基本的なインストール
いよいよ、Arch Linux をストレージにインストールします。\
まずは、iso イメージを書き込んだ USB フラッシュドライブから Arch Linux をブートしてください。
### 手順
#### 1. キーマップを設定します。
* 日本語のキーボードを使用している場合は、以下のコマンドを実行します。
    ```sh
    $ loadkeys jp106
    ```
* 英字のキーボードを使用している場合は、手順をスキップしてください。
#### 2. インターネットに接続します。
* 有線で接続する場合\
LAN ケーブルをコンピュータに接続してください。
* Wi-Fi で接続する場合
1. `iwctl` コマンドを実行します。プロンプトが `[iwd]#` に変化したことを確認してください。
2. `device list` で無線 LAN アダプターの一覧を表示します。\
   `Name` の列に表示されているものを覚えるか、メモしてください。通常 `wlan0` などが該当します。\
   これはデバイス名で、ステップ 3 以降で使用します。
3. `station デバイス名 scan` で Wi-Fi ネットワークをスキャンします。
4. `station デバイス名 get-networks` で近隣にあるアクセスポイントの SSID を確認します。
5. `station デバイス名 connect 目的の SSID` でアクセスポイントに接続します。
   コマンドの実行後、パスワードを求められますから入力してください。
6. `exit` で iwctl から抜けます。
#### 3. 時計を調節します。
* NTP サーバから正しい時刻を取得します。
    ```sh
    $ timedatectl set-ntp true
    ```
#### 4. パーティションを初期化します。
1. 目的のパーティションのデバイスファイルの場所を確認します。
    ```sh
    $ fdisk -l
    ```
デバイス の列に表示されているものが、デバイスファイルの場所です。\
いくつか表示されているもののうち、次に該当するものをメモしておきます。
* タイプが "EFI システム" となっているもの。
* Arch Linux をインストールする先のパーティション
    * 「Windows の設定」で用意したパーティションのデバイス ファイルをメモしてください。
    * 明確なラベル等は表示されないため、パーティションの順序・大きさ等から目的のパーティションを特定してください。
        * もしくは、一時的にマウントして目的のパーティションであるかどうかを確認できます:
        ```sh
        # NTFS のパーティションをマウントするために必要
        $ pacman -S ntfs-3g
        # マウントする
        ## ここでエラーが発生するとき、「パーティションの中身を表示する」をスキップしてください。
        ## エラーが発生する場合は、この手順で目的のパーティションであるかどうかを特定することは危険です。
        $ mount --mkdir [パーティションのデバイス ファイルの場所] /tmp/hogepart
        # パーティションの中身を表示する
        $ ls /tmp/hogepart
        ```
2. Arch Linux をインストールするパーティションを ext4 でフォーマットします。
* ext4 は Linux において最も一般的なファイルシステムです。
* 次のコマンドでフォーマットできます:
    ```sh
    $ mkfs.ext4 [ステップ 1 で確認したデバイスファイルのパス]
    # 例: mkfs.ext4 /dev/sda2 または mkfs.ext4 /dev/nvme1n1p2 など。
    ```

#### 5. 必要なパーティションをマウントします。
* マウントとは、ストレージ デバイスの中にある特定のパーティションと、自分が現在アクセスできる何らかのディレクトリを関連付ける操作のことをいいます。
1. Linux のインストール先のパーティションをマウントします。
    ```sh
    $ mount [ステップ 1 で確認したデバイスファイルのパス] /mnt
    # 例: mount /dev/sda2 /mnt または mount /dev/nvme1n1p2 /mnt など。
    ```
2. EFI パーティションをマウントします。
    ```sh
    $ mount --mkdir [ステップ 1 で確認したデバイスファイルのパス] /mnt/boot
    # 例: mount /dev/sda1 /mnt または mount /dev/nvme1n1p0 /mnt など。
    ```

### 6. 基本的な Linux システムのインストール
Arch Linux の基本的な内容をインストールするには、`pacstrap` コマンドを使用します。\
* 実用的な Linux システムをインストールするには、次のように実行します。
    ```sh
    $ pacstrap /mnt base base-devel linux linux-firmware nano neofetch sudo networkmanager git grep refind intel-ucode bash-completion
    ```
* `pacstrap` の説明
    * 第1引数には、Linux をインストールするパーティションのマウント先を指定します。
    * 第2引数以降には、Linux システムを初期化するとともにインストールしたいパッケージを列挙します。
        * 基本的には、例示されているパッケージを削らないでください。これからのステップでは、これらのパッケージがインストール済みであることを前提に進むからです。
        * パッケージの説明 (一部省略)
            * `base`, `linux`, `linux-firmware`: Arch Linux を構成する基本的なパッケージ / グループで、必須です。
            * `base-devel`: パッケージをビルドしたりするための開発用ツールの集合です。
            * `nano`: CLI で使えるテキストエディタです。`vim` などに置き換えることができます。
            * `neofetch`: システムの概要を表示します。
            * `sudo`: 一時的にユーザーに特権を許します。
            * `networkmanager`: ネットワークへの接続を司ります。
            * `git`: バージョン管理システム Git のクライアントです。
            * `intel-ucode`: Intel 製 CPU のマイクロコードです。CPU がリリースされた後に発見されたバグなどを修正します。(**AMD 製 CPU をお使いの方は、代わりに `amd-ucode` をインストールしてください。**)

### 7. インストールした Arch Linux を設定します。
1. fstab を生成します。
`/etc/fstab` というファイルがあり、ここには Linux システムがどのパーティションを起動時等にどこにマウントすべきかを記述します。\
以下のコマンドで、自動的に生成できます。
    ```sh
    $ genfstab -U /mnt >> /mnt/etc/fstab
    ```
2. chroot でインストールした Linux システムに憑依します。
インストールしたシステムに入り込んで、詳細な設定を行います。
    ```sh
    $ arch-chroot /mnt
    ```
3. タイムゾーンを設定します。
以下のコマンドを実行して、タイムゾーンを設定します。日本にお住まいの場合は以下のコマンドを実行してください。
    ```sh
    $ sudo timedatectl set-timezone Asia/Tokyo
    $ hwclock --systohc
    ```

4. 国際化
Linux システムに日本語を教えます。
1. `/etc/locale.gen` を `nano` などのテキストエディタで開き、以下の内容に該当する行のコメントアウトを解除してください。
    ```
    en_US.UTF-8
    ja_JP.UTF-8
    ```
2. 以下のコマンドを実行して、キーマップを設定します。
    ```sh
    $ localectl set-keymap jp106
    ```
3. 以下のコマンドを実行して、言語ファイルを生成します。
    ```sh
    $ locale-gen
    ```

5. コンピュータのホスト名を設定します。
英数字を用いて、コンピュータの名前を設定してください。ただし、先頭に数字が来ないようにしてください。\
以下のコマンドを実行することで、設定できます。
    ```sh
    $ echo [コンピュータの名前] >> /etc/hostname
    # 例: echo "arch" >> /etc/hostname
    ```

6. コンピュータのアカウントを設定します。
    * まず、root アカウントのパスワードを設定します。以下のコマンドを実行してください。
    ```sh
    $ passwd
    ```
    * 次に、自分が普段使用するアカウントを作成し、パスワードを設定します。以下のコマンドを実行してください。
    ```sh
    # 以下の例では、自分のアカウントを wheel グループ (管理者) に所属させ、シェルに Bash を使うようにします。
    # 名前は、英数字で設定してください。
    $ useradd -m -G wheel -s /bin/bash 名前
    # パスワードを設定します。
    passwd 名前
    ```
    * `wheel` グループが `sudo` コマンドを使用できるようにします。
    `sudo` の設定ファイルは、`EDITOR=nano visudo` コマンドを実行すると開けます。\
    以下の内容を、開いたテキストファイルに**追記**してください。
    ```
    %wheel ALL=(ALL) ALL
    ```

7. 必要なサービスの有効化
普段使用するサービスを、Linux の起動時に同時に起動させるようにしておきます。\
以下のコマンドを実行してください。
```sh
$ sudo systemctl enable NetworkManager.service
```

8. ブートローダの設定
Linux を呼び出すには、ブートローダーが必要です。今回は [rEFInd](https://wiki.archlinux.jp/index.php/REFInd) という優れたブートローダーを使用します。\
以下に手順を示します。
    1. 以下のコマンドで、基本的なファイルを自動的に生成します。
    ```sh
    $ refind-install
    ```
    2. `/boot/refind_linux.conf` を編集します。
    * 作業前に、ファイルをバックアップしておきます。以下のコマンドを実行してください。\
    ```sh
    cp /boot/refind_linux.conf /boot/refind_linux.conf.bak
    ```
* 以下のコマンドを実行して、rEFInd を設定します。
```sh
echo "\"Boot with standard options\" \"root=UUID=$(blkid [Linux をインストールしたパーティションのデバイス ファイルの場所] -s UUID -o value) rootfstype=ext4 rw splash\""
```

#### 9. 基本的なセットアップの完了
以上で、基本的なセットアップは完了したはずです。`exit` コマンドを実行して chroot から抜け、`reboot` で再起動します。
* 起動しない場合
    * Windows が起動してしまう場合\
    UEFI の設定で、`rEFInd Boot Manager` の優先順位を最高にしてください。
    * Emergency mode に入ってしまう場合\
    `refind_linux.conf` の記述が間違っています。もう一度手順を読み込み、やり直してください。

## 10. Arch Linux のデスクトップ環境の導入
* デスクトップ環境が必要ない場合、この手順を完全に飛ばすことができます。
* 今回は、[KDE Plasma](https://kde.org/plasma-desktop/) というデスクトップ環境を導入します。
    * スクリーンショット
    ![](https://i.imgur.com/xlxiPMR.png)

* 1. 必要なパッケージをインストールします。
    ```bash
    $ sudo pacman -Syu plasma kde-applications sddm xorg adobe-source-han-sans-jp-fonts fcitx-im fcitx-configtool fcitx-mozc kcm-fcitx
    ```

* 2. SDDM が Arch Linux の起動時に自動的に立ち上がるようにします。
    * SDDM は、X サーバのセッションを開始する役目を担います。
    * 以下のコマンドを実行して、自動起動を有効にします。
    ```bash
    $ sudo systemctl enable sddm
    ```

* 3. 日本語入力の設定をします。
    * ホームディレクトリ以下の `.xprofile` (正確なパス: `$HOME/.xprofile`) に以下の内容を書き込んでください。
    ```
    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XMODIFIERS=”@im=fcitx”
    ```

* 4. 表示言語を日本語に設定し、キーボードレイアウトを設定します。
    ```bash
    $ sudo localectl set-locale ja_JP.UTF-8
    $ sudo localectl set-x11-keymap jp

* 5. 再起動し、Plasma を起動します。

* 6. Fcitx (日本語入力メソッド) が自動的に起動するようにします。また、入力メソッドとして登録します。
    * ここからのコマンドは、Konsole 等のターミナルエミュレータから実行するようにします。
    * 自動起動するには、以下のコマンドを実行します。
    ```bash
    $ fcitx-autostart
    ```
    * Fcitx を入力メソッドの1つとして登録します。以下のコマンドを実行して表示された画面から、Mozc を追加します。
    ```bash
    $ fcitx-configtool
    ```

* 7. もう一度再起動すると、すべての設定が完了します。

# 11. 終わりに
内容の誤り、補足、誤字・脱字 等ございましたら、[こちら](https://github.com/yudejp/yude.jp_v2/issues) までお願いします。

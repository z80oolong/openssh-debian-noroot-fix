# Debian noroot 環境において OpenSSH を動作させるための差分ファイル

## 概要

これらの差分ファイルは、標準的な SSH サーバである [OpenSSH][OSSH] のうち、安定版の [OpenSSH][OSSH] 及び [開発版の OpenSSH][OPRP] において、一部 bug fix を行い、 [Debian noroot 環境][DBNR]において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 [Android OS 5.0 以降][ANDR] における [Debian noroot 環境][DBNR]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール [```link(2)```][LINK] の実行を回避しています。

## 差分ファイルの適用とコンパイル

[OpenSSH][OSSH] のソースコードに差分ファイルを適用するには、安定版の [OpenSSH][OSSH] には、差分ファイル ```openssh-x.ypz-fix.diff (ここに、 x.y は安定版のバージョン番号であり、 pz はパッチレベル番号)``` を、[開発版の OpenSSH][OPRP] には、差分ファイル ```openssh-HEAD-xxxxxxxx-fix.diff (ここに、 xxxxxxxx は、HEAD の commit ID 番号)``` をそれぞれ適用して下さい。

例えば、安定版の [OpenSSH][OSSH] のソースコードに ```openssh-x.ypz-fix.diff``` を適用するには、安定版の [OpenSSH][OSSH] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```openssh-x.y-fix.diff``` を適用します。

```
 $ patch -p1 < /path/to/openssh-x.ypz-fix.diff
 (ここに、/path/to/diff は、 openssh-x.ypz-fix.diff が置かれたディレクトリのパス名)
```
そして、 [開発版の OpenSSH][OPRP] のソースコードに ```dropbear-HEAD-xxxxxxxx.diff``` を適用するには、 [開発版の OpenSSH][OPRP] のソースコードが置かれているディレクトリより、以下のようにして差分ファイル ```dropbear-HEAD-xxxxxxxx.diff``` を適用します。

```
 $ patch -p1 < /path/to/openssh-HEAD-xxxxxxxx.diff
 (ここに、/path/to/diff は、 openssh-HEAD-xxxxxxxx.diff が置かれたディレクトリのパス名)
```

なお、これらの差分ファイルを適用した [OpenSSH][OSSH] のソースコードを [Debian noroot 環境][DBNR]においてコンパイルするには、```./configure``` コマンドの実行時に以下のようにして、環境変数 ```CFLAGS``` に ```-DDEBIAN_NOROOT``` を設定する必要があります。

```
 $ CFLAGS="-DDEBIAN_NOROOT" ./configure --prefix=...  # (以下、適宜オプションを設定すること。)
```

## 謝辞

なお、これらの差分ファイルの作成に当たっては、 [termux の開発コミュニティ][TERM] による差分ファイルを参考にしました。 [termux の開発コミュニティ][TERM]の皆様には心より感謝致します。

### 2019/03/19 の追記

[開発版の OpenSSH][OPRP] の HEAD の commit である 9edbd782 に対応した差分ファイル ```openssh-HEAD-9edbd782-fix.diff``` を追加しました。これに伴い、差分ファイル ```openssh-7.8p1-fix.diff, openssh-HEAD-aede1c34-fix.diff```を削除しました。どうか御了承下さい。

### 2019/04/09 の追記

この度、 [Debian noroot 環境][DBNR]上の ```proot``` にて link2symlink 機能を使用している際に、 [OpenSSH][OSSH] による SFTP サーバ経由でディレクトリを読み出した場合、 link2symlink 機能が内部で使用する ```.l2s.``` で始まるファイル及びシンボリックリンクが可視化される不具合を修正しました。

これに伴い、上記不具合を修正した [OpenSSH 7.9p1][OSSH] 及び [開発版の OpenSSH][OPRP] の HEAD の commit である 5de397a8 に対応した差分ファイル ```openssh-7.9p1_1-fix.diff, openssh-HEAD-5de397a8-fix.diff``` を追加しました。

また、これに伴い、差分ファイル ```openssh-7.9p1-fix.diff, openssh-HEAD-9edbd782-fix.diff``` を削除しました。どうか御了承下さい。

### 2019/04/22 の追記

最新の安定版である [OpenSSH 8.0p1][OSSH] に対応した差分ファイル ```openssh-8.0p1-fix.diff``` を追加しました。これに伴い、差分ファイル ```openssh-7.9p1_1-fix.diff```を削除しました。どうか御了承下さい。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[OSSH]:https://www.openssh.com/
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[OPRP]:https://anongit.mindrot.org/openssh.git
[TERM]:https://termux.com/

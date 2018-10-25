# Debian noroot 環境において OpenSSH を動作させるための差分ファイル

## 概要

これらの差分ファイルは、標準的な SSH サーバである [OpenSSH][OSSH] のうち、安定版の [OpenSSH][OSSH] 及び [開発版の OpenSSH][OPRP] において、一部 bug fix を行い、 [Debian noroot 環境][DBNR]において正常に動作させる為の差分ファイルです。

これらの差分ファイルでは、 [Android OS 5.0 以降][ANDR] における [Debian noroot 環境][DBNR]において、擬似端末デバイスファイルである ```/dev/pts/*``` の所有権及び権限の変更が出来ない制約を回避し、また、システムコール [```link(2)```][LINK] の実行を回避しています。

## 差分ファイルの適用とコンパイル

[OpenSSH][OSSH] のソースコードに差分ファイルを適用するには、安定版の [OpenSSH][OSSH] には、差分ファイル ```openssh-x.ypz-fix.diff (ここに、 x.y は安定版のバージョン番号であり、 pz はパッチレベル番号)``` を、[開発版の OpenSSH][OPRP] には、差分ファイル ```openssh-HEAD-xxxxxxxx-fix.diff (ここに、 xxxxxxxx は、リビジョン番号)``` をそれぞれ適用して下さい。

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

なお、これらの差分ファイルの作成に当たっては、 [termux の開発コミュニティ][TERM] による差分ファイルを参考にしました。

[termux の開発コミュニティ][TERM]の皆様には心より感謝致します。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[OSSH]:https://www.openssh.com/
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[OPRP]:https://anongit.mindrot.org/openssh.git
[TERM]:https://termux.com/
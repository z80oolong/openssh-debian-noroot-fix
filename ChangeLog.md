# ChangeLog 一覧

本稿では、標準的な SSH サーバである [OpenSSH][OSSH] において、 [Debian noroot 環境][DBNR]にて正常に動作させる為の差分ファイルについての変更履歴の一覧を "ChangeLog 一覧" として纏めます。

なお、過去に Gist 上において "追記" として示した変更履歴についても、 "追記" の表記を "ChangeLog" と改め、最新の ChangeLog を先頭に並べ替えた上で再掲してあります。

## 2019/04/22 の ChangeLog

最新の安定版である [OpenSSH 8.0p1][OSSH] に対応した差分ファイル ```openssh-8.0p1-fix.diff``` を追加しました。これに伴い、差分ファイル ```openssh-7.9p1_1-fix.diff```を削除しました。どうか御了承下さい。

## 2019/04/09 の ChangeLog

この度、 [Debian noroot 環境][DBNR]上の ```proot``` にて link2symlink 機能を使用している際に、 [OpenSSH][OSSH] による SFTP サーバ経由でディレクトリを読み出した場合、 link2symlink 機能が内部で使用する ```.l2s.``` で始まるファイル及びシンボリックリンクが可視化される不具合を修正しました。

これに伴い、上記不具合を修正した [OpenSSH 7.9p1][OSSH] 及び [開発版の OpenSSH][OPRP] の HEAD の commit である 5de397a8 に対応した差分ファイル ```openssh-7.9p1_1-fix.diff, openssh-HEAD-5de397a8-fix.diff``` を追加しました。

また、これに伴い、差分ファイル ```openssh-7.9p1-fix.diff, openssh-HEAD-9edbd782-fix.diff``` を削除しました。どうか御了承下さい。

## 2019/03/19 の ChangeLog

[開発版の OpenSSH][OPRP] の HEAD の commit である 9edbd782 に対応した差分ファイル ```openssh-HEAD-9edbd782-fix.diff``` を追加しました。これに伴い、差分ファイル ```openssh-7.8p1-fix.diff, openssh-HEAD-aede1c34-fix.diff```を削除しました。どうか御了承下さい。

<!-- 外部リンク一覧 -->

[DBNR]:https://play.google.com/store/apps/details?id=com.cuntubuntu&hl=ja
[ANDR]:https://www.android.com/intl/ja_jp/
[OSSH]:https://www.openssh.com/
[LINK]:http://man7.org/linux/man-pages/man2/link.2.html
[OPRP]:https://anongit.mindrot.org/openssh.git
[TERM]:https://termux.com/

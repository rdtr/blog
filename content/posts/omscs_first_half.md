---
title: "GTOMSCS 前半戦振り返り"
slug: "gtomscs_first_half_semesters"
date: 2018-12-29T02:02:17-08:00
draft: false
toc: false
featuredImg: "https://en.wikipedia.org/wiki/File:Georgia_Tech_logo.svg"
tags: 
  - OMSCS
---

## What is GTOMSCS ?

[Georgia Institute of Technology](https://www.gatech.edu/)がMOOCSのスタートアップ、[Udacity](https://www.udacity.com/)と提携して提供するオンライン形式のコンピュータサイエンス専攻修士課程コース。以下のような特徴があります。

- 完全オンライン、フルタイムで働いている社会人が主な対象
- 授業はすべて録画済みのビデオ講義
- 試験は[Proctortrack](https://www.proctortrack.com/)で遠隔監視
- 最大5年まで在籍可能で、授業を取らない学期があってもよい
- 卒業時のdegreeはジョージア工科大のキャンパスのCS修士卒と同一
- アメリカの一般的な学費を考慮すると安い(公式情報で卒業までの総コストが約$7,000)

なおパートタイム修士の位置付けなので、このコースを通してアメリカで働くためのビザなどは取得できません。
あくまでキャリアアップや自己研鑽のため、という位置付けになると思います。自分は2017年秋にapplicationを提出して、acceptされて学生になりました。
コースの詳細に興味がある人は公式サイトの[Explore OMSCS](https://www.omscs.gatech.edu/explore-oms-cs)の項から読んでみると良いと思います。

卒業の要件としてGPA 3.0以上をキープしつつ30units分の単位を集める必要があり、
1科目3unitsなので10科目取れば終わりということになります。
現在5科目を終えてちょうど前半戦折り返しという時期なので、記憶が新しいうちに授業の内容や感想をここにまとめておきます。

---

### ◆ [CS 6200 Graduate Introduction to Operating Systems](https://www.udacity.com/course/introduction-to-operating-systems--ud923) (2017 Fall) 

記念すべき1科目目。OSの内部にがっつり踏み込むというよりも、

- プロセスとスレッド、スケジューリング
- プロセス間通信
- ファイルシステム
- 分散システム
  
あたりの話を非常にわかりやすく解説してくれて、ここらへんはそれこそ大学以来全く勉強してこなかったので良い復習になりました。そもそもC言語をまじめに書いたのも大学以来…
逆に普段からローレベルな実装と多少なりとも触れ合っている人には、簡単すぎるんじゃないかなと思いました。

試験はMidtermとFinalの2回で、授業を真面目に聴いていれば80-90点は取れるレベル。

Assignmentは合計3つのProjectがあって、それぞれ

(1) Multl-threading  
C言語でスクラッチでTCPのserverとclientを実装する。
両者ともコマンドライン引数でthread数を指定してマルチスレッドで動くことが要件。
個人的には要件を実装することよりもCに慣れることのほうが大変でした。

(2) Inter-Process Communication  
(1)で作ったサーバの前段にproxyコンポーネントを実装する。proxyはキャッシュ機構とかは割愛で、ただserverからコンテンツを取ってきてclientに返すのだけど、ここでproxyとserverとはTCPとかHTTPとかで通信するのではなくてSystem VかPOSIX APIの[Shared Memory](https://www.geeksforgeeks.org/posix-shared-memory-api/)の機構で物理メモリ上に共有領域を作ってデータの受け渡しをしろという課題。

そもそも複数プロセス間で直接メモリを共有する、というのをやったことなかったのでこの課題は楽しかったです。

(3) RPC  
うってかわってclientとserverをRPCで通信させろという課題。
clientはraw画像を投げるのでserverは圧縮した画像を返す（圧縮のパートは提供されている）というもので、
個人的に[SunのRPC](https://web.cs.wpi.edu/~rek/DCS/D04/SunRPC.html)の仕様を理解するのに手こずりました。

最後にExtra Credit(optionalだけど点数が追加でもらえる)として(1)〜(3)を全部つなげてclient -> proxy -> server でRPCとIPC経由で画像をやりとりするという課題もありました。

これも普段からC/C++でがりがり書いてる人には物足りない気はするんですが、個人的にはCでmutexとcondition variable使ってmaster-workerパターンのmulti thread処理を書くとかっていうのは良い経験になったと思ってます。

だいぶconcurrency系の内容にフォーカスがあたっていて、Node.jsなんかで有名なEvent Driven Modelの論文 <sup>[1](#event_driven_model_paper)</sup> とかを読む機会があったのも良し。OSの基礎の基礎を総復習できたという意味でも良かったです。
欲を言うとファイルシステムとかもcoding assignmentがあればな〜というところ。講義内容は良かったですが、結局コード書かないと知識が定着しないように思います。

ちなみにこのコースの直前に <i class="fas fa-baby"></i> が産まれたので、[flux](https://justgetflux.com/)を使って夜は画面をDarkroomモードにして毎日3:00くらいまで、<i class="fas fa-baby"></i> が起きるたびに中断しつつ講義を見たり宿題をやっていたのを覚えています。

Grade: Extra creditもこなしたのが功を奏してA。

---

### ◆ [CS 6035 Introduction to Information Security](https://www.udacity.com/course/intro-to-information-security--ud459) (2018 Spring) 

2学期目は軽めのコースを2つ取って負荷を確認してみることにしたのですが、結論からいうとフルタイムで働きつつ <i class="fas fa-baby"></i> の世話もし、2つ授業を取るというのはかなり厳しいということがわかったのでこれ以降1学期ごとに1クラス履修するようにしています。

授業のビデオと与えられた教科書は予想を遥かに超えるDryさで辛かったのと、内容が簡単すぎたので講義はスキップして、この授業は課題とテストに専念することに。

課題は毎週20問くらいのクイズ(T/F形式か選択形式)をこなすのと、4つのプロジェクトから構成されていて、プロジェクトは

(1) Stack buffer overflow  
C言語で書かれた、標準入力から受け取る文字列の長さをチェックしていないコードが与えられるので、その長さを超える入力を与えてスタックのデータを上書きしてリターンアドレスにシェルコードを仕込む、という古典的なやつでした。なかなか面白かった。

(2) Malware analysis  
VM上でWindowsマシンを動かして、その上でMalwareが複数動いているのでどういう悪さをしているのかレポートを書けというもの。Windowsのレジストリを確認したりするのは久々でした…でもあんまり面白くなかったかな。

(3) RSA暗号  
みんな知ってる[RSA暗号](https://ja.wikipedia.org/wiki/RSA%E6%9A%97%E5%8F%B7)を実装しましょうというもの。これは日本の大学院時代にもやったことがありました。[中国人剰余定理](https://ja.wikipedia.org/wiki/%E4%B8%AD%E5%9B%BD%E3%81%AE%E5%89%B0%E4%BD%99%E5%AE%9A%E7%90%86)、懐かしいです。

上のリンクにもありますがRSA暗号は特定の条件が揃うと脆弱性をついて平文を復号できてしまうのですが、それも合わせて実装する課題でした。

(4) SQL Injection  
セキュリティがガバガバなPHPとJavascriptのファイルがあたえられるので、sqlite上のデータを不正に取得したり上書いてしまうという課題。ガバガバといっても一部の文字だけはきっちりチェックする実装が入っていたりして、実装の間隙を縫って攻撃する感じが面白かったです。

テストはMidtermとFinalの2回でしたが、クイズを総復習しておけば7-8割は取れるかなという感じで、かつテストの点数配分が低いのでProjectしっかりこなしておけば問題なかったです。

Grade: プロジェクトほぼ満点で通したこともあってA。

---

### ◆ [CS 6250 Computer Networks](https://www.udacity.com/course/computer-networking--ud436) (2018 Spring) 

上記のCS6035と並行して取ったのがこの授業。こちらも正直講義はすごい単調でした。テストは3回、プロジェクトも7つというなかなかのボリューム。

内容自体はTCP/IP周りの話を非常にライトに総復習していくという感じで、ライトすぎてトピックは面白そうなのに講義を聴いてもそこまで新しい発見がなかったのも残念。個人的にはSoftware Defined Networkとかをもうちょっと深掘りしてくれると良かったのだけど。

プロジェクトに関しては、Pythonで[mininet](https://github.com/mininet/mininet/wiki/Introduction-to-Mininet)というライブラリを使って仮想的にネットワーク環境を構築して、その上で色々やってみましょうというものがメインでした。
Spanning Treeの構築は無限loopをうまいこと防ぐのがなかなか大変だったのを覚えてます。

あと真ん中の3つのプロジェクトは論文を読んで、その論文の内容をmininet上に実装したコードが既にあるので走らせてみて結果をanalyzeしろというものだったんですが、これがかなり曲者で、実行するたびに結果が全然違ったり、そもそもコードにバグがあって結果通りにならなかったり…。引っ掛けとかはなしで論文の考察通りの結果になることを期待していたので、生徒側もだいぶ困惑していました。

ただ論文の内容自体は面白かったです。GoogleのTCP Fast Open <sup>[2](#tcp_fast_open)</sup> (初回の通信でsecurity cookieを発行して、2回目以降の通信ではACKを待たないことで通信を高速化する)とか。

Grade: プロジェクトほぼ満点で通したこともあってA。

---

### ◆ [CS 7646 Machine Learning for Trading](https://www.udacity.com/course/machine-learning-for-trading--ud501) (2018 Summer) 

ちょっと気分転換も兼ねて、これまでやったことのない機械学習系の講義を受講してみました。

ちなみにこれは夏季クラスで、夏季は通常の4ヶ月の春・秋のsemesterと違って2ヶ月の短期講習です。なので必然的に講義内容は圧縮されて忙しくなる(あるいは一部の講義内容がカットされる)のですが、夏季を避けて1学期1クラスでやっていると卒業までに丸々5年かかってしまうのでそれは避けたいなということで夏季も履修していくようにしています。

この講義はなかなか面白くて、過去の株価のデータを元に色々機械学習のメソッドを適用して未来のデータを予想してみましょうというものです。投資に絡むFinanceの内容も結構がっつり講義に含まれていて正直そこは辛かった(もっと機械学習の方に集中したかった…)んですが、まあドメイン知識も無しに機械学習を適用できるわけがないだろということなのでしょう。

言語はPythonで、Pandasとnum.pyをツールとして使っていくので最初らへんの講義はほぼそのライブラリのチュートリアルと言った感じ。それを抜けると内容も機械学習っぽくなっていきます。

この講義でやるのは

- Decision Tree, Romdom Tree
- Q学習 with Dyna-Q
  
くらいなので本当にさわりレベルかなと思います。ただそれぞれの実装はoverfittingに最適なleaf sizeとか、bagging、Ensemble learningあたりまでやってくれるので、なんとなく分かった気分になれます <i class="far fa-grin-beam-sweat"></i> 

あとこの講義は教授がなかなかお茶目で、飽きずにビデオを最後まで見ることができました。う〜ん、将来チャンスがあったら機械学習系やりたいのかどうか、自分でもよくわからないですね。

Grade: プロジェクトもテストも問題なくA。

---

### ◆ [CS 6210: Advanced Operating Systems](https://www.udacity.com/course/advanced-operating-systems--ud189) (2018 Fall) 

このクラスはGTOMSCSの中でも難しいクラスの1つとして挙げられることが多いのですが、Introduction to Operating Systemsを受けてからローレベル面白いなあという気持ちがさらに高まってきたのでAdvancedもいってみようということで取りました。

が、今度こそlinuxのOS内部の話に踏み込んでいくのかと思ったら割と歴史上のOSや分散システムの機構をひたすら浅く広くsurveyしまくるというスタイルで、自分の期待していた内容とは違いました。
また、surveyスタイルの講義ということで学期を通して論文を70-80本くらい読むように指定されるんですが、子どもが成長してきて休みの日も日中はほぼ自分の時間が取れなくなったこと、仕事も忙しくなってきた影響で割と早い時点で断念してしまいました。無念 <i class="far fa-sad-tear"></i>

プロジェクトは4つあって、

(1) Virtual MachineのCPU、メモリ制御  
[libvert](https://libvirt.org/)のAPIを使って、仮想マシン間でCPU使いすぎてたら他のマシンから分け与えたり、メモリ量も適切にballooningしてやるというもの。

libvertの使い方さえ分かればそんなに難しくはないんですが、どこまで作り込めばいいのかの要件が曖昧だったのもあってなかなか手こずりました。あとこの手の宿題があるなら大学にあるクラスタを使わせてもらいたいし実際他のクラスではあったのですが、このクラスは何故か提供されなかったので自腹でGCP上で[Nested Virtualization](https://cloud.google.com/compute/docs/instances/enable-nested-virtualization-vm-instances)使って環境構築する羽目に。

(2) Barriar Synchronization  
[Open MPI](https://www.open-mpi.org/)を使って分散環境上でコミュニケーション取りつつ Tournament、Tree、DisseminationといったBarria Synchronizationを実装するもの。Psudocodeが与えられていたのでそこまで難しくはなかったです。

(3) GRPC  
モダンなトピックだけど何故これがOSの授業にあるのかはよくわからない…。まあ次のMap Reduceで必要なのでその準備段階としてのプロジェクトなのかも。C++でGRPC使ってclient-server間で通信しましょうというものでした。もちろんmulti-thread。

(4) Map-Reduce framework  
Word Countに特化した実装でいいのでGRPCを使ってmasterと複数workerでmap reduceの処理を実装するというもの。これはなかなか面白かったです。

テストはかなり難しくて、全問題が自由記述形式。個別の内容はそんなに難しくないんですがとにかく浅く広く大量のトピックを扱っているので暗記量が半端なくて、最終的に試験の数日前に <i class="fas fa-baby"></i> から強烈な風邪をもらったのも災いして期末試験の成績はふるいませんでした。むしろ39度近い熱の中試験を受けた自分を褒めたい。

後半あまりに駆け足すぎて講義内容も消化しきれてないところがあって、Consistent Hashing, DHTあたりはもう一度どこかで再度腰をすえて理解を深めたいです。

Grade: 期末テストの成績が祟って初のB。あと1、2点でAだったようなので悔しい。

---

## まとめ

こんなところです。中間地点まで来たOMSCSの感想としては、まだ出来て5年ということもあり荒削りな印象は否めないです。キャンパスで行われている授業のほんのsubsetがオンラインのフォーマットになっている現状なので、もっと授業の選択の幅が広がると良いですね。
あと個人的にシステムプログラミングの見地を深めたかったのでそこも今の所肩透かしです。（これは残りの授業によっては評価が変わるかもしれません）

@rui314さんのStanfordの授業の話とか、

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">スタンフォードのコンピュータサイエンスでどういう授業を受けているかというとこんな感じです。（昔の記事） <a href="https://t.co/2VcGqFmozn">https://t.co/2VcGqFmozn</a></p>&mdash; Rui Ueyama (@rui314) <a href="https://twitter.com/rui314/status/1075426966289842176?ref_src=twsrc%5Etfw">December 19, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

最近だと@k0kubunさんのブログとか

<blockquote class="twitter-tweet" data-lang="en"><p lang="ja" dir="ltr">日記書いた / リモートでアメリカの大学院のCSの授業を取ってみた話 - k0kubun&#39;s blog <a href="https://t.co/M76fK6I7fS">https://t.co/M76fK6I7fS</a></p>&mdash; k0kubun (@k0kubun) <a href="https://twitter.com/k0kubun/status/1076721993360134144?ref_src=twsrc%5Etfw">December 23, 2018</a></blockquote>

を読んでいると、「おぉ〜徹底的な感じでいいなあ。自分もそういうのやりたいんだよなあ」と思わないこともないです。

ただどう見てもOMSCSよりも負荷が大きそうで、今の自分の環境でそこまでrigorousな授業に耐えられるかと言われると自信が無いのと、コスト面の問題と、あとはOMSCSでも自分のcomfort zoneから出る勉強体験は確実にできていると思うし、それを楽しいと思っている自分が居るのは確かなので、とりあえずは残りの後半戦も頑張って学位をゲットしたいかなという気持ちでいます。実績のunlock、大切です <i class="fas fa-trophy"></i>

結局、本当に勉強したいことならOMSCSに固執しなくとも他の方法でできるはずですし。  
年の瀬ですが、2019年もNo learning, no lifeでいきたいと思います。

---

<a name="event_driven_model_paper">1</a>: [Flash: An Efficient and Portable Web Server](https://s3.amazonaws.com/content.udacity-data.com/courses/ud923/references/ud923-pai-paper.pdf)  
<a name="tcp_fast_open">2</a>: [TCP Fast Open](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/37517.pdf)
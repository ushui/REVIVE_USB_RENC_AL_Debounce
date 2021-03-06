# REVIVE USB よくある質問

## Q.昭光式ボタンに接続したいのですが、どのように接続したらランプが点灯しますでしょうか？

### A.以下の回路を参照下さい
動作の保証はいたしかねますが、ボタンを押している間点灯する回路として、REVIVE USBより5V、GND、スイッチ接続端子Px(xは1~12のポート)を引き出し、
以下のように接続する例が考えられます。
抵抗Rの値につきましてはスイッチの仕様に合わせた値を選定下さい。

----

# 対策版 よくある質問

## Q: 対策版を適用してもチャタリングが発生してしまいました。
### A: サンプリング周期または一致検出回数を変更することでチャタリング対策を強化できます。
ひとまず設定値を以下に変更してください。  
 - チャタリング防止設定：サンプリング周期=10ms、一致検出回数=3回
 - ロータリーエンコーダ設定：一致検出回数=2回
 
それでも改善しない場合は、さらに数値を増やして適正値を見つけてください。  
あまりに酷いようであれば、スイッチの接続に問題があるかスイッチの故障を疑ってください。  

## Q: ロータリーエンコーダを接続しましたが、動作しません。
### A: インクリメンタル形のA相/B相があるロータリーエンコーダにのみ対応しています。アブソリュート形には対応していません。
インクリメンタル形のロータリーエンコーダを使用している場合は以下を確認してください。  
 - 1相タイプ：B相がないタイプです。対応していません。
 - 2相タイプ：A相/B相の接続先が正しいピンになっていること、接続したピンにチェックを付けて設定していることを確認してください。
  A相は1ピン、B相は2ピンというように、必ず隣り合ったピンに接続する必要があります。
 - 3相タイプ：Z相には対応していないため、A相/B相のみ接続してください。

使用する方が多いかもしれませんので特記しますが、EC12E2430803やRES20D-50-201-1は2相タイプですので使用できます。

## Q: 遅延を最小限にする設定をしたいのですが、どうすればよいですか？
### A: チャタリング防止設定（＋ロータリーエンコーダ設定の一致検出回数）の値をすべて1に設定してください。
チャタリング防止機能を無効化できます。  

## Q: サンプリング周期と一致検出回数のデフォルト値の根拠は何ですか？
### A: 実体験に基づいたフィーリングです。
対策版を作成した当初はサンプリング周期=10ms／一致検出回数=3回(ロータリーエンコーダは当初から1回)でしたが、途中から4ms／2回に変更しています。  
後者の設定で賄えるパターンが実はほとんどなのでは？　と感じたので、もしもこの設定でチャタリングが起きたならば設定値を変えてもらおうという思想で作りました。  
参考までに設定値の決め方は以下です。  

#### デジタル入力
対策版ファームウェアを使用した個人的な経験では、マイクロスイッチ使用時にはサンプリング周期=3ms(一致検出回数=1回)もしくは2ms(2回)からチャタリングが起こらなくなります。  
チャタリングの確認方法は、適当なキーボード入力にしておき、何度もスイッチを押してみて、キーを1回しか入力していないのに2回入力されることがあるか、という方法です。  
経験に基づき、スイッチの劣化も考慮すると4ms(2回)くらいにしておけばいいかな、という感覚で設定しました。  

一般的にマイクロスイッチのチャタリング時間には1～10msの幅があると言われています。  
4ms(2回)の設定ならチャタリング時間=8msまでカバーできるため、おおよそこの程度で間違いはないと思います。  

#### デジタル入力(ロータリーエンコーダ)
サンプリング周期は上記項目に依存するため、一致検出回数について記載します。  
個人的な経験では一致検出回数=2回までは入力を受け取ってくれるのですが、3回以上に設定していくと徐々に反応しなくなってきます。  
これはロータリーエンコーダはマイクロスイッチ等よりもパルス出力が安定しないことによるものなので、あえて無効（=1回）にしています。  

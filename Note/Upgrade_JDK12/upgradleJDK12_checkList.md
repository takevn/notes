# JDKアップグレードをインフラと連携する #deliver
jsvc・Jetty・embulkのバージョンアップするのであれば連絡欲しい

# 方針確認
事前準備
localのDockerを起動し、
リクエストを送って、valid=1のレスポンスが返ってくることを確認する。

0. 確認仕方2通りあります。(注意：sampledataフォルダが必要)

1. commandでcurlを使う
curl -v -H "Content-Type: application/json" -X POST "localhost/dsp/bid/v1?ssp_id=1" --data @sampledata/bidsample/bidtrial/sample-gmossp-real_phase8.json
2. テストクラスからリクエストを送る
BidApiGmoSspDockerTest#doPost_GMO_SSP_phase8
1. JDK 12.0.1をダウンロードする。
https://jdk.java.net/12/
このリンクはどうですか。
https://www.oracle.com/technetwork/java/javase/downloads/jdk12-downloads-5295953.html

2. コンパイルエラーが発生していないことを確認する。
発生していれば修正する。

buildはbuild.gradleを‌sourceCompatibility = 12‌に変更して実行する。

dsp-deliverでは、( ./gradlew updateJettyWebapp)でbuildする。

dsp-manageを最新のmasterにして、

bundle exec rake db:drop db:create

bundle exec rake db:migrate db:seed

を実行する。

dsp-monitorはProject->ProjectSDK

dsp-monitorは‌./gradlew clean fatJar‌でbuildする。

3. JUnitを実行できることを確認する。

4. localのdsp-deliver、dsp-monitorのJDKを12.0.1にして起動する。
localで起動した環境にリクエストを送り、valid=1のレスポンスが返ってくることを確認する。

2019/05/20追記

DockerfileのJDKダウンロード処理も修正する。

5. ステージング環境にdeployして、リクエストを送り、valid=1のレスポンスが返ってくることを確認する。

6. dsp-batchのJDKを12.0.1にする。

7. dsp-batchでコンパイルエラーが発生していないことを確認する。
発生していれば修正する。

8. dsp-batchでembulkを使う処理を実行し、エラーが出ないことを確認する。
エラーが出た場合は、対応方法を検討する。

# JDKアップグレードをインフラと連携する
インフラ希望日は5/28(火)、5/29(水)
jsvc・Jetty・embulkのバージョンアップするのであれば連絡欲しい

jsvc 変更なし。原因：/commons-daemonが変更なし。


 buildgralde


 DBのテーブルを作成しました。
ます、dsp-manageで以下のブランチをcheckoutし、
```bundle exec rake db:migrate```
を実行してください。
https://github.com/gmo-am/dsp-manage/pull/198

その後に、dsp-cacheの最新のmasterをpullした後に、
dsp-cacheのディレクトリで、
```export JAVA_HOME=`/usr/libexec/java_home -v 10.0.2`
./build_cache.sh```
を実行してください。

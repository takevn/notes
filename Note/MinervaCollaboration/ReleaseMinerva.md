リリースMinerva
# 必ず以下のリンクをもう一度呼んでください。
https://github.com/gmo-am/dsp-batch/wiki/%E3%83%90%E3%83%83%E3%83%81%E3%82%A2%E3%83%97%E3%83%AA%E3%83%AA%E3%83%AA%E3%83%BC%E3%82%B9

# ssh
ssh dsp
ssh dsp-batch01

cd /data/dsp/dsp-batch
36  git pull
37  ./gradlew clean fatJar
38  crontab -e

KVSのデータ確認は以下のURLで出来ます。
XXXXのところはimport対象のUIDを設定してみてください
```http://mon.reemo.sp.gmossp-sp.jp/debug/kvs/v1?namespace=USER_DATA&key=XXXXX
```

minerva_collaboration.shの32行目なのですが、野田さんと話してて本番だと動かないみたいでした。
修正後の方に直すと動きそうな気がします
修正前
```$BQ extract --destination_format=NEWLINE_DELIMITED_JSON  --project_id gmo-am-minerva-prd minerva_prd_dataset.latest_seg_log_$TARGET_DATE gs://reemo_batch_ane1/minerva_prefix_*.json```
修正後
```$BQ extract --destination_format=NEWLINE_DELIMITED_JSON  gmo-am-minerva-prd:minerva_prd_dataset.latest_seg_log_$TARGET_DATE gs://reemo_batch_ane1/minerva_prefix_*.json
```

ログが出力されるディレクトリ
/data/dsp/var/log/batch-%d{yyyy-MM-dd}.%i.log

エラーが発生せず、
-- Minerva Data import: End --
というメッセージが出ていれば良い。

KVSのユーザーデータも念のため確認する。
#Log
/var/tmp/minerva_collaboration/minerva_collaboration.2019-05-27-151001.log
/data/dsp/var/log/batch-%d{yyyy-MM-dd}.%i.log


#KVS確認
kvsにデータが入っているか見てみて欲しいです。
`/data/dsp/var/data/minerva_collaboration/20190527/mn_import_1`

#confirmLink
KVSのデータ確認は以下のURLで出来ます。
XXXXのところはimport対象のUIDを設定してみてください
```http://mon.reemo.sp.gmossp-sp.jp/debug/kvs/v1?namespace=USER_DATA&key=XXXXX
```

# Show log with debug mode
`/data/dsp/dsp-batch/src/main/resources/logback.xml`
上記を編集します
以下の４６行目辺りのINFOをDEBUGに変えます
         ```<root>
                 <level value="INFO" />
                 <appender-ref ref="file4Production" />
         </root>```
本番の直接書き換えてください

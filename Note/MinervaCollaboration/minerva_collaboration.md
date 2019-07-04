minerva

# giai quyet van de khac nhau giua 2 location bang cach dung google clound platform(google storage)
https://console.cloud.google.com/storage/browser?project=reemo-173606&pli=1

echo "extract data from Minerva to ReeMo google storage :"
$BQ extract --destination_format=NEWLINE_DELIMITED_JSON  --project_id gmo-am-minerva-prd minerva_prd_dataset.latest_seg_log_$TARGET_DATE gs://reemo_batch_ane1/minerva_prefix_*.json

$BQ show --schema --format=prettyjson gmo-am-minerva-prd:minerva_prd_dataset.latest_seg_log_$TARGET_DATE > latest_seg_log_schema.json
echo "Load Minerva saved in ReeMo google storage to ReeMo BigQuery dataset:"
$BQ load --autodetect --source_format=NEWLINE_DELIMITED_JSON --project_id reemo-173606 test.minerva_latest_seg_log_$TARGET_DATE gs://reemo_batch_ane1/minerva_prefix_*.json latest_seg_log_schema.json

JARFILE=`dirname $0`/../build/libs/dsp-batch.jar
java -cp $JARFILE jp.gmoam.dsp.batch.task.MinervaCollaborationTask -env $BATCH_ENV -targetDate $TARGET_DATE

# bigQuery
以下をすることで実行が可能になりました
`gcloud auth application-default login`


# check lai phan xoa namespace
@Parameter(names = "-namespace", description = "kvs cookiesync namespace", order = 6)
private String namespace;

#===============================================================================
# develop staging productionの設定
#===============================================================================


source $SCRIPT_DIR/environment/$BATCH_ENV.sh

# threadNum required
例外の内容を再度確認して、調査します。

# note
From your report, your project is using Gradle 2.8 which was released in October 2015.

Because of its age and the need to parse Java version strings, it cannot recognise the version from a Java 12 VM.

You will need to either:

Install an older Java version compatible with your build tool and the code it builds,
Upgrade your Grade build to a more recent version - knowing that running Gradle with Java 12 support will appear in Gradle 5.4 (unreleased at this time),
Run your build with a compatible Java version and update it to fork tasks that would need to run things with Java 12.

# SQL
SELECT
 dsp_uid, STRING_AGG(DISTINCT cast(seg.id as string), "-") AS seg_id
FROM
  `${REEMO_DATASET}.minerva_latest_seg_log_${TARGET_DATE}` minerva
   , UNNEST(minerva.seg) seg
INNER JOIN
  `reemo_log.sync_master_${TARGET_DATE}` reemo
ON
  minerva.device_id = reemo.ssp_uid
GROUP BY dsp_uid



を実行してください。
https://github.com/gmo-am/dsp-manage/pull/198

その後に、dsp-cacheの最新のmasterをpullした後に、
dsp-cacheのディレクトリで、
```export JAVA_HOME=`/usr/libexec/java_home -v 10.0.2`
./build_cache.sh
```
を実行してください。


DBのテーブルを作成しました。
ます、dsp-manageで以下のブランチをcheckoutし、
```bundle exec rake db:migrate
```
を実行してください。
https://github.com/gmo-am/dsp-manage/pull/198

その後に、dsp-cacheの最新のmasterをpullした後に、
dsp-cacheのディレクトリで、
```export JAVA_HOME=`/usr/libexec/java_home -v 10.0.2`
./build_cache.sh
```
を実行してください。

# note
device_idを、ssp_uidとして扱ってください。
seg.idがセグメントIDです。
device_idと、sync_master.ssp_uidをJOINして、データをKVSに取り込みます。

chay lai file minerva_collaboration.sh
test.minerva_latest_seg_log_$TARGET_DATE
-> reeMobatch.minerva_latest_seg_log_$TARGET_DATE

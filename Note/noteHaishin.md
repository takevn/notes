note haishin

# Minerva 連携





# setting for test
-ea -Djdk.attach.allowAttachSelf

# make jar file to have minerva MinervaSegmentModel
# DBのテーブルを作成しました。
まず、dsp-manageで以下の
ブランチをcheckout：
https://github.com/gmo-am/dsp-manage/pull/198

bundle exec rake db:migrate
を実行してください。

その後に、dsp-cacheの最新のmasterをpullした後に、
dsp-cacheのディレクトリで、
export JAVA_HOME=`/usr/libexec/java_home -v 10.0.2`
./build_cache.sh
を実行してください。
# run .sh file to generate below file
lib/main/dsp-model-cache-all.jar

/build_cache.shは、
DBのschemaをもとに、
DBのデータのキャッシュを取得するためのjarファイルを生成し、
dsp-deliverとdsp-monitorにコピーしています。
dsp-deliverで、jarファイルのクラスから、Minervaのセグメントを取得して、
KVSのセグメントの比較を行います。


~/projects/dsp-monitor  master ✗ 2.4.1                                                                                      63d ⚑ ◒  
# git pull origin master
error: Your local changes to the following files would be overwritten by merge:
	lib/main/dsp-model-cache-all.jar


# mergeData function
UserDataRoot oldUserData1 = user.get();
oldUserData1.behavior().minervaCreateIfNull();
oldUserData1.behavior().minerva().segmentIdsCreateIfNull();
// ファイルから（BQから）のデータ
LinkedList<Integer> segmentIds = data.behavior().minerva().segmentIds();
segmentIds.forEach((segmentId) -> {
    // 既存のデータのsegmentIdがない場合のListに追加する
    if (oldUserData1.behavior().minerva().segmentIds().indexOf(segmentId) == -1) {
        oldUserData1.behavior().minerva().segmentIds().add(segmentId);
    }
});

# code java 8 de check vaidate minerva
Collection<AdGroupsMinervaSegmentModel> collectionAdGroupsMinervaSegmentModel = adGroup.transformAdGroupsMinervaSegmentsModels();
List<Integer> adGroupsMinervaSegmentsList = new ArrayList<Integer>();

collectionAdGroupsMinervaSegmentModel.forEach(
        (adGroupsMinervaSegmentModel) -> {
            if (adGroupsMinervaSegmentModel != null) {

                MinervaSegmentModel minervaSegmentModel = adGroupsMinervaSegmentModel.getMinervaSegmentModel();
                Integer value = minervaSegmentModel.getValue();
//                        adGroupsMinervaSegmentsList.add(adGroupsMinervaSegmentModel.getMinervaSegmentModel().getValue());
                adGroupsMinervaSegmentsList.add(value);
            }
        }
);

# code java 10 de check vaidate minerva
UserDataRoot userDataRoot = parameter.userDataMapper().userDataRoot();
LinkedList<Integer> userDataRootMinervaSegments = userDataRoot.behavior().minerva().segmentIdsCreateIfNull();

boolean match = adGroupsMinervaSegmentsList.stream().anyMatch(userDataRootMinervaSegments::contains);
//        if (!match) {
//            return AdGroupLogCode.NOT_CONTAINED_IN_TARGET_MINERVA_SEGMENT;
//        }
//        return SuccessLogCode.SUCCESS;



# error log
```
if (!result.value2().success()) {
    log.warn("KVS access failed");
    executeState.abort("invalid KVS Access");
}
```

```
kvsClient = {KVSUserDataRootClient@3293}
 client = {AeroSpikeByteBufClient@3492}
  client = {AerospikeDspClient@3493}
   client = {AerospikeClient@3494}
   writePolicy = {WritePolicy@3495}
   readPolicy = {Policy@3496}
   expiry = 15552000
   nameSpace = "development"
   setName = "userdata"
   useDigest = false
   ```
#### KVSUserDataRootClient data
```
Path kvsUserPath = Paths.get("sampledata/kvssample/user/kvs-user.json");
TestUtils.resetKvsData("GbasyCBaZxCyhJoe", KVSOperationApi.Namespace.USER_DATA.name(),
                kvsUserPath, TestEnvironment.DEVELOPMENT);
  ```

com.aerospike.client.AerospikeException: Invalid namespace: USER_DATA
com.aerospike.client.AerospikeException: Invalid namespace: userdata


###　KVS Debug Url
public enum TestEnvironment {

    DEVELOPMENT(
            "http://localhost/dsp/bid/v1",
            "http://localhost/dsp/debug/kvs/v1"
http://localhost/dsp/debug/kvs/v1?namespace=USER_DATA&key=GbasyCBaZxCyhJoe

*** migrate log  
~/projects/dsp-manage  feature/RM-433_Minerva連携 ✔ 2.4.1                                          18m  
▶ bundle exec rake db:migrate
== 20190304031120 CreateCvrAdvertiserSummaries: migrating =====================
-- create_table(:cvr_advertiser_summaries)
-- add_index(:cvr_advertiser_summaries, [:sponsor_id, :is_rt], {:unique=>true})
-- create_table(:cvr_slot_features)
-- change_column(:cvr_slot_features, :advsp_mcvr, :decimal,
== 20190422052436 CreateMinervaSegments: migrating ============================

-- create_table(:minerva_segments)
== 20190422052436 CreateMinervaSegments: migrated (0.0183s) ===================

== 20190422052536 CreateAdGroupsMinervaSegments: migrating ====================
-- create_table(:ad_groups_minerva_segments)
-- add_index(:ad_groups_minerva_segments, [:ad_group_id, :minerva_segment_id], {:unique=>true, :name=>"index_ad_groups_minerva_segments_on_ad_grp_id_and_mnrv_seg_id"})

dsp-deliverでは、
KVSから取得したデータで、ユーザーのセグメントを判定し、
広告グループに設定したセグメントに該当するユーザーにだけ配信するようにします。
DBのad_groupsにカラムを追加する必要があります
-> まだ追加していない？

Q: Dsp-deliverの作業はなんのテーブルを修正しますか？
A: 新規に作成することになると思います。
セグメントテーブルと広告グループとセグメントテーブルの関連テーブルの２つです。
-> というのはminerva_segments　と ad_groups_minerva_segmentsですね。

-> ad_groups_minerva_segmentsの構成 [:ad_group_id, :minerva_segment_id],
　　minerva_segmentsの構成は？

修正を行うクラスは、
dsp-deliverのAdGroupValidatorWithRequest.javaです。
このクラスは、広告グループのvalidationを行うクラスで、
validationを通過した広告グループだけに、配信するようにしています。
validationエラーになった場合は、エラーコードを返します。
エラーコードは、AdGroupLogCode.javaのenumの一番下に、
```
NOT_CONTAINED_IN_TARGET_MINERVA_SEGMENT("ユーザーが配信対象のMinervaセグメントに含まれていなかった")
```
を追加し、それを使用してください。

validationは、doValidateというメソッドで行なっているので、
既存のものと同じように、minervaのチェック処理を追加してください。



@noda-takahiro
adGroup.getAdGroupsMinervaSegments().add(1L);
KVSのモックの仕方：
```
        LinkedList<Long> linkedList = new LinkedList<Long>(Arrays.asList(1L, 2L));
        params.userDataMapper().userDataRoot().behavior().minervaCreateIfNull();
        params.userDataMapper().userDataRoot().behavior().minerva().segmentIdsCreateIfNull();
        params.userDataMapper().userDataRoot().behavior().minerva().segmentIds(linkedList);
```
モデルからデータのモックの仕方：
```
        Set<Long> segmentIds = new HashSet<Long>(Arrays.<Long>asList(1L, 2L));
        adGroup.getAdGroupsMinervaSegments().add(1L);　// ここにエラーが出ます。
```
質問：adGroupのMinervaSegmentsはどのようにモックしますね？

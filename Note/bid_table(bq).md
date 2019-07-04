# bid Table
log.site. fqdn domain

# BQのBidテーブルのカラムから→MariaDBのCommonDomainテーブルに保存する。
log.site. ssp_id	INTEGER	NULLABLE    -> ssp_id INTEGER	NULLABLE
log.site. fqdn	STRING	NULLABLE      -> domain STRING	NULLABLE
log.site. url	STRING	NULLABLE        -> sample_url STRING	NULLABLE
審査状態 {0:"未審査", 1:"許可", 2:"拒否"} -> review {0:"未審査", 1:"許可", 2:"拒否"}

domain (https, サブドメインをのぞいて  )
isInWhiteList　（可否未→０、１、２ornull、０、１） -> 審査状態 {0:"未審査", 1:"許可", 2:"拒否"}
sample_url
URL_例


t.string :fqdn, limit: 255, null: false, comment: 'FQDN(サブドメイン名＋ドメイン名)'
t.string :domain, limit: 255, null: false, comment: 'ドメイン名。サブドメインを含まない部分'
  

フィールド名	タイプ	モード	説明
time	TIMESTAMP	NULLABLE
ip	STRING	NULLABLE
method	STRING	NULLABLE
len	STRING	NULLABLE
uri	STRING	NULLABLE
https	STRING	NULLABLE
qs	STRING	NULLABLE
status	STRING	NULLABLE
sent	STRING	NULLABLE
ref	STRING	NULLABLE
ua	STRING	NULLABLE
forwarded	STRING	NULLABLE
req_time	STRING	NULLABLE
app_time	STRING	NULLABLE
log	RECORD	NULLABLE
log. v	FLOAT	NULLABLE
log. action	STRING	NULLABLE
log. req_id	STRING	NULLABLE
log. valid	INTEGER	NULLABLE
log. reason	STRING	NULLABLE
log. imp	RECORD	NULLABLE
log.imp. id	STRING	NULLABLE
log.imp. slot_id	STRING	NULLABLE
log.imp. floor	FLOAT	NULLABLE
log.imp. auction_type	INTEGER	NULLABLE
log.imp. x	INTEGER	NULLABLE
log.imp. y	INTEGER	NULLABLE
log.imp. banner_type	INTEGER	NULLABLE
log.imp. plcmtcnt	INTEGER	NULLABLE
log.imp. pos	INTEGER	NULLABLE
log.imp. slot_ave_ctr	FLOAT	NULLABLE
log.imp. slot_ave_cvr	FLOAT	NULLABLE
log.imp. slot_inview_ratio	FLOAT	NULLABLE
log.imp. rtb_ctr	FLOAT	NULLABLE
log.imp. rtb_iv_ratio	FLOAT	NULLABLE
log.imp. allowed_ad_types	INTEGER	REPEATED
log.imp. phase	INTEGER	NULLABLE
log.imp. context	INTEGER	NULLABLE
log.imp. plcmttype	INTEGER	NULLABLE
log. imps	RECORD	REPEATED
log.imps. id	STRING	NULLABLE
log.imps. slot_id	STRING	NULLABLE
log.imps. floor	FLOAT	NULLABLE
log.imps. auction_type	INTEGER	NULLABLE
log.imps. x	INTEGER	NULLABLE
log.imps. y	INTEGER	NULLABLE
log.imps. banner_type	INTEGER	NULLABLE
log.imps. plcmtcnt	INTEGER	NULLABLE
log.imps. pos	INTEGER	NULLABLE
log.imps. slot_ave_ctr	FLOAT	NULLABLE
log.imps. slot_ave_cvr	FLOAT	NULLABLE
log.imps. slot_inview_ratio	FLOAT	NULLABLE
log.imps. rtb_ctr	FLOAT	NULLABLE
log.imps. rtb_iv_ratio	FLOAT	NULLABLE
log.imps. allowed_ad_types	INTEGER	REPEATED
log.imps. phase	INTEGER	NULLABLE
log.imps. context	INTEGER	NULLABLE
log.imps. plcmttype	INTEGER	NULLABLE
log. site	RECORD	NULLABLE
log.site. ssp_id	INTEGER	NULLABLE
log.site. pub_id	STRING	NULLABLE
log.site. site_id	STRING	NULLABLE
log.site. slot_id	STRING	NULLABLE
log.site. name	STRING	NULLABLE
log.site. fqdn	STRING	NULLABLE
log.site. url	STRING	NULLABLE
log.site. kw	STRING	NULLABLE
log.site. ref	STRING	NULLABLE
log.site. cat	STRING	NULLABLE
log.site. sub_cat	STRING	REPEATED
log.site. search	STRING	NULLABLE
log.site. ctr	FLOAT	NULLABLE
log.site. cvr	FLOAT	NULLABLE
log.site. inview_ratio	FLOAT	NULLABLE
log.site. dom_type	INTEGER	NULLABLE
log.site. app	INTEGER	NULLABLE
log.site. rtb_ctr	FLOAT	NULLABLE
log.site. rtb_iv_ratio	FLOAT	NULLABLE
log.site. ma_id	STRING	NULLABLE
log.site. bundle	STRING	NULLABLE
log.site. store_url	STRING	NULLABLE
log. user	RECORD	NULLABLE
log.user. ua	STRING	NULLABLE
log.user. ip	STRING	NULLABLE
log.user. ssp_uid	STRING	NULLABLE
log.user. dsp_uid	STRING	NULLABLE
log.user. os_id	INTEGER	NULLABLE
log.user. dev_id	INTEGER	NULLABLE
log.user. pf_id	INTEGER	NULLABLE
log.user. has_rt	INTEGER	NULLABLE
log.user. has_cookie_sync_uid	INTEGER	NULLABLE
log.user. long_term_storage	INTEGER	NULLABLE
log.user. dnt	INTEGER	NULLABLE
log.user. user_seg	RECORD	REPEATED
log.user.user_seg. segs	STRING	REPEATED
log. bids	RECORD	REPEATED
log.bids. bid_id	STRING	NULLABLE
log.bids. imp_id	STRING	NULLABLE
log.bids. agency_id	INTEGER	NULLABLE
log.bids. advertiser_id	INTEGER	NULLABLE
log.bids. campaign_id	INTEGER	NULLABLE
log.bids. ad_group_id	INTEGER	NULLABLE
log.bids. creative_group_id	INTEGER	NULLABLE
log.bids. creative_id	INTEGER	NULLABLE
log.bids. bid_price	FLOAT	NULLABLE
log.bids. raw_bid_price	FLOAT	NULLABLE
log.bids. creatable_type	STRING	NULLABLE
log.bids. aa_id	STRING	NULLABLE
log.bids. ext_type	INTEGER	NULLABLE
log. logcode	RECORD	REPEATED
log.logcode. ad_group_id	INTEGER	NULLABLE
log.logcode. codes	INTEGER	REPEATED
log. feedbacks	RECORD	REPEATED
log.feedbacks. request_id	STRING	NULLABLE
log.feedbacks. index	INTEGER	NULLABLE
log.feedbacks. status	INTEGER	NULLABLE
log.feedbacks. cpm	FLOAT	NULLABLE
log. model	RECORD	NULLABLE
log.model. user_feature	RECORD	NULLABLE
log.model.user_feature. prob_man	FLOAT	NULLABLE
log.model.user_feature. ctr	FLOAT	NULLABLE
log.model.user_feature. cv_re	INTEGER	NULLABLE
log.model.user_feature. cv_fq	INTEGER	NULLABLE
log.model.user_feature. rt_re	INTEGER	NULLABLE
log.model.user_feature. rt_fq	INTEGER	NULLABLE
log.model.user_feature. cl_re	INTEGER	NULLABLE
log.model.user_feature. cl_fq	INTEGER	NULLABLE
log.model. adv	RECORD	REPEATED
log.model.adv. advertiser_id	INTEGER	NULLABLE
log.model.adv. i_re	INTEGER	NULLABLE
log.model.adv. re	INTEGER	NULLABLE
log.model.adv. i_fq	INTEGER	NULLABLE
log.model.adv. fq	INTEGER	NULLABLE
log.model.adv. cv_re	INTEGER	NULLABLE
log.model.adv. cv_fq	INTEGER	NULLABLE
log.model.adv. rt_re	INTEGER	NULLABLE
log.model.adv. rt_fq	INTEGER	NULLABLE
log.model.adv. cl_re	INTEGER	NULLABLE
log.model.adv. cl_fq	INTEGER	NULLABLE
log.model.adv. t_cpa	INTEGER	NULLABLE
log.model.adv. sec_id	INTEGER	NULLABLE
log.model.adv. ctr	FLOAT	NULLABLE
log.model.adv. s_ctr	FLOAT	NULLABLE
log.model.adv. u_ctr	FLOAT	NULLABLE
log.model.adv. ud	FLOAT	NULLABLE
log.model. predicts	RECORD	REPEATED
log.model.predicts. imp_id	STRING	NULLABLE
log.model.predicts. advertiser_id	INTEGER	NULLABLE
log.model.predicts. ad_group_id	INTEGER	NULLABLE
log.model.predicts. aa_id	STRING	NULLABLE
log.model.predicts. p_ctr	FLOAT	NULLABLE
log.model.predicts. p_cvr	FLOAT	NULLABLE
log.model.predicts. p_win	FLOAT	NULLABLE
log.model.predicts. net	FLOAT	NULLABLE
log.model.predicts. win_idx	INTEGER	NULLABLE
log.model.predicts. p_cpa	FLOAT	NULLABLE
log.model.predicts. p_cpc	FLOAT	NULLABLE
log.model.predicts. beta	FLOAT	NULLABLE
log.model.predicts. gamma	FLOAT	NULLABLE
log.model.predicts. ctr_thresh	FLOAT	NULLABLE
log.model.predicts. ctr_average	FLOAT	NULLABLE
log.model.predicts. softmax_prob	FLOAT	NULLABLE
log.model.predicts. softmax_net	FLOAT	NULLABLE
log.model.predicts. gross	FLOAT	NULLABLE
log.model.predicts. target_optimize_type	INTEGER	NULLABLE
log.model.predicts. features	FLOAT	REPEATED
log.model.predicts. adg_seg	RECORD	REPEATED
log.model.predicts.adg_seg. segs	STRING	REPEATED
log.model.predicts. ad_groups	RECORD	REPEATED
log.model.predicts.ad_groups. ad_group_id	INTEGER	NULLABLE
log.model.predicts.ad_groups. p_win	FLOAT	NULLABLE
log.model.predicts.ad_groups. net	FLOAT	NULLABLE
log.model.predicts.ad_groups. win_idx	INTEGER	NULLABLE
log.model.predicts.ad_groups. p_cpa	FLOAT	NULLABLE
log.model.predicts.ad_groups. p_cpc	FLOAT	NULLABLE
log.model.predicts.ad_groups. beta	FLOAT	NULLABLE
log.model.predicts.ad_groups. gamma	FLOAT	NULLABLE
log.model.predicts.ad_groups. ctr_thresh	FLOAT	NULLABLE
log.model.predicts.ad_groups. ctr_average	FLOAT	NULLABLE
log.model.predicts.ad_groups. softmax_prob	FLOAT	NULLABLE
log.model.predicts.ad_groups. softmax_net	FLOAT	NULLABLE
log.model.predicts.ad_groups. gross	FLOAT	NULLABLE
log.model.predicts.ad_groups. target_optimize_type	INTEGER	NULLABLE
log. ab_test	RECORD	NULLABLE
log.ab_test. test_cases	RECORD	REPEATED
log.ab_test.test_cases. setting_id	STRING	NULLABLE
log.ab_test.test_cases. case_id	STRING	NULLABLE
log. bid_phase	RECORD	NULLABLE
log.bid_phase. phase	INTEGER	NULLABLE
log. momentum	RECORD	NULLABLE
log.momentum. nbr	STRING	NULLABLE
log.momentum. fraud	RECORD	NULLABLE
log.momentum.fraud. valid	INTEGER	NULLABLE
log.momentum.fraud. fraud	INTEGER	NULLABLE
log.momentum.fraud. accuracy	INTEGER	NULLABLE
log.momentum.fraud. key	INTEGER	NULLABLE
log.momentum.fraud. expiry	INTEGER	NULLABLE
log.momentum. valid	INTEGER	NULLABLE
log.momentum. res_time	INTEGER	NULLABLE

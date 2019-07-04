
現在：insert row by row
insert into common_white_domains
get id in common_white_domains、IDをとって、
それからcommon_white_domain_reviewsにInsertします。

改善版：
一括common_white_domainsに追加して、
もう一回ループでドメイン名でcommon_white_domainsを検索して、IDをとって、
それからcommon_white_domain_reviewsにInsertします。

改善版の場合はもう一度ループしないといけないですが、そっちの方がいいかな。
とりあえず、コードを作成して、どっちの方が早いのがわかると思います。



insert into common_white_domain_reviews

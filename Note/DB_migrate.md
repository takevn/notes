# Migrate DB
 bin/rails generate migration create_domains_ssp

DBのテーブルを作成しました。

ます、dsp-manageで以下のブランチをcheckoutし、
migrate:
bundle exec rake db:migrate
rollback:
bundle exec rake db:rollback

rake db:version
Current version: 20131002104226
ls db/migrate
20130927063810_create_users.rb
20130927093118_create_tasks.rb
20130928114148_add_password_to_users.rb
20130929025154_add_adm_to_users.rb
20131002103504_create_tags.rb
20131002104226_create_task_tags.rb

curl -v localhost/dsp/health/v1

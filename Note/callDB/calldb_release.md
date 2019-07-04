calldb release
STG: https://150.95.149.73/
https://150.95.149.73/admin/login
manhbv/123456
manh-admin/manh-admin123456
Honban: https://150.95.237.45/
https://150.95.237.45/admin/login

リリースの流れは以下で:
* feature/import_and_check_contracted_product をdevelop へマージ
* 150.95.149.73 にデプロイ
* https://150.95.149.73/ で動作確認
* develop をmaster へマージ
* backup data on stg and master,
note: dump table only
https://stackoverflow.com/questions/5387619/how-to-import-a-single-table-in-to-mysql-database-using-command-line/18047421
dump command: mysqldump -u root -p -t calldb contracted_products product_names > calldb_contracted_products_product_names_20190527.dump
copy from stg to CI: scp root@192.168.9.2:/root/calldb_contracted_products_product_names_20190527.dump .
copy from CI to master: scp calldb_contracted_products_product_names_20190527.dump root@192.168.10.1:/root/

* 150.95.149.73 にデプロイ
***CALLDB***-deploy:~/longta/call-db
 (feature/private_net)
$ ansible-playbook -i hosts.prd deploy.yml
* データベースマイグレーション
[root@PRD-calldb-web-01 ~]# cd /var/www/calldb/
[root@PRD-calldb-web-01 calldb]# php artisan migrate

* https://150.95.237.45/ で動作確認
* 150.95.149.73 において商材データ周りのテーブルのみをダンプして、150.95.237.45 でリストア
mysql -u root -p calldb < calldb_contracted_products_product_names_20190527.dump
* https://150.95.237.45/ で動作確認

* setting crontab for laravel
- check report.txt file
cd resources/import/
- setting crontab for laravel(chú ý setting cả 2 máy web, máy 10.5 và 10.6  )
[root@PRD-calldb-web-02 import]# cat /var/spool/cron/calldb
#Ansible: Laravel Scheduler
* * * * * php /var/www/calldb/artisan schedule:run >> /dev/null 2>&1

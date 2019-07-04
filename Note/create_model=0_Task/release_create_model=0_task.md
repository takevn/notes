create_mode release

1. まずは、dsp-batchのPRをマージする所からです。
2.


2. Check table on bq:
reemo_batch.reset_create_model_advertisers_20190611

show list of changed advertiser_id

# khi can tao thu muc bang crontab:
thi them doan:
`mkdir -p /var/tmp/reset_create_model_at_unnecessary_advertisers &&`
vao
37 15 * * tue  mkdir -p /var/tmp/reset_create_model_at_unnecessary_advertisers && /data/dsp/dsp-batch/commands/reset_create_model_at_unness

sau khi check ket qua, vao crontab -e de setting lai dung thoi diem nhu setting ban dau

# search history of commands
$ history | grep command-name
$ history | egrep -i 'scp|ssh|ftp'

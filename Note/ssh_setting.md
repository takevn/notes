less ~/.ssh/id_rsa.pub

~/.ssh/config
```
Host dsp
  HostName test01.z.gmossp-sp.jp
  Port 10022
  User dsp
  IdentityFile    ~/.ssh/id_rsa.XXXX
  AddKeysToAgent yes
  UseKeychain yes
```
`~/.ssh/id_rsa.XXXX` の部分は秘密鍵の場所に書き換えてください
configの権限は `-rw-r--r--` これで作ってください
`ssh dsp`で接続できる

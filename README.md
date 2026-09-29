# Docker-Mail-Server
Custom prepared mail server using Dovecot, postfix and roundcube

Check out ready to run docker compose file.<br>
Only requirement is to create a new account in mailserver container using:
```bash
setup email add test@archiwum.local
```
and adding php code from docker compose to config file in roundcube if running loccaly.<br>

If needed sync mails:
Install **imapsync** on linux, then try to connect:
```bash
imapsync --host1 server_host --port1 993 --ssl1 --user1 "user@domain.com" --password1 "TestPassword1!" --host2 local-docker-mail-server --port2 993 --ssl2 --user2 "test@archive.local" --password2 "TestPassword2!" --justlogin
```
If you need to login via sso and need to get token you need to install/download **oauth2_imap**, when downloaded and extracted run below commands:
```bash
cd oauth2_imap/
mkdir -p ./tokens

./oauth2_imap --provider host-like-office365 --remotebrowser --token_file ./tokens/host-like-microsoft.txt "user@domain.com"
```
and do this to try connect using token:
```bash
imapsync --host1 server_host --port1 993 --ssl1 --user1 "user@domain.com" --oauthaccesstoken1 "./tokens/host.txt" --host2 local-docker-mail-server --port2 993 --ssl2 --user2 "test@archive.local" --password2 "TestTest123!" --justlogin
```

To run the copy mails process change:
```bash
- --justlogin
into
+ --automap
```
<br><br>

Docker compose contains **Kopia** instance to make backups of archived mails.

## Useful links:
[Docker Mail Server](https://github.com/docker-mailserver/docker-mailserver)

[Roundcube](https://roundcube.net/)

[Imapsync](https://github.com/imapsync/imapsync)

[oauth2_imap](https://imapsync.lamiral.info/oauth2/)

[Kopia](https://kopia.io/)

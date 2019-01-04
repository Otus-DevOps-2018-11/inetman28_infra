# inetman28_infra
inetman28 Infra repository

bastion_IP = 35.205.225.172

someinternalhost_IP = 10.132.0.3

testapp_IP = 35.199.179.182

testapp_port = 9292

# добавить ключ в ssh-agent
ssh-add ~/.ssh/github
Identity added: /home/ruslan/.ssh/github (/home/ruslan/.ssh/github)
# проверить, добавился ли ключ
ssh-add -L
<вывод обрезан>
# подключение к someinternalhost через bastion
ssh -J ruslan@35.205.225.172 ruslan@10.132.0.3

# дополнительная проверка
ruslan@someinternalhost:~$ hostname
someinternalhost

# для подключения к someinternalhost с помощью альяса someinternalhost добавить в ~.zshrc строку:
alias someinternalhost="ssh -J ruslan@35.205.225.172 ruslan@10.132.0.3"


# развернуть приложение Reddit в GCP

gcloud compute instances create reddit-app-with-startup-script01 \
--boot-disk-size=10GB \
--image-family ubuntu-1604-lts \
--image-project=ubuntu-os-cloud \
--machine-type=g1-small \
--tags puma-server \
--restart-on-failure \
--metadata-from-file startup-script=startup-script.sh


# разрешить TCP 9292 к VM с тэгом puma-server
gcloud compute firewall-rules create puma-server-gcloud \
--allow tcp:9292 \
--direction ingress \
--target-tags puma-server

# inetman28_infra
inetman28 Infra repository

# Лабораторная работа №10. Ansible-1

Я склонировал репозиторий с reddit приложением в /home/appuser на app виртуальной
машине с помощью модуля Ansible и модуля git.
Затем, с помощью модуля command и ansible я удалил репозиторий из home пользователя
appuser.
Затем снова запустил playbook и у меня появилось информация, что после 
выполнения произошли изменения (changed). До этого вместо changed ansible
возвращал ok (вместо changed) из-за индепотенции. Ansible и модуль git
видели, что изменений нет, и возвращали ok не снося никаких changed. 

# Лабораторная работа №9. Terraform-2

Выполнены все основные задания.

- С помощью терраформа теперь можно создатьва тестовое и продакшн окружение
- Параметризированы переменные насколько это считается нужным
- Появилась возможно переиспользования кода с помощью modules
- Среда разработка доступна из любой точки мира
- Продакшн среда доступна только с моего компуктера :)


# Лабораторная работа №8
Выполнены все основые задания.

Были развернуты тестовые VM на основе тестовых images созданных в Packer в лабораторной работе №7. Было запущено приложение "reddit".
С помощью Terraform я понял основу практики IaC.

Были добавлены след. файлы:
- main.tf
- variables.tf
- terraform.tfvars (terraform.tfvars.example)
- outputs.tf

В конце лабораторной работы резурсы были "разрушены".

# Лабораторная работа №7

Выполнены все задания (исключая задания со *).
variables.json добавлен в .gitignore


# Лабораторная работа №6

Задание №1

testapp_IP = 35.199.179.182

testapp_port = 9292

Доп. задание №1 - Развернуть приложение Reddit в GCP с startup-script.sh

  gcloud compute instances create reddit-app-with-startup-script01 \
--boot-disk-size=10GB \
--image-family ubuntu-1604-lts \
--image-project=ubuntu-os-cloud \
--machine-type=g1-small \
--tags puma-server \
--restart-on-failure \
--metadata-from-file startup-script=startup-script.sh

Доп. задание №2 - Разрешить TCP 9292 к VM с тэгом puma-server

gcloud compute firewall-rules create puma-server-gcloud \
--allow tcp:9292 \
--direction ingress \
--target-tags puma-server


# Лабораторная работа №5

bastion_IP = 35.205.225.172

someinternalhost_IP = 10.132.0.3



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

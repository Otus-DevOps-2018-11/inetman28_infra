# inetman28_infra
inetman28 Infra repository

bastion_IP = 35.205.225.172
someinternalhost = 10.132.0.3

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


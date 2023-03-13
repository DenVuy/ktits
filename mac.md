#Mac os 
###Создание скрытой папки 
1. command + space -> terminal (ter)
2. сжать до минимума 
3. убрать в самый край + open люб прогу
4. cd 
5. mkdir <folder_name>
6. chflags hidden <folder_name>
7. cd <folder_name>
8. curl <domen> -o <file_name>

###Подлючение к серверу 
ssh root@ip

###Текстовый редактор в терминале
nano somefile.txt
//ctrl + o => сохранение 
//ctrl + x => выйти из nano

###История терминала
rm .zsh_history
history -p

###Отключение firewall
defaults write /Library/Preferences/com.apple.alf globalstate -int 0
launchctl unload /System/Library/LaunchDaemons/com.apple.alf.agent.plist

###Открыть настройки
1. command + space -> settings (set) 
    || Через значок яблока в левом верхнем углу 
    
###git
git clone https://github.com/DenVuy/ktits.git

###Открыть все порты 
lsof -i -P | grep -i "listen"
sudo pfctl -vnf /etc/pf.conf

###bash file 
chmod u+x myfile.sh
cp myfile.sh /usr/local/bin
alias myfile=./myfile.sh
source ~/.bash_profile
$ myfile

// #!/bin/sh
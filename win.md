#Windows
###Скачать проги 
wsl --install
sudo apt update && sudo apt upgrade

winget search
winget install

###Проверка сети
ping -r google.com

###Git
winget install --id Git.Git -e --source winget
git clone https://github.com/DenVuy/ktits.git
git clone https://github.com/PowerShell/PowerShell.git
git clone https://github.com/fleschutz/PowerShell.git

###Отключение firewall
Set-NetFirewallProfile -Enabled False
netsh advfirewall show all //посмотреть 

###История терминала
doskey /listsize=0
Alt+F7

###Создание скрытой папки 

###Подключение к серверу 

###Текстовый редактор в консоли 
notepad somefile.txt



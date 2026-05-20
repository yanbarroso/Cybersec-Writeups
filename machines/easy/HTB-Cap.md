# HTB — Cap

![Badge](https://img.shields.io/badge/Hack_The_Box-Cap-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Dificuldade](https://img.shields.io/badge/Dificuldade-Easy-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Cap |
| **Categoria** | Retired Machine |
| **OS** | Linux |
| **Dificuldade** | Easy |
| **Status** | ✅ Concluída |
| **Tags** | `idor`, `pcap`, `ftp`, `ssh`, `capabilities`, `linux` |

---

## 🗺️ Reconhecimento

O reconhecimento inicial começou com um scan de portas para identificar os serviços expostos pelo alvo.

```bash
nmap -sC -sV -oN nmap/initial TARGET_IP
```

O scan geralmente revela três portas principais abertas:

- `21/tcp` — FTP
- `22/tcp` — SSH
- `80/tcp` — HTTP

Com uma superfície relativamente pequena, o foco naturalmente se volta para a aplicação web na porta 80, já que ela aparenta expor funcionalidades administrativas.

---

## 🔍 Enumeração

Ao acessar a interface web, é possível encontrar um painel com funcionalidades relacionadas a captura e análise de tráfego de rede. Um dos endpoints direciona para URLs no formato:

```text
/data/1
/data/2
/data/3
```

Essa estrutura sugere um possível caso de **IDOR** (*Insecure Direct Object Reference*), já que o identificador numérico pode ser alterado manualmente para acessar capturas que não deveriam estar disponíveis ao usuário atual.

Ao trocar o ID por `0`, a aplicação normalmente permite baixar um arquivo `.pcap` pertencente a outra sessão:

```text
http://TARGET_IP/data/0
```

O arquivo baixado pode então ser analisado com Wireshark ou `tcpdump`.

---

## 💥 Exploração

Dentro do arquivo `.pcap`, é possível observar tráfego contendo autenticação em texto claro. A análise dos pacotes revela credenciais válidas utilizadas em uma sessão FTP.

Com as credenciais recuperadas, o acesso inicial pode ser testado via FTP:

```bash
ftp TARGET_IP
```

Depois de confirmar que as credenciais funcionam, o acesso mais útil passa a ser via SSH:

```bash
ssh nathan@TARGET_IP
```

Isso fornece um shell estável como o usuário `nathan`, permitindo enumeração local completa.

---

## 🚩 Flag do Usuário

Depois do acesso via SSH, a flag de usuário pode ser lida normalmente no diretório home do usuário comprometido.

```bash
whoami
ls -la /home/nathan
cat /home/nathan/user.txt
```

---

## ⬆️ Escalada de Privilégios

Com o shell inicial obtido, a próxima etapa é buscar vetores locais de privilege escalation. Uma enumeração manual ou com scripts como LinPEAS pode revelar que o binário Python possui uma capability incomum atribuída a ele.

Um comando útil para identificar capabilities é:

```bash
getcap -r / 2>/dev/null
```

A saída normalmente mostra algo semelhante a:

```text
/usr/bin/python3.8 = cap_setuid,cap_net_bind_service+eip
```

A capability `cap_setuid` permite alterar o UID efetivo do processo. Como consequência, é possível usar o Python para elevar o contexto para UID 0 e abrir um shell como root:

```bash
/usr/bin/python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

Após isso, o shell passa a ter privilégios de root.

---

## 🏆 Flag do Root

Com privilégios elevados, a flag final pode ser obtida diretamente:

```bash
whoami
cat /root/root.txt
```

---

## 📝 Lições Aprendidas

- Um **IDOR** simples pode expor arquivos sensíveis sem exigir exploração complexa.
- Capturas de rede mal protegidas podem vazar credenciais em texto claro.
- Reutilização de credenciais entre serviços, como FTP e SSH, amplia o impacto da falha inicial.
- **Linux capabilities** podem criar caminhos de escalada discretos e muito poderosos.
- Ferramentas como Wireshark, `getcap` e `linpeas` são extremamente úteis em máquinas desse perfil.

---

## 📚 Referências

- HTB — Cap
- GTFOBins
- Documentação sobre Linux capabilities
- Wireshark User Guide

---

*Writeup gerado para uso educacional e documentação pessoal.*

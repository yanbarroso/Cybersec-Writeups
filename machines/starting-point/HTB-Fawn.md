# HTB — Fawn

![Badge](https://img.shields.io/badge/Hack_The_Box-Fawn-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Tier](https://img.shields.io/badge/Starting_Point-Tier_0-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Fawn |
| **Categoria** | Starting Point |
| **OS** | Linux |
| **Dificuldade** | Very Easy |
| **Status** | ✅ Concluída |
| **Tags** | `ftp`, `anonymous-login`, `misconfiguration`, `linux` |

---

## 🗺️ Reconhecimento

O reconhecimento começou com um scan simples para identificar portas abertas e versões dos serviços.

```bash
ping -c 4 TARGET_IP
nmap -sC -sV TARGET_IP
```

O resultado indicou a porta **21/tcp** aberta, rodando **FTP**. Dependendo do scan utilizado, também é possível ver indícios de login anônimo permitido.

---

## 🔍 Enumeração

Sabendo que o serviço ativo era FTP, o próximo passo foi testar acesso com credenciais padrão e contas conhecidas. Uma tentativa com o usuário `anonymous` foi suficiente para entrar.

```bash
ftp anonymous@TARGET_IP
```

Depois do login, foi possível listar os arquivos disponíveis no diretório remoto:

```bash
ls
```

Entre os arquivos disponíveis estava `flag.txt`.

---

## 💥 Exploração

A exploração aqui não exige execução de código nem bypass complexo. O ponto central da box é a **má configuração do FTP com acesso anônimo habilitado**, expondo conteúdo sensível para qualquer usuário.

Após a autenticação, a flag foi baixada com:

```bash
get flag.txt
exit
cat flag.txt
```

Isso foi suficiente para concluir a máquina.

---

## 🚩 Captura da Flag

A flag estava diretamente acessível no diretório raiz compartilhado pelo servidor FTP, sem qualquer controle de acesso adicional.

```bash
get flag.txt
cat flag.txt
```

---

## 📝 Lições Aprendidas

- **Anonymous FTP** em produção é uma configuração altamente arriscada.
- Enumeração básica de serviços pode revelar falhas graves sem necessidade de exploits complexos.
- Testar usuários como `anonymous` faz parte da checklist padrão ao encontrar FTP exposto.
- Boxes simples como essa ajudam a criar disciplina operacional no processo de enumeração.

---

## 📚 Referências

- HTB Starting Point — Fawn
- Manual do `ftp`
- Documentação do `nmap`

---

*Writeup gerado para uso educacional e documentação pessoal.*

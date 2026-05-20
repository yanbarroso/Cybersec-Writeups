# HTB — Meow

![Badge](https://img.shields.io/badge/Hack_The_Box-Meow-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Tier](https://img.shields.io/badge/Starting_Point-Tier_0-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Meow |
| **Categoria** | Starting Point |
| **OS** | Linux |
| **Dificuldade** | Very Easy |
| **Status** | ✅ Concluída |
| **Tags** | `telnet`, `misconfiguration`, `blank-password`, `linux` |

---

## 🗺️ Reconhecimento

O primeiro passo foi validar a conectividade com a máquina e fazer um scan de portas para identificar serviços expostos.

```bash
ping -c 4 TARGET_IP
nmap -sC -sV TARGET_IP
```

O scan mostrou a porta **23/tcp** aberta, com o serviço **Telnet**, indicando um vetor clássico de acesso remoto inseguro quando exposto sem proteção adequada.

---

## 🔍 Enumeração

Com a presença do Telnet, a enumeração passou a focar em autenticação fraca. Em ambientes de laboratório como o Meow, o objetivo é introduzir o aluno ao risco de credenciais triviais ou autenticação sem senha.

A conexão foi feita com:

```bash
telnet TARGET_IP
```

Depois disso, foram testados logins simples. O acesso foi obtido com o usuário `root` e senha em branco.

---

## 💥 Exploração

A exploração da máquina consiste justamente em abusar da má configuração do serviço Telnet. Como o login `root` com senha vazia era aceito, o acesso inicial já ocorreu com privilégios máximos.

```text
Meow login: root
Password: [enter em branco]
```

Após o login, bastou confirmar o contexto:

```bash
whoami
hostname
pwd
```

O resultado esperado é um shell já autenticado como `root`.

---

## 🚩 Captura da Flag

Como o acesso já era privilegiado, a etapa seguinte foi localizar e ler a flag armazenada no sistema.

```bash
ls
cat flag.txt
```

Em algumas resoluções, a flag pode estar diretamente no diretório inicial do usuário autenticado ou em um local visível logo após o login.

---

## 📝 Lições Aprendidas

- Serviços legados como **Telnet** não devem ser expostos publicamente.
- Permitir autenticação com **senha em branco** é uma falha crítica.
- O laboratório introduz o fluxo básico de **reconhecimento → enumeração → acesso → captura de flag**.
- Mesmo boxes simples ajudam a fixar leitura de portas, identificação de protocolos e validação de hipóteses.

---

## 📚 Referências

- HTB Starting Point — Meow
- Documentação do `nmap`
- Manual do `telnet`

---

*Writeup gerado para uso educacional e documentação pessoal.*

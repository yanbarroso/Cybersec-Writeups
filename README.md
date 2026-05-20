# 🔐 HTB Writeups — Yan Barroso

Repositório pessoal com writeups das máquinas que pratiquei no [Hack The Box](https://www.hackthebox.com/). Cada máquina resolvida vira um arquivo em Markdown com o passo a passo do processo, desde o reconhecimento até a escalada de privilégios.

> **Objetivo:** documentar meus estudos em segurança ofensiva, consolidar aprendizado prático e manter uma base de consulta para revisões futuras.

---

## 📚 Sobre este repositório

Este projeto foi criado para organizar minha jornada de estudos em pentest e laboratório ofensivo. A ideia é manter uma documentação clara, reproduzível e progressiva, facilitando tanto a revisão dos conceitos quanto a visualização da minha evolução técnica.

Cada writeup pode incluir:

- Reconhecimento inicial
- Enumeração de serviços
- Exploração da vulnerabilidade
- Obtenção da flag de usuário
- Escalada de privilégios
- Obtenção da flag de root/administrator
- Lições aprendidas

---

## 📋 Índice de máquinas

| Máquina | OS | Dificuldade | Técnicas | Status |
|---|---|---|---|---|
| Em breve | — | — | — | 🔄 Preparando estrutura |

> Legenda: ✅ Concluída · 🔄 Em progresso · ⏳ Pendente

---

## 🗂️ Estrutura do projeto

```text
htb-writeups/
├── README.md
├── TEMPLATE.md
├── machines/
│   ├── easy/
│   ├── medium/
│   └── hard/
└── notes/
    └── cheatsheet.md
```

### Organização

- `README.md`: visão geral do repositório e índice das máquinas.
- `TEMPLATE.md`: modelo base para criar novos writeups.
- `machines/easy`, `machines/medium`, `machines/hard`: separação por dificuldade.
- `notes/cheatsheet.md`: comandos úteis e referência rápida para laboratório.

---

## 🧠 Tópicos estudados

As máquinas documentadas aqui podem envolver, entre outros temas:

- Reconhecimento com `nmap`, `whatweb`, `ffuf`, `gobuster`
- Enumeração de serviços como SMB, FTP, SSH, RDP, WinRM e NFS
- Vulnerabilidades web como SQL Injection, LFI, RFI, SSRF, XSS e IDOR
- Exploração de bancos de dados como MySQL, Redis, MongoDB e MSSQL
- Escalada de privilégios em Linux e Windows
- Abordagens de Active Directory, conforme os laboratórios evoluírem

---

## ⚙️ Fluxo de documentação

Para manter consistência entre os writeups, o processo de documentação segue este padrão:

1. Resolver a máquina no laboratório.
2. Registrar comandos, portas, credenciais, vetores e observações.
3. Copiar o `TEMPLATE.md` e adaptar para a máquina atual.
4. Salvar o arquivo na pasta correspondente à dificuldade.
5. Atualizar a tabela de índice neste README.

---

## ✅ Padrão de nomenclatura

Os arquivos de writeup seguem um padrão simples e previsível:

```text
HTB-NomeDaMaquina.md
```

Exemplos:

- `HTB-Archetype.md`
- `HTB-Appointment.md`
- `HTB-Three.md`

---

## 🛠️ Ambiente utilizado

| Ferramenta | Uso principal |
|---|---|
| Kali Linux / outra distro | Sistema para laboratório |
| Hack The Box VPN | Conexão com o ambiente HTB |
| Burp Suite | Interceptação e análise web |
| VS Code / Obsidian | Escrita e organização das notas |
| LinPEAS / WinPEAS | Enumeração local |
| Metasploit | Apoio em exploração, quando aplicável |

---

## 🎯 Objetivo de evolução

Este repositório não serve apenas para guardar soluções. Ele também funciona como trilha de estudo, histórico de prática e material de revisão para fixar técnicas, padrões de enumeração e caminhos de exploração.

Com o tempo, a tendência é que os writeups fiquem mais completos, mais objetivos e melhor estruturados.

---

## ⚠️ Aviso legal

Todo o conteúdo deste repositório se refere exclusivamente a ambientes controlados e autorizados, especialmente laboratórios do Hack The Box. O material tem finalidade estritamente educacional.

---

## 🔗 Perfis

- GitHub: [yanbarroso](https://github.com/yanbarroso)
- Autor: Yan Barroso
- HTB Profile: adicionar depois

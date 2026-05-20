# HTB Writeups — Yan Barroso

<p align="center">
  <a href="https://github.com/yanbarroso">
    <img src="https://img.shields.io/badge/GitHub-yanbarroso-181717?style=for-the-badge&logo=github" alt="GitHub">
  </a>
  <a href="https://app.hackthebox.com/users/3468054?profile-top-tab=machines&ownership-period=1M&profile-bottom-tab=prolabs">
    <img src="https://img.shields.io/badge/Hack%20The%20Box-YanBarroso%20%23BR-9FEF00?style=for-the-badge&logo=hackthebox&logoColor=black" alt="Hack The Box">
  </a>
  <img src="https://img.shields.io/badge/Writeups-Markdown-blue?style=for-the-badge&logo=markdown" alt="Markdown">
</p>

Repositório pessoal com writeups das máquinas que pratiquei no [Hack The Box](https://www.hackthebox.com/). Cada máquina resolvida vira um arquivo em Markdown com o processo de reconhecimento, enumeração, exploração e escalada de privilégios.

> Este repositório funciona como diário técnico, material de revisão e histórico da minha evolução em segurança ofensiva.

---

## Visão geral

A proposta é manter writeups claros, reproduzíveis e organizados. Em vez de guardar anotações soltas, cada máquina passa a ter uma documentação própria, com comandos, hipóteses, exploração, pós-exploração e aprendizados.

Os writeups podem incluir:

- Reconhecimento inicial
- Enumeração de serviços e tecnologias
- Exploração da vulnerabilidade
- Captura da flag de usuário
- Escalada de privilégios
- Captura da flag final
- Lições aprendidas e referências

---

## Índice de máquinas

| Máquina | SO | Dificuldade | Técnicas | Status |
|---|---|---|---|---|
| Em breve | — | — | — | 🔄 Preparando estrutura |

> Legenda: ✅ Concluída · 🔄 Em progresso · ⏳ Pendente

---

## Estrutura do repositório

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

### Organização das pastas

- `README.md` — visão geral do projeto e índice das máquinas.
- `TEMPLATE.md` — modelo base para padronizar novos writeups.
- `machines/easy` — máquinas de dificuldade easy.
- `machines/medium` — máquinas de dificuldade medium.
- `machines/hard` — máquinas de dificuldade hard.
- `notes/cheatsheet.md` — comandos e referências rápidas para laboratório.

---

## Fluxo de documentação

1. Resolver a máquina no laboratório.
2. Registrar portas, versões, vetores, credenciais e observações.
3. Duplicar o `TEMPLATE.md`.
4. Salvar o writeup na pasta correspondente à dificuldade.
5. Atualizar a tabela de índice neste README.

---

## Convenção de nomes

Todos os writeups seguem o padrão:

```text
HTB-NomeDaMaquina.md
```

Exemplos:

- `HTB-Archetype.md`
- `HTB-Appointment.md`
- `HTB-Three.md`

---

## Tópicos estudados

As máquinas deste repositório podem envolver assuntos como:

- Reconhecimento com `nmap`, `whatweb`, `ffuf`, `gobuster`
- Enumeração de serviços como SMB, FTP, SSH, RDP, WinRM e NFS
- Vulnerabilidades web como SQL Injection, LFI, RFI, SSRF, XSS e IDOR
- Bancos de dados como MySQL, Redis, MongoDB e MSSQL
- Escalada de privilégios em Linux e Windows
- Técnicas de Active Directory, conforme a trilha de estudos avançar

---

## Ambiente de estudo

| Ferramenta | Uso principal |
|---|---|
| Kali Linux / outra distro | Sistema para laboratório |
| Hack The Box VPN | Conexão com o ambiente HTB |
| Burp Suite | Interceptação e análise web |
| VS Code / Obsidian | Escrita e organização das notas |
| LinPEAS / WinPEAS | Enumeração local |
| Metasploit | Apoio em exploração, quando necessário |

---

## Objetivo do projeto

Este repositório não existe só para armazenar soluções. Ele serve para consolidar método, melhorar capacidade de enumeração, registrar padrões de ataque e criar um material de consulta rápido para estudos futuros.

Com o tempo, a tendência é que os writeups fiquem mais completos, mais limpos e mais consistentes.

---

## Perfis

- GitHub: [yanbarroso](https://github.com/yanbarroso)
- Hack The Box: [YanBarroso #BR](https://app.hackthebox.com/users/3468054?profile-top-tab=machines&ownership-period=1M&profile-bottom-tab=prolabs)
- Autor: Yan Barroso

---

## Aviso legal

Todo o conteúdo deste repositório se refere exclusivamente a ambientes controlados e autorizados, especialmente laboratórios do Hack The Box. O material tem finalidade estritamente educacional.

# HTB — Appointment

![Badge](https://img.shields.io/badge/Hack_The_Box-Appointment-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Tier](https://img.shields.io/badge/Starting_Point-Tier_1-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Appointment |
| **Categoria** | Starting Point |
| **OS** | Linux |
| **Dificuldade** | Very Easy |
| **Status** | ✅ Concluída |
| **Tags** | `sql injection`, `web`, `authentication bypass`, `linux` |

---

## 🗺️ Reconhecimento

O fluxo começou com o reconhecimento padrão da máquina usando Nmap para localizar serviços expostos.

```bash
nmap -sC -sV TARGET_IP
```

O scan mostrou a porta **80/tcp** aberta com um serviço **HTTP**, então a próxima etapa foi acessar o site no navegador.

---

## 🔍 Enumeração

Ao abrir a aplicação web, encontrei uma página de login. Como a superfície era pequena, a hipótese mais forte foi testar o formulário por **SQL Injection**.

O primeiro payload que funcionou foi no campo de usuário:

```text
admin' #
```

Com qualquer valor no campo de senha, a autenticação foi aceita.

Esse comportamento indica que a consulta SQL provavelmente seguia uma estrutura parecida com:

```sql
SELECT * FROM users WHERE username='$username' AND password='$password'
```

Ao inserir o payload acima, o restante da query é comentado, deixando a validação de senha fora da lógica.

---

## 💥 Exploração

A exploração foi direta: a aplicação aceitava a injeção no login e permitia acesso como administrador sem conhecer a senha real.

Exemplo de tentativa que funcionou:

- **Usuário:** `admin' #`
- **Senha:** qualquer valor

Outros payloads de SQLi também funcionaram, o que reforça que o formulário era vulnerável a manipulação da consulta no backend.

Depois do login bem-sucedido, a própria aplicação exibiu a flag ou confirmou o acesso administrativo necessário para capturá-la.

---

## 🚩 Captura da Flag

Após o bypass de autenticação, a flag pôde ser obtida diretamente da página administrativa ou da resposta pós-login.

```text
admin' #
```

Com isso, a máquina foi concluída sem necessidade de exploração adicional.

---

## 📝 Lições Aprendidas

- Formulários de login são alvos clássicos para testes de SQLi.
- Um payload simples com aspas e comentário pode ser suficiente para bypass de autenticação.
- Reconhecimento básico com Nmap continua sendo o melhor ponto de partida.
- Máquinas Starting Point são ótimas para fixar padrões de enumeração e injeção.

---

## 📚 Referências

- HTB Starting Point — Appointment
- Conceitos básicos de SQL Injection
- Documentação sobre comentários em SQL

---

*Writeup gerado para uso educacional e documentação pessoal.*

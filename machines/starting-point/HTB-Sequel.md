# HTB — Sequel





***

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Sequel |
| **Categoria** | Starting Point |
| **OS** | Linux |
| **Dificuldade** | Easy |
| **Status** | ✅ Concluída |
| **Tags** | `mariadb`, `mysql`, `database`, `weak authentication`, `linux` |

***

## 🗺️ Reconhecimento

O reconhecimento começou com um scan padrão usando scripts padrão do Nmap para identificar serviços e versões expostas.

```bash
nmap -sC -sV TARGET_IP
```

O resultado apontou a porta **3306/tcp** aberta, identificando um serviço **MySQL/MariaDB**. Como a superfície principal da máquina era o banco de dados, o próximo passo foi testar conexão direta usando o cliente `mysql`.

***

## 🔍 Enumeração

A conexão com o serviço foi feita tentando autenticação como `root`, sem senha. Nesse laboratório, a instância estava configurada de forma insegura e permitia acesso remoto sem exigir password.

```bash
mysql -h TARGET_IP -u root
```

Já no terminal do MariaDB, a enumeração começou com os bancos disponíveis:

```sql
SHOW DATABASES;
```

A saída mostrava as databases padrão do MySQL/MariaDB e uma database adicional chamada `htb`, que chamou a atenção por não fazer parte do conjunto padrão.

Depois disso, a investigação seguiu para essa database:

```sql
USE htb;
SHOW TABLES;
```

Dentro dela, apareciam duas tabelas. Para entender o conteúdo de ambas, a abordagem foi consultar tudo diretamente:

```sql
SELECT * FROM config;
SELECT * FROM users;
```

***

## 💥 Exploração

A exploração da máquina foi essencialmente uma enumeração de banco de dados exposto com autenticação fraca. Não foi necessário exploit complexo, apenas acesso legítimo indevido a uma instância MariaDB mal configurada.

Ao consultar a tabela `config`, foi possível encontrar uma linha contendo a flag em uma das colunas de configuração.

```sql
SELECT * FROM config;
```

Isso bastou para concluir a máquina.

***

## 🚩 Captura da Flag

A flag foi localizada dentro da tabela `config`, na database `htb`, após a sequência de enumeração abaixo:

```sql
SHOW DATABASES;
USE htb;
SHOW TABLES;
SELECT * FROM config;
```

A tabela `users` também podia ser inspecionada, mas a flag estava visível na `config`.

***

## 📝 Lições Aprendidas

- Bancos de dados expostos devem sempre ser testados durante a enumeração inicial.
- Acesso remoto ao **MariaDB/MySQL** com usuário `root` sem senha é uma falha crítica.
- Comandos simples como `SHOW DATABASES`, `USE`, `SHOW TABLES` e `SELECT` já resolvem muita coisa em laboratórios básicos.
- Nem toda exploração depende de RCE; às vezes o impacto está na **exposição direta de dados sensíveis**.

***

## 📚 Referências

- HTB Starting Point — Sequel
- Documentação do MySQL / MariaDB
- Cliente `mysql`

***

*Writeup gerado para uso educacional e documentação pessoal.*

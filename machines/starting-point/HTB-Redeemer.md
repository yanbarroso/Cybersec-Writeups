# HTB — Redeemer

![Badge](https://img.shields.io/badge/Hack_The_Box-Redeemer-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Tier](https://img.shields.io/badge/Starting_Point-Tier_0-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Linux-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Redeemer |
| **Categoria** | Starting Point |
| **OS** | Linux |
| **Dificuldade** | Very Easy |
| **Status** | ✅ Concluída |
| **Tags** | `redis`, `database`, `enumeration`, `linux` |

---

## 🗺️ Reconhecimento

O processo começou com a checagem de conectividade e um scan de portas completo, já que alguns serviços de banco de dados podem não aparecer em enumerações muito superficiais.

```bash
ping -c 4 TARGET_IP
nmap -p- -sV TARGET_IP
```

O scan apontou a porta **6379/tcp** aberta, identificando o serviço **Redis**.

---

## 🔍 Enumeração

Com o Redis identificado, o próximo passo foi interagir com o banco usando a CLI oficial.

```bash
redis-cli -h TARGET_IP
```

Após a conexão, comandos básicos de enumeração ajudaram a entender a estrutura do banco:

```bash
info
select 0
keys *
```

A saída revelou chaves disponíveis no banco padrão.

---

## 💥 Exploração

A exploração da máquina é, na prática, a enumeração inadequadamente protegida de uma instância Redis acessível pela rede. Sem autenticação efetiva, foi possível consultar o conteúdo das chaves diretamente.

Depois de listar as chaves, bastou recuperar seus valores:

```bash
get flag
```

Em alguns casos, o nome da chave pode variar, então a enumeração com `keys *` é a etapa decisiva.

---

## 🚩 Captura da Flag

Com acesso ao Redis sem credenciais, a flag foi obtida consultando diretamente a chave que a armazenava.

```bash
keys *
get <nome_da_chave>
```

---

## 📝 Lições Aprendidas

- **Redis exposto sem proteção** é uma falha séria de segurança.
- Serviços de banco de dados também devem fazer parte da enumeração inicial.
- O uso de CLIs nativas, como `redis-cli`, acelera muito a análise de serviços específicos.
- Mesmo sem RCE, uma exposição de dados já caracteriza um impacto relevante.

---

## 📚 Referências

- HTB Starting Point — Redeemer
- Documentação do `redis-cli`
- Documentação oficial do Redis

---

*Writeup gerado para uso educacional e documentação pessoal.*

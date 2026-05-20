# HTB — Dancing

![Badge](https://img.shields.io/badge/Hack_The_Box-Dancing-9FEF00?style=flat-square&logo=hackthebox&logoColor=white)
![Tier](https://img.shields.io/badge/Starting_Point-Tier_0-brightgreen?style=flat-square)
![OS](https://img.shields.io/badge/OS-Windows-blue?style=flat-square)

---

## 📋 Informações Gerais

| Campo | Valor |
|---|---|
| **Nome** | Dancing |
| **Categoria** | Starting Point |
| **OS** | Windows |
| **Dificuldade** | Very Easy |
| **Status** | ✅ Concluída |
| **Tags** | `smb`, `guest-access`, `share-enumeration`, `windows` |

---

## 🗺️ Reconhecimento

A enumeração começou com o scan de portas para descobrir quais serviços estavam disponíveis.

```bash
ping -c 4 TARGET_IP
nmap -sC -sV TARGET_IP
```

O scan revelou portas ligadas ao ecossistema SMB, especialmente **445/tcp**, indicando compartilhamentos de arquivos acessíveis via rede.

---

## 🔍 Enumeração

Com SMB identificado, a próxima etapa foi listar os compartilhamentos disponíveis no host remoto.

```bash
smbclient -L \\TARGET_IP\\ -N
```

A opção `-N` tenta conexão sem senha. A enumeração mostrou múltiplos shares, e um deles permitia acesso com credenciais nulas/guest.

Em seguida, foi feita a conexão ao compartilhamento acessível:

```bash
smbclient \\TARGET_IP\\WorkShares -N
```

Dentro do share, o conteúdo foi enumerado com comandos como:

```bash
ls
cd James
ls
```

---

## 💥 Exploração

A exploração consistiu em abusar de um compartilhamento SMB acessível sem autenticação forte. Dentro do share havia arquivos disponíveis para leitura, incluindo a flag.

O arquivo foi baixado usando:

```bash
get flag.txt
exit
cat flag.txt
```

Em algumas resoluções, também aparece um arquivo auxiliar como `worknotes.txt`, útil apenas como contexto do ambiente.

---

## 🚩 Captura da Flag

A flag foi encontrada dentro de um diretório acessível pelo compartilhamento SMB e baixada localmente para leitura.

```bash
get flag.txt
cat flag.txt
```

---

## 📝 Lições Aprendidas

- **SMB** é um protocolo crítico em ambientes Windows e deve sempre ser enumerado.
- Shares expostos com acesso guest ou sem senha representam risco real de vazamento de dados.
- `smbclient` é uma ferramenta essencial para reconhecimento e enumeração inicial.
- A máquina reforça a importância de testar acessos nulos sempre que SMB estiver exposto.

---

## 📚 Referências

- HTB Starting Point — Dancing
- Manual do `smbclient`
- Documentação sobre SMB

---

*Writeup gerado para uso educacional e documentação pessoal.*

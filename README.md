# auditoria-bruteforce-devsecops.
Projeto prático de segurança ofensiva e defensiva focado em ataques de Força Bruta (Medusa) e mitigação de riscos.
Este projeto demonstra a capacidade de configurar um ambiente de testes, simular ataques de Força Bruta em serviços comuns (FTP, Web) e, o mais importante, propor medidas de **DevSecOps** para mitigar esses riscos.

---

## ⚙️ 1. Configuração do Laboratório

A parte mais crucial da prática: a configuração do ambiente de testes.

* **Máquina Atacante:** Kali Linux (VM)
* **Alvo Vulnerável:** Metasploitable 2 (VM) e DVWA (Damn Vulnerable Web Application).
* **Topologia de Rede:** Configuração Host-Only/Interna no VirtualBox.
* **Endereços IP:** Kali: [Seu IP do Kali] | Metasploitable: [IP do Metasploitable]
* **Comprovação de Conexão:** [Inserir aqui o comando 'ping' ou 'nmap -sn' mostrando que as máquinas se comunicam.]

---

## 💥 2. Cenários de Exploração (O Ataque)

A ferramenta **Medusa** foi utilizada para automatizar a tentativa de senhas.

### 2.1. Ataque de Força Bruta no Serviço FTP

O serviço FTP (Porta 21) do Metasploitable é o alvo.

| Ação | Comando Medusa (Exemplo) | Evidência |
| :--- | :--- | :--- |
| **Varredura (Nmap)** | `nmap -sV [IP do Metasploitable]` | Porta 21: open (Serviço ProFTPD) |
| **Ataque Brute Force** | `medusa -u msfadmin -P /caminho/para/wordlist.txt -h [IP] -M ftp` | [Inserir a captura de tela do Medusa mostrando a senha encontrada.] |
| **Login Obtido** | Usuário: `msfadmin` / Senha: `msfadmin` (ou a senha que você descobriu) | [Comprovar o login bem-sucedido.] |

### 2.2. Ataque de Força Bruta em Formulário Web (DVWA)

*Detalhar aqui o comando ou a metodologia para quebrar a senha do formulário web.*

---

## ✅ 3. Mitigação e Defesa (O Valor Profissional)

O conhecimento obtido no ataque deve ser usado para a defesa. A vulnerabilidade principal encontrada é a falta de **Rate Limiting** e senhas fracas.

| Serviço | Vulnerabilidade Principal | Medidas de Mitigação (DevSecOps) |
| :--- | :--- | :--- |
| **FTP/Web** | Vulnerável a milhares de tentativas por minuto. | **Implementar Rate Limiting:** Bloquear o IP de origem após 5 tentativas de login em 60 segundos. |
| **Geral** | Senhas fracas (dicionário) funcionando. | **Forçar MFA** (Autenticação de Múltiplos Fatores) em todos os usuários. |
| **Geral** | | Adotar **Políticas de Senha Forte** (mínimo 12 caracteres, complexidade obrigatória). |

---

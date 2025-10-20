# auditoria-bruteforce-devsecops.
<img width="1600" height="896" alt="Capa trabalho da DIO" src="https://github.com/user-attachments/assets/98fcdbce-3ae6-48a6-b556-69445171ddc1" />

Projeto prático de segurança ofensiva e defensiva focado em ataques de Força Bruta (Medusa) e mitigação de riscos.
Este projeto demonstra a capacidade de configurar um ambiente de testes, simular ataques de Força Bruta em serviços comuns (FTP, Web) e, o mais importante, propor medidas de **DevSecOps** para mitigar esses riscos.
![Maquinas Ligadas](https://github.com/user-attachments/assets/324a99db-0289-48e3-9cb9-cb9a6ef78da0)

---

## ⚙️ 1. Configuração do Laboratório

A parte mais crucial da prática: a configuração do ambiente de testes.

* **Máquina Atacante:** Kali Linux (VM)
* **Alvo Vulnerável:** Metasploitable 2 (VM) e DVWA (Damn Vulnerable Web Application).
* **Topologia de Rede:** Configuração Host-Only/Interna no VirtualBox.
* **Endereços IP:** Kali: [Seu IP do Kali] | Metasploitable: [IP do Metasploitable]
* **Comprovação de Conexão:** [Inserir aqui o comando 'ping' ou 'nmap -sn' mostrando que as máquinas se comunicam.]
![metasploitables na rede Host-Only](https://github.com/user-attachments/assets/267167b7-38c8-42c1-832b-4dd0e79c2664)
![Kali Linux na mesma rede Host_Only](https://github.com/user-attachments/assets/1fc668d8-7b4c-4b48-95eb-65392cc6f8f8)

---

## 💥 2. Cenários de Exploração (O Ataque)

A ferramenta **Medusa** foi utilizada para automatizar a tentativa de senhas.

### 2.1. Ataque de Força Bruta no Serviço FTP

O serviço FTP (Porta 21) do Metasploitable é o alvo.

![IPs e Varredura (Scanning)](https://github.com/user-attachments/assets/40718837-b069-460c-9ca0-e22956886723)

| Ação | Comando Medusa (Exemplo) | Evidência |
| :--- | :--- | :--- |
| **Varredura (Nmap)** | `nmap -sV [IP do Metasploitable]` | Porta 21: open (Serviço ProFTPD) |
| **Ataque Brute Force** | `medusa -u msfadmin -P /caminho/para/wordlist.txt -h [IP] -M ftp` | ![erro001](https://github.com/user-attachments/assets/07aa40de-ba35-46eb-b6b6-50afc43ccb2c)
[] |
| **Login Obtido** | Usuário: `(admin)` / Senha:  (password) | [![senha quebrada com sucesso](https://github.com/user-attachments/assets/811b419a-33b6-4423-a795-9a0e548c4601)
] |

### 2.2. Ataque de Força Bruta em Formulário Web (DVWA)

![codigo medusa site ](https://github.com/user-attachments/assets/b7ffa41e-6c62-463a-9562-00ed8e32a730)

*Detalhar aqui o comando ou a metodologia para quebrar a senha do formulário web.*

---

## ✅ 3. Mitigação e Defesa (O Valor Profissional)

O conhecimento obtido no ataque deve ser usado para a defesa. A vulnerabilidade principal encontrada é a falta de **Rate Limiting** e senhas fracas.

| Serviço | Vulnerabilidade Principal | Medidas de Mitigação (DevSecOps) |
| :--- | :--- | :--- |
| **FTP/Web** | Vulnerável a milhares de tentativas por minuto. | **Implementar Rate Limiting:** Bloquear o IP de origem após 5 tentativas de login em 60 segundos. |
| **Geral** | Senhas fracas (dicionário) funcionando. | **Forçar MFA** (Autenticação de Múltiplos Fatores) em todos os usuários. |
| **Geral** | | Adotar **Políticas de Senha Forte** (mínimo 12 caracteres, complexidade obrigatória). | .

---

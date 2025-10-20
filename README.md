# auditoria-bruteforce-devsecops.
<img width="1600" height="896" alt="Capa trabalho da DIO" src="https://github.com/user-attachments/assets/98fcdbce-3ae6-48a6-b556-69445171ddc1" />
Projeto prático de segurança ofensiva e defensiva focado em ataques de Força Bruta (Medusa) e mitigação de riscos.
Este projeto demonstra a capacidade de configurar um ambiente de testes, simular ataques de Força Bruta em serviços comuns (FTP, Web) e, o mais importante, propor medidas de **DevSecOps** para mitigar esses riscos.
![Maquinas Ligadas](https://github.com/user-attachments/assets/324a99db-0289-48e3-9cb9-cb9a6ef78da0)

---

## ⚙️ 1. Configuração do Laboratório

A parte mais crucial da prática: a configuração do ambiente de testes.
![Maquinas Ligadas](https://github.com/user-attachments/assets/324a99db-0289-48e3-9cb9-cb9a6ef78da0)
* **Máquina Atacante:** Kali Linux (VM)
* **Alvo Vulnerável:** Metasploitable 2 (VM) e DVWA (Damn Vulnerable Web Application).
* **Topologia de Rede:** Configuração Host-Only/Interna no VirtualBox.
* **Endereços IP:** Kali: 192.168.56.101 | Metasploitable: IP 192.168.56.102
* **Comprovação de Conexão:** [Inserir aqui o comando 'ping' ou 'nmap -sn' mostrando que as máquinas se comunicam.]
![metasploitables na rede Host-Only](https://github.com/user-attachments/assets/267167b7-38c8-42c1-832b-4dd0e79c2664)
![Kali Linux na mesma rede Host_Only](https://github.com/user-attachments/assets/1fc668d8-7b4c-4b48-95eb-65392cc6f8f8)

---

## 💥 2. Cenários de Exploração (O Ataque)

A ferramenta **Medusa** foi utilizada para automatizar a tentativa de senhas.

### 2.1. Ataque de Força Bruta no Serviço FTP

O serviço FTP (Porta 21) do Metasploitable é o alvo.
![erro001](https://github.com/user-attachments/assets/07aa40de-ba35-46eb-b6b6-50afc43ccb2c)


| Ação | Comando Medusa (Exemplo) | Evidência |
| :--- | :--- | :--- |
| **Varredura (Nmap)** | `nmap -sV 192.168.56.102` | Porta 21: open (Serviço ProFTPD) |![IPs e Varredura (Scanning)](https://github.com/user-attachments/assets/40718837-b069-460c-9ca0-e22956886723)
| **Ataque Brute Force** | `medusa -u msfadmin -P /caminho/para/wordlist.txt -h [IP] -M ftp` | ![IPs e Varredura (Scanning)](https://github.com/user-attachments/assets/40718837-b069-460c-9ca0-e22956886723)
[] |
| **Login Obtido** | Usuário: `(admin)` / Senha:  (password) |
] |

### 2.2. Ataque de Força Bruta em Formulário Web (DVWA)



Este cenário simula um ataque contra um **formulário de login HTTP**, que é uma vulnerabilidade extremamente comum em aplicações web mal codificadas.

Diferente do FTP, o atacante aqui explora a ausência de proteções básicas no código-fonte da aplicação (como **CAPTCHA** ou **Rate Limiting**). Essa falha permite que o **Medusa** (ou outra ferramenta como Burp Suite ou Hydra) automatize o envio de milhares de requisições POST com senhas diferentes.

O objetivo é demonstrar que a falta de validação no código do site pode ser um vetor de ataque mais rápido e silencioso que o ataque direto ao serviço de rede.

---
![site DVWA](https://github.com/user-attachments/assets/d3f71b2c-1c4b-45c0-9464-62503f3ab606)


*Usando esse código na medusa poderemos encontrar .*
![Codigo](https://github.com/user-attachments/assets/83adbba0-668a-45b8-9a5a-c19f8bde04d3)
![senha quebrada com sucesso](https://github.com/user-attachments/assets/7f817177-3446-4fce-8c70-46808d5c9143)
Login e senha encontrado com sucesso.
---

## ✅ 3. Mitigação e Defesa (O Valor Profissional)

O conhecimento obtido no ataque deve ser usado para a defesa. A vulnerabilidade principal encontrada é a falta de **Rate Limiting** e senhas fracas.

| Serviço | Vulnerabilidade Principal | Medidas de Mitigação (DevSecOps) |
| :--- | :--- | :--- |
| **FTP/Web** | Vulnerável a milhares de tentativas por minuto. | **Implementar Rate Limiting:** Bloquear o IP de origem após 5 tentativas de login em 60 segundos. |
| **Geral** | Senhas fracas (dicionário) funcionando. | **Forçar MFA** (Autenticação de Múltiplos Fatores) em todos os usuários. |
| **Geral** | | Adotar **Políticas de Senha Forte** (mínimo 12 caracteres, complexidade obrigatória). | .

🛑 Conclusão: De Atacante a Defensor DevSecOps
O sucesso da simulação de ataque de Força Bruta contra os serviços FTP e Web (DVWA), utilizando Kali Linux e Medusa, reforçou uma lição crucial: a segurança de um sistema é tão forte quanto seu elo mais fraco. Neste caso, o elo mais fraco foi a falha na implementação de proteções básicas contra a automação de tentativas.

Este projeto, no entanto, não se encerra com a quebra de uma senha. O verdadeiro aprendizado reside na proposta de mitigação. Ao entender como o ataque ocorre, podemos implementar as defesas necessárias:

Validação de Infraestrutura: A prova de que o Rate Limiting e as políticas de bloqueio de IP são defesas prioritárias no firewall ou servidor Web.

Segurança da Aplicação: A necessidade de integrar recursos de MFA (Autenticação de Múltiplos Fatores) e CAPTCHA em formulários Web, provando que a segurança deve estar no código ("shift left").

Ao transformar a exploração em um tutorial didático, demonstrei domínio sobre o ciclo completo de segurança: Varredura → Ataque → Mitigação.

Este trabalho serve como prova de que minha transição para DevSecOps e Análise de Dados é baseada em uma compreensão prática de como os dados e a infraestrutura devem ser protegidos desde o início.
---

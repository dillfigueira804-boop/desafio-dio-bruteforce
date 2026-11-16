# 🛡️ Simulação de Ataque de Brute Force em Ambiente Controlado (Mobile / Termux)

Projeto prático desenvolvido para o Bootcamp de Cibersegurança da **DIO (Digital Innovation One)** em parceria com o **Santander**.

## 📌 Objetivo e Adaptação do Ambiente
O desafio original propõe o uso de Kali Linux e Medusa/Hydra para testar vulnerabilidades de autenticação. Seguindo a flexibilidade proposta pela DIO, o laboratório foi **100% adaptado e executado em um smartphone Android utilizando Termux e Python 3**, demonstrando a viabilidade de realizar estudos e auditorias de segurança em ambientes móveis.

## 🧠 Conceitos Estudados e Aplicados
* **Brute Force (Força Bruta):** Automação de tentativas combinando listas de usuários e senhas (*wordlists*) contra um formulário de login até encontrar a credencial válida.
* **Password Spraying:** Teste de poucas senhas comuns contra uma grande lista de usuários corporativos (coletados via OSINT), evitando o bloqueio de contas por tentativas excessivas.
* **Credential Stuffing:** Uso automatizado de pares de e-mail e senha vazados anteriormente em outros serviços para tentar acesso não autorizado.

## 🛠️ Estrutura do Laboratório (`Python` + `Termux`)
1. **Wordlists (`usuarios.txt` e `senhas.txt`):** Dicionários contendo possíveis nomes de usuários e senhas previsíveis para alimentar o teste.
2. **Servidor Alvo Local (`servidor_alvo.py`):** Servidor HTTP local rodando em `127.0.0.1:8080` que simula um sistema de login vulnerável (recebendo requisições `POST` e retornando status HTTP `401` para falha ou `200` para sucesso).
3. **Script de Ataque (`ataque_bruteforce.py`):** Automação que cruza todas as combinações das *wordlists* e envia requisições sequenciais até identificar o status `200 OK` (`dill:dio2026`).

## 📸 Evidências da Execução no Termux

### 1. Código do Servidor Alvo (`servidor_alvo.py`) e Execução
![Servidor Alvo e Execução](Captura%20de%20tela_20261116_101924_Termux.jpg)

### 2. Código do Script Atacante (`ataque_bruteforce.py`) e Resultado
![Script Atacante e Resultado](Captura%20de%20tela_20261115_201904_Termux.jpg)

## 🛡️ Medidas de Mitigação e Defesa (Blue Team)
Para proteger sistemas reais contra os ataques demonstrados neste laboratório, recomenda-se:
* **Autenticação Multifator (MFA / 2FA):** Exigir um segundo fator de validação (aplicativo autenticador, *Number Matching* ou chave física FIDO2) para impedir o acesso mesmo que a senha seja descoberta.
* **Rate Limiting e Bloqueio de Conta:** Limitar a quantidade de tentativas falhas por minuto ou bloquear temporariamente o IP/usuário após falhas consecutivas.
* **Armazenamento Seguro de Senhas (Hashing):** Substituir algoritmos antigos/reversíveis (como 3DES) por funções de *hashing* modernas com *Salt* e lentidão proposital, como **bcrypt**, **PBKDF2** ou **Argon2**.
* **Monitoramento de Vazamentos:** Utilizar serviços como o *Have I Been Pwned* para detectar e redefinir credenciais corporativas expostas em vazamentos externos.

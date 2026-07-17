# Hospital SaoMetasploitable - Ethical Security Audit & Network Analysis

Este repositório documenta um projeto académico-prático focado na avaliação de segurança, reconhecimento de rede, exploração ética e análise de tráfego num ambiente laboratorial isolado. O trabalho simula um cenário de segurança para uma instituição de saúde fictícia (*Hospital SaoMetasploitable*), demonstrando a aplicação prática de ferramentas padrão da indústria para identificar e compreender vulnerabilidades em sistemas informáticos.

---

## Objetivos do Projeto

O principal objetivo deste projeto é demonstrar competências práticas em cibersegurança, abrangendo tanto perspetivas ofensivas (compreensão de vetores de ataque) como defensivas (monitorização, mitigação e engenharia de privacidade):

*   *Laboratório Seguro:* Criação e configuração de um ambiente virtualizado isolado para testes de segurança.
*   *Reconhecimento e OSINT:* Identificação de subdomínios, emails expostos e mapeamento da superfície de ataque do hospital.
*   *Avaliação de Risco:* Simulação de testes de intrusão automatizados para validar a robustez dos sistemas de autenticação.
*   *Análise Forense de Logs:* Inspeção de históricos de acessos para rastrear incidentes e tentativas de intrusão passadas.
*   *Privacidade e Conformidade:* Implementação de técnicas de pseudo-anonimização em dados sensíveis de pacientes.

---

## Tecnologias e Ferramentas Utilizadas

*   *Recolha de Inteligência (OSINT):* TheHarvester
*   *Reconhecimento de Rede:* Nmap
*   *Avaliação de Segurança:* Hydra (Ataques baseados em dicionário)
*   *Forense Digital:* Análise de Logs do Linux (auth.log)
*   *Processamento e Privacidade:* Bash (sed / RegEx)
*   *Conceitos Abordados:* Postura de Segurança, Vetores de Ataque (FTP/SSH), Logs de Autenticação e Proteção de Dados

---

##  Metodologia e Fases do Projeto

### 1. Reconhecimento Passivo (OSINT)
Utilização do *TheHarvester* para mapear a pegada digital externa do hospital, procurando possíveis subdomínios expostos ou fugas de emails institucionais em fontes públicas.

### 2. Auditoria e Mapeamento de Rede
Execução do *Nmap* para realizar varrimentos de portas e identificação de versões de serviços ativos nos servidores do hospital. A análise focou-se nos serviços expostos nas portas do FTP, SSH e Telnet.

### 3. Teste de Intrusão Baseado em Dicionário
Simulação de um ataque de força bruta direcionado ao serviço FTP utilizando a ferramenta *Hydra, cruzando uma *wordlist de credenciais comuns para testar a robustez das políticas de autenticação da instituição.

### 4. Análise Forense de Logs (Live Forensics)
Inspeção minuciosa do ficheiro auth.log (diretório /var/log) recolhido do servidor alvo. A análise serviu para reconstruir a cronologia de acessos e monitorizar tentativas de login falhadas de origem externa.

### 5. Engenharia de Privacidade e Anonimização de Dados
Manipulação de ficheiros sensíveis em texto limpo (lista_utentes.txt). Implementação de uma pipeline via linha de comandos com o utilitário sed para mascarar os identificadores diretos dos pacientes, garantindo a conformidade na proteção de dados médicos.

---

##  Principais Descobertas e Resultados

> *Nota de Impacto:* Este projeto validou a importância crítica da abordagem Defense-in-Depth na infraestrutura digital do Hospital SaoMetasploitable.

*   *Vulnerabilidade de Autenticação (Hydra):* Quebra imediata do serviço FTP devido à utilização de credenciais padrão e fracas (ftp/ftp), demonstrando a falta de controlos rígidos de acesso.
*   *Evidências de Ataques Ativos (Logs):* A análise forense do auth.log documentou uma vulnerabilidade operacional ativa, provando que o servidor já estava a ser alvo de tentativas externas de brute-force antes da auditoria.
*   *Falta de Conformidade e Remediação:* Identificação de dados médicos expostos em texto claro. O impacto foi mitigado com sucesso através da pipeline de anonimização com sed, mascarando as identidades de forma irreversível.
*   *Mitigação Recomendada:* Atualização imediata de serviços desatualizados, desativação de protocolos inseguros (Telnet), aplicação de políticas de passwords complexas com autenticação multi-fator (MFA) e centralização de logs para deteção precoce.

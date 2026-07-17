# Hospital SaoMetasploitable - Ethical Security Audit & Network Analysis

Este repositório documenta um projeto académico-prático focado na avaliação de segurança, reconhecimento de rede, exploração ética e análise de tráfego num ambiente laboratorial isolado. O trabalho simula um cenário de segurança para uma instituição de saúde fictícia (*Hospital SaoMetasploitable*), demonstrando a aplicação prática de ferramentas padrão da indústria.

---

##  Estrutura do Repositório

Para garantir as boas práticas de organização de um projeto de auditoria, os ficheiros estão estruturados da seguinte forma:

*   scripts/anonimizar.sh -> Script Bash automatizado para proteção de dados médicos.
*   docs/nmap_scan.txt -> Log bruto com o varrimento completo de portas e serviços.
*   README.md -> Este guia de documentação principal.

---

##  Objetivos do Projeto

O principal objetivo deste projeto é demonstrar competências práticas em cibersegurança, abrangendo tanto perspetivas ofensivas (compreensão de vetores de ataque) como defensivas (monitorização, mitigação e engenharia de privacidade):

*   *Laboratório Seguro:* Criação e configuração de um ambiente virtualizado isolado para testes de segurança.
*   *Reconhecimento e OSINT:* Identificação de subdomínios, emails expostos e mapeamento da superfície de ataque do hospital.
*   *Avaliação de Risco:* Simulação de testes de intrusão automatizados para validar a robustez dos sistemas de autenticação.
*   *Análise Forense de Logs:* Inspeção de históricos de acessos para rastrear incidentes e tentativas de intrusão passadas.
*   *Privacidade e Conformidade:* Implementação de técnicas de pseudo-anonimização em dados sensíveis de pacientes.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

*   *Recolha de Inteligência (OSINT):* TheHarvester
*   *Reconhecimento de Rede:* Nmap
*   *Avaliação de Segurança:* Hydra (Ataques baseados em dicionário)
*   *Forense Digital:* Análise de Logs do Linux (auth.log)
*   *Processamento e Privacidade:* Bash (sed / RegEx)

---

## 📊 Metodologia e Fases do Projeto

### 1. Reconhecimento Passivo (OSINT)
Utilização do *TheHarvester* para mapear a pegada digital externa do hospital, procurando possíveis subdomínios expostos ou fugas de emails institucionais em fontes públicas.

### 2. Auditoria e Mapeamento de Rede
Execução do *Nmap* para realizar varrimentos de portas e identificação de versões de serviços ativos nos servidores do hospital. A análise focou-se nos serviços expostos nas portas do FTP, SSH e Telnet.
> 📁 O relatório técnico gerado pelo varrimento pode ser consultado diretamente em [docs/nmap_scan.txt](docs/nmap_scan.txt).

### 3. Teste de Intrusão Baseado em Dicionário
Simulação de um ataque de força bruta direcionado ao serviço FTP utilizando a ferramenta *Hydra, cruzando uma *wordlist de credenciais comuns para testar a robustez das políticas de autenticação da instituição.

### 4. Análise Forense de Logs (Live Forensics)
Inspeção minuciosa do ficheiro auth.log (diretório /var/log) recolhido do servidor alvo. A análise serviu para reconstruir a cronologia de acessos e monitorizar tentativas de login falhadas de origem externa.

### 5. Engenharia de Privacidade e Anonimização de Dados
Manipulação de ficheiros sensíveis em texto limpo (lista_utentes.txt). Foi desenvolvida uma pipeline automatizada para mascarar os identificadores diretos dos pacientes, garantindo a conformidade na proteção de dados médicos.
> 📁 O código-fonte do script de automação está disponível em [scripts/anonimizar.sh](scripts/anonimizar.sh).

---

## Principais Descobertas e Resultados

| Severidade | Vulnerabilidade Detetada | Impacto |
| :--- | :--- | :--- |
| *Crítica* | Porta 21 activa com vsftpd 2.3.4 | Versão obsoleta com histórico de backdoor. |
| *Alta* | Credenciais FTP padrão (ftp/ftp) | Permitiu a quebra imediata de autenticação via Hydra. |
| *Média* | lista_utentes.txt em texto limpo | Exposição direta de dados médicos sensíveis. |
| *Baixa* | Versões de serviços visíveis | Facilita o reconhecimento por parte de atacantes. |

*   *Resultado OSINT:* Limpo. Não foram encontrados dados do hospital expostos publicamente.
*   *Resultado Forense:* Foram encontradas evidências de ataques de força bruta ativos no auth.log anteriores a esta auditoria.
*   *Remediação de Dados:* O impacto da exposição da lista de utentes foi mitigado com sucesso através da pipeline de anonimização irreversível.

---

## Plano de Ação Recomendado

1.  *Remediação de Credenciais:* Forçar políticas de passwords complexas e desativar contas padrão.
2.  *Atualização de Serviços:* Atualizar o serviço FTP e desativar protocolos inseguros como Telnet.
3.  *Monitorização:* Implementar alertas automatizados para falhas repetidas de login no auth.log.

# Hospital SaoMetasploitable - Ethical Security Audit

Este repositório documenta uma *auditoria de segurança ética e análise forense* completa realizada na infraestrutura digital do cenário fictício Hospital SaoMetasploitable. O projeto simula a atuação de uma equipa de consultoria de segurança contratada para avaliar a postura defensiva da instituição, mitigar fugas de informação e garantir a conformidade na proteção de dados de saúde.

---

## Objetivos do Projeto

O principal objetivo deste projeto é demonstrar competências práticas em Red Teaming (avaliação ofensiva) e Blue Teaming (análise e remediação defensiva) num ambiente de saúde crítico:

- *Avaliação de Exposição Pública (OSINT):* Verificar se dados confidenciais do hospital estão acessíveis na internet pública.
- *Análise Forense Digital (Live Forensics):* Identificar e analisar tentativas de acessos não autorizados através de logs do sistema.
- *Mapeamento de Superfície de Ataque:* Descobrir e catalogar todos os serviços e portas ativos nos servidores do hospital.
- *Testes de Robustez de Autenticação:* Validar a segurança e a resiliência do protocolo FTP contra ataques de força bruta.
- *Proteção e Privacidade de Dados:* Implementar técnicas de pseudo-anonimização em dados sensíveis de pacientes (em conformidade com as regras de proteção de dados de saúde).

---

## Tecnologias e Ferramentas Utilizadas

| Ferramenta | Categoria | Propósito Técnico |
| :--- | :--- | :--- |
| *TheHarvester* | OSINT | Recolha de inteligência pública e subdomínios |
| *Nmap* | Auditoria de Rede | Descoberta de ativos, portas abertas e versões de serviços |
| *Hydra* | Penetration Testing | Testes automatizados de robustez de credenciais |
| *Linux Logs (auth.log)* | Forense Digital | Análise de incidentes e histórico de acessos |
| *Bash (sed / RegEx)* | Processamento de Dados | Engenharia de privacidade e anonimização de dados |

---

## Metodologia e Fases do Projeto

### 1. Reconhecimento Passivo (OSINT)
Utilização do *TheHarvester* para mapear a pegada digital do hospital. O objetivo foi identificar possíveis fugas de emails de funcionários ou subdomínios expostos.
* *Ação:* Varrimento direcionado a fontes públicas e motores de pesquisa à procura de vetores de engenharia social.

### 2. Análise Forense de Logs (Live Forensics)
Extração e análise do ficheiro auth.log (diretório /var/log) da máquina alvo através de uma sessão FTP controlada.
* *Ação:* Inspeção minuciosa de eventos para reconstruir a cronologia de acessos e monitorizar atividade suspeita no servidor.

### 3. Auditoria de Segurança de Rede
Execução do *Nmap* para mapeamento topológico e deteção de serviços ativos no servidor alvo.
```bash
# Varrimento detalhado de serviços, scripts padrão e deteção de OS
nmap -sV -sC -O 192.168.100.10

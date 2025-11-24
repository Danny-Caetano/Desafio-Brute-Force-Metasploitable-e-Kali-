📘 Projeto Prático: Exploração com Kali Linux, Medusa e Metasploitable 2

🧭 Visão Geral

Este documento descreve o projeto prático realizado com Kali Linux, Metasploitable 2 e DVWA para simular cenários de exploração de vulnerabilidades em ambiente totalmente controlado.
O objetivo foi:

Entender ataques de força bruta nos serviços FTP, Web/DVWA e SMB

Criar wordlists simples para estudos

Usar o Medusa como ferramenta de auditoria

Validar acessos simulados e interpretar respostas dos serviços

Documentar o processo de forma clara, estruturada e responsável

Propor medidas concretas de mitigação

⚠️ Todos os testes foram realizados exclusivamente em laboratório isolado, sem qualquer acesso a sistemas reais.
Este conteúdo tem caráter educacional e demonstração de aprendizado.

🛠️ Ambiente Utilizado

Ferramentas e Sistemas

Kali Linux

Oracle VirtualBox

Metasploitable 2 (ambiente vulnerável propositalmente)

DVWA – Damn Vulnerable Web App (rodando dentro do Metasploitable)

Medusa (ferramenta de auditoria de autenticação)

Configuração das VMs

As máquinas foram configuradas com:

Máquina	Tipo	Função
Kali Linux	VM	Ferramentas de auditoria
Metasploitable 2	VM	Sistema vulnerável
DVWA	Serviço	Exploração web controlada

Modo de rede utilizado

Host-Only (Rede Interna)

Permitiu que apenas as duas VMs se comunicassem entre si

Garantiu isolamento total da rede real

📄  Preparação do Ambiente no Kali
Acesso como root para os testes de laboratório

Usuário: admcybersec

Senha: cyber

(esse foi um ambiente criado apenas para o curso, sem risco real)

 Criação das wordlists simples

Foram criados dois arquivos de wordlist para testes:

pass.txt
users.txt

Esses arquivos foram gerados diretamente no terminal do Kali, com conteúdos simples e fictícios, exemplo:

users.txt
-------------
admin
msfadmin (Adm Metasploitable)
user
root

pass.txt
-------------
123456
admin
password
msfadmin (Password Metasploitable)

🎯 Testes Realizados

A seguir, está a documentação estruturada dos testes feitos utilizando o Medusa e outros recursos educacionais do Kali Linux.

Teste 1 – Força Bruta no Serviço FTP (Metasploitable 2)
Objetivo

Simular tentativas de autenticação no serviço FTP do Metasploitable usando wordlist simples.

Procedimento

Foi utilizada a wordlist users.txt + pass.txt

O alvo foi o IP da VM Metasploitable na rede host-only

O Medusa analisou combinações possíveis e respondeu com falhas ou sucesso

Resultados

O serviço FTP respondeu rapidamente às tentativas

Credenciais fracas foram facilmente identificadas

Validou-se acesso a partir de uma combinação válida da wordlist

Riscos observados

Serviços FTP sem limitação de tentativas são vulneráveis

Senhas fracas são facilmente quebradas

Mitigações

Habilitar SFTP/FTPS

Criar política de bloqueio de tentativas

Desabilitar usuários desnecessários

Impor senhas complexas

Teste 2 – Automação em Formulário Web (DVWA – Low Security)
Objetivo

Entender como um formulário web vulnerável reage a tentativas automatizadas.

Procedimento

DVWA configurado em segurança “Low”

Wordlist simples utilizada

Teste de repetição de tentativas para observar comportamento

Resultados

DVWA aceitou tentativas sem rate limiting

Identificou-se resposta “Login Failed” repetida nas tentativas incorretas

Com credenciais simples, a autenticação foi validada

Mitigações

Implementação de CAPTCHA

2FA/MFA para áreas sensíveis

Rate limiting e bloqueio de IP

Uso de hashing e controle de sessão robusto

Teste 3 – Password Spraying e Enumeração de Usuários via SMB
Objetivo

Entender como serviços SMB respondem a tentativas de autenticação com a técnica de password spraying, usando uma senha para vários usuários, evitando bloqueio de contas.

Procedimento

Wordlist users.txt para enumeração

Senha única “msfadmin” para teste

Observação do comportamento do serviço SMB do Metasploitable

Resultados

O SMB permitiu enumeração de usuários válidos

A técnica de “password spraying” demonstrou como contas fracas podem ser comprometidas

Validou-se acesso com usuário/senha fracos presentes no ambiente vulnerável

🧪 Mitigações

Ativar política de bloqueio progressivo

Senhas únicas e fortes para cada usuário

Desabilitar SMBv1

Auditoria de contas inativas

🧪 Validação de Acesso

Cada teste confirmou:

Mensagens claras de falha/sucesso

Comportamentos previsíveis de serviços vulneráveis

Capacidade de identificar credenciais fracas

Logs de autenticação registrando tentativas

A documentação das evidências (prints de tela) pode ser adicionada na pasta:
evidencias/

🛡️ Recomendações Gerais de Mitigação

🔒 Fortalecer credenciais

Senhas longas e únicas

MFA sempre que possível

🚫 Limitar tentativas

Bloqueio temporário após falhas seguidas

Contagem de tentativas por IP

📜 Auditoria e monitoramento

Logs ativados e monitorados

Alertas automáticos para tentativas massivas

🔧 Hardening de serviços

Desabilitar serviços não utilizados

Atualizar protocolos (ex.: SMBv1 → SMBv3)

Usar FTP seguro (SFTP/FTPS)

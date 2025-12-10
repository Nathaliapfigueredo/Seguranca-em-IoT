Análise estática do código ESP32 Web Server 

1. Introdução
Este relatório apresenta uma análise estática do código de um servidor web implementado em um ESP32, baseado no exemplo de Rui Santos (Random Nerd Tutorials). O programa cria um servidor HTTP na porta 80 que permite controlar remotamente os GPIOs 26 e 27 por meio de requisições GET acessadas via navegador, sem mecanismos adicionais de segurança. A análise foca na identificação de vulnerabilidades inerentes ao código, considerando práticas de segurança, manipulação de entrada, exposição da rede e riscos de disponibilidade, integridade e confidencialidade. A partir dessas observações, são discutidos ataques plausíveis decorrentes dessas falhas e propostas recomendações técnicas para mitigar esses riscos.
2. Vulnerabilidades
2.1 Autenticação
Dessa forma, qualquer atacante na mesma rede (ou com rota até o dispositivo) pode ligar/desligar GPIOs enviando requisições HTTP GET simples.

2.1.1 Ataque 

Passo-a-passo do ataque:
O atacante obtém acesso à mesma rede do ESP32. Basta estar conectado ao mesmo Wi-Fi ou ter qualquer rota de rede que alcance o dispositivo.
Descobrir o IP do ESP32. Pode usar ferramentas de varredura como nmap, fing, ARP/MDNS, ou simplesmente verificar o log do roteador.
Enviar requisição HTTP GET para o endpoint de interesse.
O atacante aciona GPIOs por comandos simples
2.1.2 Probabilidade de ocorrência
Alta se o dispositivo estiver em uma rede sem segmentação (Wi-Fi doméstico) ou se o roteador permitir acesso (NAT) e não houver firewall.
Média se a rede corporativa for mais restrita, mas possível via vulnerabilidades internas.
O servidor aceita requisições sem autenticação e usa HTTP simples; tudo o que o atacante precisa é reachability.
2.1.3 Impacto estimado
Físico/operacional: alto — GPIOs podem controlar relés, motores, bombas, portas, sistemas de aquecimento, etc. Comutação indevida pode causar danos físicos, segurança física comprometida ou perda de inventário.


Disponibilidade: médio — controle indevido pode interromper serviços.


Privacidade: baixo/médio dependendo do que estiver conectado.


2.1.4 Risco resultante
Alto — combinação de alta probabilidade (rede simples) e alto impacto físico/operacional.

2.2 XXXX

3. Conclusão da análise

Título do Ataque
Probabilidade
Impacto
Risco
1. Controle Remoto Não Autorizado dos GPIOs
Alta
Alto
Alto
2. DoS por Esgotamento de Memória/Conexões
Média
Alto
Médio-Alto
3. Sniffing de Tráfego para Captura de Comandos
Média
Médio
Médio
4. Manipulação via CSRF (Ação Remota Indireta)
Baixa
Médio
Baixo-Médio




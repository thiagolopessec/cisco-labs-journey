# Análise de Encapsulamento de Pacotes: ICMP e Switching (Layer 2 vs Layer 3)

## Objetivo
Investigar como Switches e Roteadores tratam pacotes de forma diferente, desmistificando a relação entre Endereçamento IP (Lógico) e Endereçamento MAC (Físico) em uma LAN.

## Ferramentas Utilizadas
- Cisco Packet Tracer (Simulation Mode)
- Filtros de Protocolo (ICMP)
- Análise de PDU (Protocol Data Unit)

## O Cenário
Uma topologia simples com dois hosts (192.168.1.1 e 192.168.1.2) conectados a um Switch 2960. O objetivo foi interceptar um pacote ICMP (Ping) no momento exato em que ele passa pelo Switch.

## Análise Técnica
Ao inspecionar o cabeçalho do pacote no Packet Tracer, confirmei o processo de encapsulamento:

1. **Camada 3 (Network):** O pacote contém os IPs de Origem e Destino (`Src IP: 192.168.1.2`). Isso define a rota "fim-a-fim".
2. **Camada 2 (Data Link):** O pacote contém os MACs de Origem e Destino.
3. **A Descoberta:** O Switch ignora completamente a informação da Camada 3. Ele encaminha o quadro baseando-se **exclusivamente no MAC Address de destino** (`0001.64CA.A127`) consultando sua Tabela MAC (CAM Table).

## Conclusão de Segurança
Entender que a LAN opera em "confiança" baseada em MAC expõe a importância de proteger a Camada 2. Ataques como *ARP Spoofing* ou *MAC Flooding* exploram exatamente essa mecânica de funcionamento dos switches, que confiam cegamente nos endereços físicos apresentados.

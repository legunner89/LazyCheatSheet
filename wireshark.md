```
Usage	Filter Syntax
Wireshark Filter by IP	ip.add == 10.10.50.1
Filter by Destination IP	ip.dest == 10.10.50.1
Filter by Source IP	ip.src == 10.10.50.1
Filter by IP range	ip.addr >= 10.10.50.1 and ip.addr <=10.10.50.100
Filter by Multiple Ips	ip.addr == 10.10.50.1 and ip.addr == 10.10.50.100
Filter out IP adress	! (ip.addr == 10.10.50.1)
Filter subnet	ip.addr == 10.10.50.1/24
Filter by port	tcp.port == 25
Filter by destination port	tcp.dstport == 23
Filter by ip adress and port	ip.addr == 10.10.50.1 and Tcp.port == 25
Filter by URL	http.host == "host name"
Filter by time stamp	frame.time >= "June 02, 2019 18:04:00"
Filter SYN flag	Tcp.flags.syn == 1 and tcp.flags.ack ==0
Wireshark Beacon Filter	wlan.fc.type_subtype = 0x08
Wireshark broadcast filter	eth.dst == ff:ff:ff:ff:ff:ff
Wireshark multicast filter	(eth.dst[0] & 1)
Host name filter	ip.host = hostname
MAC address filter	eth.addr == 00:70:f4:23:18:c4
RST flag filter	tcp.flag.reset == 1


```

```
IP Address: ip.addr == 192.168.1.1

    Filtra pacotes baseados em um endereço IP específico.

Port: tcp.port == 80

    Filtra pacotes com base em uma porta TCP específica (neste caso, a porta 80).

Protocol: http

    Filtra pacotes baseados no protocolo, como HTTP.

Host: http.host == "example.com"

    Filtra pacotes HTTP para um host específico.

Source or Destination: ip.src == 192.168.1.1 ou ip.dst == 192.168.1.1

    Filtra pacotes com base no endereço IP de origem ou destino.

Subnet: ip.addr == 192.168.1.0/24

    Filtra pacotes para um intervalo de sub-rede específico.

Expression: tcp.flags.syn == 1

    Filtra pacotes com flags TCP específicas (SYN, ACK, etc.).

HTTP GET Requests: http.request.method == "GET"

    Filtra pacotes HTTP para solicitações GET.

HTTP Status Code: http.response.code == 200

    Filtra pacotes HTTP com um código de status específico.

UDP: udp

    Filtra pacotes baseados no protocolo UDP.

ICMP: icmp

    Filtra pacotes baseados no protocolo ICMP.

DNS Requests: dns.qry.type == 1

    Filtra pacotes DNS para solicitações de consulta.

Length: frame.len > 1000

    Filtra pacotes com base no tamanho do quadro.

Follow TCP Stream: tcp.stream eq 5

    Exibe o fluxo TCP para uma conexão específica.

Time Range: frame.time_relative > 5 && frame.time_relative < 10

    Filtra pacotes com base no intervalo de tempo relativo.

Packet Number: frame.number == 100

    Filtra pacotes com base no número de pacote.

IPv6: ipv6

    Filtra pacotes IPv6.

ARP: arp

    Filtra pacotes ARP.

FTP: ftp

    Filtra pacotes FTP.

TLS: tls

    Filtra pacotes TLS.

```

Para filtrar pacotes que contenham a palavra "gobuster" nas requisições no Wireshark, você pode usar o filtro:


frame contains "gobuster"

Esse filtro busca por qualquer pacote que contenha a string "gobuster" em seu conteúdo, independentemente do protocolo.

Se você quiser ser mais específico e focar em pacotes HTTP, por exemplo, pode combinar com o filtro HTTP:


http contains "gobuster"

Isso vai garantir que o Wireshark mostre apenas pacotes HTTP que contenham a palavra "gobuster".
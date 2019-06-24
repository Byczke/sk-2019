**Pierwszym krokiem jest utworzenie 3 maszyn w środowisku VirtualBox
Wykorzystałem do tego maszynę załączoną na moodlu i opcję clone aby uzyskać 2 pozostałe maszyny**

![](part2.JPG)

**Następnie tworzymy dwie sieci typu NAT**

![](part1.JPG)

**Wybieramy maski podsieci i adresy IP
Korzystając z tablic dostępnych w internecie możemy sprawdzić jaka maska będzie nam potrzebna**

![](maska_podsieci.png)

 Czyli w naszym przypadku będzie to 
 172.22.128.0/19 dla 8190 hostów, aby była możliwość adresacji 5000 urządzań
 172.22.128.0/23 dla 510  hostów, aby była możliwość adresacji 500  urządzeń
 
 
 **PC1** podłączamy do:
 
 karta nr1 - NAT
 
 karta nr2 - LAN1
 
 karta nr3 - LAN2
 
 **PC2** podłączamy do:
 
 karta nr1 -LAN1
 
 **PC3** podłączamy do:
 
 karta nr1 - LAN2
 
 **Konfiguracja sieci:**
 
  **PC1**
  
  ![](part3.JPG)
  
  **PC2**
  
  ![](part4.JPG)
  
  **PC3**
  
  ![](part5.JPG)

**Routing PC2 oraz PC3**

Dodajemy te linijki w /etc/network/interfaces

**PC2**

![](part6.JPG)

**PC3**

![](part7.JPG)

Następnie sprawdzamy poprawność korzystając z **ip route show**

**Konfiguracja forwardingu na PC1**

w  pliku znajdującym się w ścieżce /etc/sysctl.d w pliku 99-sysctl.conf odkomentować następującą linijkę

![](part8lub9.JPG)

**MASQUERADE - PC1**

Ścieżka /etc/ w pliku iptables.up.rules dopisać

![](part9.JPG)

Trzeba także ustawić automatyczne wczytywanie tych reguł przy starcie maszyny
Robimy to poprzez edycję pliku interfaces w ścieżce /etc/network/ dopisując

![](part10.JPG)

**DNS**

Ostatnim krokiem jest dodanie w pliku resolv.conf w ścieżce /etc/ adresów DNS, w tym przypadku "1.1.1.1"

![](part11.JPG)

Zarówno dla PC2 jak i PC3

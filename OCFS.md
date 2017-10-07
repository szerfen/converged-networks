#  OCFS i OCFS2

OCFS czyli Oracle Cluster File System jest to specjalnie zaprojektowany system plików przez Oracle Corporation i wydana na licencji GNU General Public Liceense. Jest to wsóldzielony system plików do zarządzania bazami danych w klastrach komputerowych. Pozwala on administratorom korzystać z systemu plików dla oraclowych danobazowych plików (pliki dnaych, pliki kontrolne i dzienniki) oraz plików konfiguracyjnych. Każdy węzeł w klastrze ma dostęp do wszystkich urządzeń blokowych (dysków twardych). Dostęp jest zapewniany poprzez szbyką sieć lokalną SAN (Storage Area network).
OCFS w wersji drugiej wspiera m.in. semantykę POSIX czy listy dostępu ACL. 
OCFS2 został włączony do jądra linuxa w wersji 2.6.16 jako eksperymentalny, a w wersji 2.6.19 jako wersja normalna.

# Zasada działania

OCFS jest wydajnieszy od jedno-węzłowego systemu plików takiego jak chocby ext3. Ma on z nim jednak cechę wspólną, w swoim rdzeniu. Mimo wielu różnic między systemami implementacja OCFS jest bardzo podobna do systemu plików ext3. OCFS musi posiadać inforamcje o klastrze na którym operuje co stwarza wymóg pliku konfiguracyjnego *(/etc/ocfs2/cluster.conf)*. Klastrowy system plików ma dostęp do wszystkich dysków w węźle przez szybką sieć lokalną tak aby nie trzebabyło używać serwerów pośrednich. OCFS2 sprawdza się przy operacjach na dużej ilości małych plików w odróżnieniu chociażby do GFS2 który lepiej sprawdza się na dużych plikach danych.

# Konfiguracja

Konfiguracja OCFS2 w systemie linux przebiega następująco. 
Skoro OCFS2 znajduje się w jądrze linuxa od wersji 2.6.19 to nie trzeba nic instalować i możemy przejść bezpośrednio do konfiguracji. Wszystkie maszyny które chcemy połączyć muszą być w jednej sieci lokalnej, najlepiej typu SAN. 
Po pierwsze należy umieścić w pliku konfiguracyjnym informacje o węzłach w kalstrze. W tym celu należy edytować plik /etc/ocfs2/cluster.conf. Ta konfiguracja musi pojawić się we wszystkich maszynach w sieci które mają mieć dostęp do skonfigurowanego OCFS.

node:

        ip_port = 7777
        ip_address = 192.168.0.11
        number = 0
        name = ocfs
        cluster = ocfs2

node:

        ip_port = 7777
        ip_address = 192.168.1.12
        number = 1
        name = ocfs
        cluster = ocfs2

Kolejnym korkiem jest uruchomienie usługi o2cb która zarządzna dostępem węzłów do klastra.

*/etc/init.d/o2cb start*

Następnie musimy przygotować dysk do pracy w OCFS. nalezy go odpowiednio sformatowac

*mkfs.ocfs2 -b 4k -C 32K -L "etykieta" /dev/sda1*

Teraz trzeba jeszcze zamontować utowrzony dysk na wszystkich maszynach i system jest gotowy do pracy.

*mount /dev/sda1 /dir*

Do poprawnego działania w przyapdku awarii warto dodać  wcześniej skonfigurowane usługi o2cb i ocfs2 do uruchamiania podczas startu systemu. Do tego trzeba jeszcze dodać naszą partycje do pliku fstab aby była montowana razem z innymi dyskami.

*/sbin/chkconfig o2cb on*

*/sbin/chkconfig ocfs2 on*

#### Żródła:

- https://oss.oracle.com/projects/ocfs2/
- http://www.oracle.com/us/technologies/linux/025995.htm
- https://lwn.net/Articles/137278/
- https://www.slideshare.net/gpaterno1/filesystem-comparison-nfs-gfs2-ocfs2
- http://www.lazysystemadmin.com/2011/09/ocfs2-cluster-file-system-setup-guide.html
- http://www.linux-mag.com/id/6070/

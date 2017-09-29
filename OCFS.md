#  OCFS i OCFS2

OCFS czyli Oracle Cluster File System jest to specjalnie zaprojektowany system plików przez Oracle Corporation i wydana na licencji GNU General Public Liceense. Jest to wsóldzielony system plików do zarządzania bazami danych w klastrach komputerowych. Pozwala on administratorom korzystać z systemu plików dla oraclowych danobazowych plików (pliki dnaych, pliki kontrolne i dzienniki) oraz plików konfiguracyjnych. Każdy węzeł w klastrze ma dostęp do wszystkich urządzeń blokowych (dysków twardych). Dostęp jest zapewniany poprzez szbyką sieć lokalną SAN (Storage Area network).
OCFS w wersji drugiej wspiera m.in. semantykę POSIX czy listy dostępu ACL. 
OCFS2 został włączony do jądra linuxa w wersji 2.6.16 jako eksperymentalny, a w wersji 2.6.19 jako wersja normalna.

# Zasada działania

OCFS jest wydajnieszy od jedno-węzłowego systemu plików takiego jak chocby ext3. Ma on z nim jednak cechę wspólną, w swoim rdzeniu. Mimo wielu różnic między systemami implementacja OCFS jest bardzo podobna do systemu plików ext3. OCFS musi posiadać inforamcje o klastrze na którym operuje co stwarza wymóg pliku konfiguracyjnego *(/etc/ocfs2/cluster.conf)*. Klastrowy system plików ma dostęp do wszystkich dysków w węźle przez szybką sieć lokalną tak aby nie trzebabyło używać serwerów pośrednich. OCFS2 sprawdza się przy operacjach na dużej ilości małych plików w odróżnieniu chociażby do GFS2 który lepiej sprawdza się na dużych plikach danych.

#### Żródła:

- https://oss.oracle.com/projects/ocfs2/
- http://www.oracle.com/us/technologies/linux/025995.htm
- https://lwn.net/Articles/137278/
- https://www.slideshare.net/gpaterno1/filesystem-comparison-nfs-gfs2-ocfs2

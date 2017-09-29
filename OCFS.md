#  OCFS

OCFS czyli Oracle Cluster File System jest to specjalnie zaprojektowany system plików przez Oracle Corporation i wydana na licencji GNU General Public Liceense. 

#### OCFS i OCFS2

Pierwsza wersja kładła nacisk na zarządzanie bazodanowymi systemami plików (pliki danych, pliki kontrolne) oraz plikami konfiguracyjnymi. Wersja OCFS2 wspiera m.in. semantykę POSIX czy listy dostępu ACL.



# Zasada działania

OCFS jest wydajnieszy od jedno-węzłowego systemu plików takiego jak chocby ext3. Ma on z nim jednak cechę wspólną, w swoim rdzeniu. Mimo wielu różnic między systemami implementacja OCFS jest bardzo podobna do systemu plików ext3. OCFS musi posiadać inforamcje o klastrze na którym operuje co stwarza wymóg pliku konfiguracyjnego *(/etc/ocfs2/cluster.conf)*. OCFS w wersji 2 został włączony do jądra linuxa w wersji 2.6.16 jako eksperymentalny, a w wersji 2.6.19 jako wersja normalna. Klastrowy system plików ma dostęp do wszystkich dysków w węźle przez szybką sieć lokalną tak aby nie trzebabyło używać serwerów pośrednich. OCFS2 sprawdza się przy operacjach na dużej ilości małych plików w odróżnieniu chociażby do GFS2 który lepiej sprawdza się na dużych plikach danych.

OCFS w wersji 2 został włączony do jądra linuxa w wersji 2.6.16 jako eksperymentalny, a w wersji 2.6.19 jako wersja normalna. Użycie OCFS było już mozliwe w systemie Windows w wersji The OCFS version for Windows NT/2000.

#### Żródła:

- https://oss.oracle.com/projects/ocfs2/
- http://www.oracle.com/us/technologies/linux/025995.htm
- https://lwn.net/Articles/137278/
- https://www.slideshare.net/gpaterno1/filesystem-comparison-nfs-gfs2-ocfs2

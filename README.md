#Oprendszerek elmélet

## Ezek nem hivatalos zh kérdések, és nem vagyok benne biztos, hogy minden válasz helyes.

#####Mi az operációs rendszer kernel módja és felhasználói módja közti különbség?
   - Különböző védelmi szintek, kernel mód -> felügyelt mód, felhasználói mód -> oprendszer feladatok

#####Milyen kommunikációs típust ismerünk a perifériákkal?
   - Lekérdezés átvitel (polling), megszakítás (interrupt), közvetlen memória elérés (DMA)

#####Mi a "virtuális gép" operációs rendszer struktúra lényege, honnan ered ez az elv?
   - Az IBM-től származik az elv. Pl. nem érdekel, hogyan teszi át akarok másolni egy képet.

#####Mi a CHS címzés?
   - Cilinder-Head-Selecor, mágneslemeznél adatok címzésére használjuk. (mágneslemez felépítési példa)

#####Írja le az SSTF ütemezés lényegét és jellemzőit!
   - Shortest Seek Time First. A legkisebb fejmozgatást részesíti előnyben.
   - Átlagos várakozás kicsi, várakozási idő szórása nagy. Fennáll a kiéheztetés veszélye.

#####Mi az i-node tábla?
   - Könyvtárszerkezet. UNIX rendszeren minden fájlt egy i-node ír le.
   - 15 rekeszből áll 12 fájl blokkra mutat. 13., 14. ha szükséges, akkor új i-node-ra mutat.

#####Az operációs rendszerek folyamatainak milyen állapotait, állapotátmeneteit ismerjük?
   - Futó
   - Futásra kész, ideiglenesen leállították, CPU időre vár.
   - Blokkolt, ha logikailag nem lehet folytatni, pl. másik folyamat eredményére vár.
   - Állapot átmenetek: futó -> blokkolt, blokkolt -> futásra kész, futásra kész -> futó

#####A kölcsönös kizárás Peterson féle megoldásának mi a lényege? (algoritmus)
   - A kritikus szakasz előtt minden folyamat meghívja a belépés, majd utána a kilépés fv-t.

#####Mi a szemafor?
   - Dijkstra által javasolt változótípus.
   - Ha a szemafor tilosat mutat(0) akkor a folyamat elalszik
   - Ha a szemafor>0, akkor be szabad lépni a kritikus szakaszra.
   - Két művelete van: Belépéskor csökkentjük a szemafor értékét, kilépéskor növeljük. Ezek elemi műveletek.

#####Mit takar az alábbi algoritmus, mi a jellemzője?
   ![Szemafor példa](/images/szemafor01.png) ![Szemafor példa](/images/szemafor02.png)

#####Mi a különbség a szemafor és a mutex között?
   - A mutex bináris szemafor, csak 0 és 1 lehet az értéke, míg a szemafornak 0 vagy több.
   - Pl.: vasúti sínen csak egy vonat haladhat át.

#####Mit értünk folyamatok ütemezésén?
   - Több feladat futásakor el kell dönteni, hogy melyik fusson, ezt a döntést végzi el az ütemező egy algoritmus alapján.

#####Mit jelent a holtpont gráfmodellje?
   - Holtpont feltételek ábrázolása irányított gráfokkal, ahol egy folyamatot kör, egy erőforrást négyzet jelöl.
   - Ha az erőforrások, folyamatok gráfjában kör van, az holtpontot jelent.

#####Ismertesse a bankár algoritmust! Lényege!
   - Minden kérés esetén megnézi, hogy a teljesítése biztonságos-e.
   - Biztonságos állapot: létezik olyan kezdődő állapotsorozat, melynek eredményeként mindegyik folyamat megkapja a kívánt erőforrásokat és befejeződik.
   - Ha az algoritmus ilyen állapothoz vezet, akkor jóváhagyja, ha nem, akkor a kérést elhalasztja.
   - Úgy osztja el az erőforrásokat, hogy legalább egy kérés biztosan be tudjon fejeződni, így amikor vissza adja az általa használt erőforrásokat akkor a többi kérésnek több jut.

#####Mi a POSIX?
   - Portable Operating System Interface for uniX - minimális rendszerhívás készlet, szabvány.

#####Mik a(z) (1., 2., 3., 4.) generációs operációs rendszerek jellemzői?
   - 1. gen.: kapcsolótábla, vákumcső, relé, gépi kód, lyukkártyák
   - 2. gen.: tranzisztorok; oprendszerek: FMS, IMB; kötegelt rendszer, szalagos egységek;
   - 3. gen.: integrál áramkörök; kompatibiltás; OS/360; multitask; spooling; UNIX
   - 4. gen.: személyi számítógépek; LSI áramkörök; CPU fejlődés; Hálózati osztott rendszerek;

#####Mi a RAID(1..5), mi a működésének a lényege?
   - Redundant Array of Inexpensive Disks.
   - RAID0: Több lemez logikai összefűzésével új meghajtót kapunk. (összkapacitás lesz az új lemez kapacitása) Nincs védelem.
   - RAID1: Két független lemezből készít egy logikai egységet, egyszerre menti mindkettőre.(tükrözés) Tároló kapacitás felére csökken.
   - RAID2: Adatbitek mellett hibajavító biteket tartalmaz. Azaz +1 diszk.
   - RAID3: Plusz paritásdiszk. Azaz +1 diszk
   - RAID4: RAID0 + paritásdiszk
   - RAID5: Nincs paritás diszk, el van osztva a tömb összes elemére. Adatok elosztva kerülnek tárolásra. Két lemez egyidejű meghibásodása esetén okoz adatvesztést. Azaz +1 diszket igényel.
   - RAID6: RAID 5 kiegészítése paritásdiszkekkel. Azaz +2 diszk szükséges.

#####Mi a kölcsönös kizárás, mik a megvalósítás feltételei?
   - Módszer ami biztosítja, hogy a közös adatokat egyszerre csak egy folyamat tudja használni.
   - Feltételei:
      - Nincs két folyamat egyszerre a kritikus szekcióban
      - nincs CPU paraméter függőség
      - egyetlen kritikus szekción kívül lévő folyamat sem blokkolhat msik folyamatot
      - Egy folyamat sem vár örökké, hogy a kritikus szekcióba tudjon lépni.

#####Ismertesse a kölcsönös kizárás megvalósítását TSL utasítással!
   - Atomi művelet, a belépéskor TSL lock kerül a regiszterbe, a kilépésig zárolja a memóriasínt.

#####Ismertesse a folytonos tárkiosztás(lemez) stratégiáit, jellemzőit!
   - Egy elhelyezési stragétia
   - First Fit: A legelső helyre teszi az adatot, ahova még egyben befér
   - Best Fit: A legkisebb helyre teszi az adatot, ahova még egyben befér
   - Worst Fit: A lehető legnagyobb szakaszba teszi, veszteséges lemezkihasználás

#####Mi a randevú stratégia?
   - Üzenetküldés összegzését el lehet hagyni
   - Ha a send előtt van a recieve a küldő blokkolódik, illetve fordítva. pl. minix3 adatcső kommunikáció.

#####Mi a monitor?
   - Kölcsönös kizárás magasabb szinten, lehetnek benne eljárások, adatszerkezetek.
   - A monitoron belül egyszerre egy folyamat aktív, ezt a fordítóprogram automatikusan bizztosítja
   - Egyfajta mutex, de a felhasználónak a megvalósításról nincs konkrét ismerete, sokkal biztonságosabb.

#####Mit takar az alábbi algoritmus részlet, mi a jellemzője?
   ![Monitor példa](/images/monitor01.png)
   Monitor megvalósítása

#####Mi a mutex?
   - Bináris szemafor, 0 vagy 1 lehet az értéke. Pl. vasutas probléma: egyszerre csak egy vonat tud menni a sínen.

#####Mi a soft real time rendszer?
   - Egy valós idejű ütemezési rendszer. Léteznek határidők, de ezek kismértékű elmulasztása tolerálható.

#####Mit jelent a monitor "condition" típusa?
   - Állapot változó, arra szolgál, ha egy folyamat nem tud továbbmenni a monitoron.
   - Két művelete van: wait, signal.

#####Mi a garantált ütemezés lényege?
   - Minden folyamat arányos CPU időt kap.
   - Nyilvántartjuk, hogy egy folyamat eddig mennyit kapott, aki kevesebbet kapott az kerül előre.

#####Mi az arányos ütemezés lényege?
   - Minden felhasználó arányos CPU időt kap, attól függetlenül, hogy hány folyamatot futtatnak.
   - Nyilvántartjuk, hogy egy felhasználó eddig mennyit kapott, aki kevesebbet kapott az kerül előre.

#####Mi az Ext2FS, van-e MBR-je?
   - Fájlrendszer típus, minden merevlemeznek van MBR-je függetlenül a fájlrendszertől.
   - Fájlrendszernek nincs MBR-je!

#####Mi a TLB, mi a szerepe?
   - Translation Lookaside Buffer egy cache, amit a memória kezelő hardver használ, hogy gyorsítson a virtuális címfordítás sebességén.

#####Milyen I/O eszközkategóriákat ismer? Mi a kivétel?
   - Blokkos eszközök
   - Karakteres eszközök
   - Időzítő - kivétel nem blokkos és nem Karakteres

#####Mi az MBR?
   - Master Boot Record,a 0.szektor. 2 particíója van az elsőről töltődik be az operációs rendszer

#####Mi a memóriakezelő feladata?
   - Memória nyilvántartása amelyek szabadok
   - Memóriát foglal a folyamatoknak
   - Memóriát szabadít fel
   - Csere vezérlése a RAM és a lemezek között

#####Mit értünk tevékeny várakozás alatt?
   - A kölcsönös kizárásnál a CPU-t üres ciklusban járatjuk a várakozás során, így a CPU időt pazaroljuk pl. TSL, Peterson

#####Mit értünk folyamatok erőforrás görbélyén, mire használható?
   - Folyamatok erőforrás görbéje ábrázolja, hogy mikor mennyi erőforrásra van szüksége a folyamatoknak, és hol alakulhat ki holtpont, ez segít úgy tervezni, hogy elkerüljük a holtpontot, pl. bankár algoritmusnál használjuk.

#####Mit értünk virtuális memóriakezelésen, mi a lényege? Mi a lapozás?
   - Egy program használhat több memóriát, mint a rendelkezésre álló fizikai méret. Egy program a virtuális memória térben tartózkodik. A vírtuális címtér lapokra van osztva. Ha az MMU látja, hogy egy lap nincs a memóriában, akkor laphibát okoz, op. rendszer kitesz egy lapkeretet majd behozza a szükséges lapot.

#####Mi a szoftveres és a hardveres megszakítás közti különbség? Van egyáltalán?
   - A szoftveres megszakítás kezelése azonos a hardveres megszakítás kezelésével.

#####Mi a sorsjáték ütemezés, lényege?
   - A folyamatok között sorsjegyeket osztunk szét, és az kapja a vezérlést akinél a kihúzott jegy van. Arányos CPU idő biztosítás.

#####Mi az SSTF ütemezés lényege?
   - Shortest Seek Time First, leghamarabb elérhetőt dolgozzuk fel először

#####Mi az Ext2FS, van-e MBR-je?-je.
   - Linux fájlrendszer és van MBR.

#####Mi a TLB, mi a szerepe?
   - Translation Lookaside Buffer egy cache, amit a memória kezelő hardver használ, hogy gyorsítson a virtuális címfordítás sebességén.

#####Honnan származik, és mi a lényege a virtuális gépek(szerver) használatának?
#####Mi a Round-Robin ütemezés lényege?
   - Körben járó ütemezés. Mindenkinek van időszelete, aminek a végén, vagy blokkolás esetén jön a következő folyamat. Időszelet végén a körkörös listában következő jön. Pártatlan, egyszerű. Egy listában tároljuk a folyamatok jellemzőit és ezen megyünk körbe.

#####Milyen partíciónak nincs i-node táblája?
   - Csak a UNIX rendszereknek van i-node táblája.

#####Mi a RAID0+1 illetve RAID1+0 lemezek közti különbség?
   - RAID 1+0: Tükrös diszkekből vonunk össze többet
   - RAID 0+1: Raid 0 összevont lemezcsoportból veszünk kettőt.

#####Honnan származik az op.rendszer virtualizáció, mik a jellemzői, mi köze a virtuális memóriakezeléshez?
#####Mit nevezünk szegmentált memóriakezelésnek?
   - Egymástól független címtereket hozunk létre, ezeket szegmenseknek nevezzük. 2 részből áll az elérési címük : szegmens szám és ezen belüli eltolás.
   
#####Mi a valós idejű ütemezés lényege?
   - Garantáljuk adott határidőre a válaszadást. Hard Time - nem módosítható határidők, Soft Real Time - kis mértékű időbeli eltolódás tolerálható. A programot több kisebb folyamatokr a bontják.

#####Milyen processzor védelmi szinteket ismer, hol használjuk ezeket?
   - 4 szintet különböztetünk meg, ebből 2-t használunk: kernel mód, felhasználói mód.
   - Kernel mód: felügyelt mód
   - Felhasználói mód: oprendszer, feladatok

#####Ismertesse a "probléma figyelmen kívül hagyása" módszert! Hol alkalmazzák?
   - Holtpont kezelési módszer, egyszerűen figyelmen kívül hagyuk, hátha nem okoz gondot, nagyon ritkán alakul ki és költséges a figyelése, ezért nem is figyelünk rá, Windows, Unix ezt használja.

#####Mi az MFT?
   - Master File Table, ezzel kezdődik az NTFS partició, 16 attribútum ad egy fájl bejegyzést, minden attribútum max 1kb. Ha ez nem elég, akkor egy attribútum mutat a folytatásra. Nincs fájlméret maximum.

#####Mi a probléma a kölcsönös kizárás szigorú váltogatásos megvalósítással?
   - Egy folyamat blokkolhatja saját magát.

#####Mit jelent az "interleave" fogalma?
#####Mit nevezünk valós idejű operációs rendszernek?
#####Milyen fájlrendszer specifikus fájlokat ismer? Hol találhatók átalában?
   - Karakter,blokk fájlok, /dev könyvtár

#####Mit nevezünk fájlrendszernek, mi köze van az FCFS ütemezéshez?
   - A számítógépes fájlok tárolásának és rendszerezésének a módszere.A sorrendi ütemezéssel olvashatunk és írhatunk a lemezre, aminek a rendszerét a fájlrendszer adja.

#####I/O szoftver modellje, milyen eszközkategóriákat ismer?
#####Mit nevezünk kritikus tevékenységnek?
   - Kritikus programterület, szekció, az a rész mikor a közös erőforrást (memóriát) használjuk.
#####Mire szolgálnak a lapozási algoritmusok?
   - Ha nincs egy virtuális című lap a memóriában, akkor egy lapot ki kell dobni, és berakni ezt az új lapot.

#####Mi a különbség folyamatok és szálak között? Van egyáltalán?
   - A szál egy folyamaton belüli utasítás sor. Lehet több is egy folyamaton belül
   - csak a folyamatoknak van: címtartománya, globális változója, megnyitott fájl leírója, gyermek folyamata, szignálkezelője, ébresztője

#####Ismertesse a laptáblák szerepét! Vam köze a TLB-Hez?
   - A virtuális címtér lapokra van osztva,laptábána tároljuk a lapokat. Ezeken keresztül tudjuk elérni a memória lapjait.  64 bites címezésnél ez már megvalósíthatatlan, ezért használunk TBL-t mellette.

#####Miért hasznos a kölcsönös kizárás üzenetküldéses megvalósítása?
   -
#####Mire használható a monitor?
   - Kölcsönös kizárásra, magasabb szinten. Akkor használható jól, ha CPU-knak közös memóriájuk van.

#####Mire jó a "Dirty-bit", hol használják?
   - Az MMU a lapok kezelésénél használja, ha a dirty bit 1 akkor módosult a lpkeret memória azaz lemezre íráskor tényleg ki kell írni.

#####Mi a CHS-LBA címzés közti különbség? Van egyáltalán?
   - CHS korlát 504MB, LBA minden szektor egyedi számot kap. A BIOS a megszakítások paramétereit az átalakított geometriából lemez geometriává alakítja CHS-nél, míg szektor számmá LBA-nál.

### Források:
   - előadás diák
   - iNfeRuS4 innen: elte.sharq.hu

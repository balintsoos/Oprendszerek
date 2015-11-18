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
   - Szemafor megvalósítása

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

#####Ismertesse a kölcsönös kizárás „szigorú váltogatás” megvalósítását!
   - A kölcsönös kizárás feltételeit teljesíti kivéve azt hogy egyetlen kritikus szekción kívüli folyamat sem blokkolhat másik folyamatot. 

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
   - Monitor megvalósítása

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
   - Egy program használhat több memóriát, mint a rendelkezésre álló fizikai méret.
   - A memóriában tárolt, de éppen nem használt blokkokat kiírja a külső tárolóra.
   - A virtuális címtér „lapokra” van osztva. Lapozásnak hívjuk, mikor a logikai címből előállítjuk a fizikai címet.

#####Mi a szoftveres és a hardveres megszakítás közti különbség? Van egyáltalán?
   - A szoftveres megszakítás kezelése azonos a hardveres megszakítás kezelésével.

#####Mi a sorsjáték ütemezés, lényege, hol használják?
   - A folyamatok között sorsjegyeket osztunk szét és az kapja a vezérlést akinél a kihúzott jegy van
   - Arányos CPU idő biztosítás.
   - Hasznos pl. video szervereknél.

#####Mi az SSTF ütemezés lényege?
   - Shortest Seek Time First, leghamarabb elérhetőt dolgozzuk fel először

#####Mi az Ext2FS, van-e MBR-je?-je.
   - Linux fájlrendszer és van MBR.

#####Mi a TLB, mi a szerepe?
   - Translation Lookaside Buffer egy cache, amit a memória kezelő hardver használ, hogy gyorsítson a virtuális címfordítás sebességén.

#####Mi a Round-Robin ütemezés lényege?
   - Körben járó ütemezés. Mindenkinek van időszelete, aminek a végén, vagy blokkolás esetén jön a következő folyamat.
   - Egy listában tároljuk a folyamatok jellemzőit és ezen megyünk körbe.

#####Milyen partíciónak nincs i-node táblája?
   - Csak a UNIX rendszereknek van i-node táblája.

#####Mi a RAID0+1 illetve RAID1+0 lemezek közti különbség?
   - RAID 1+0: Tükrös diszkekből vonunk össze többet
   - RAID 0+1: RAID0 összevont lemezcsoportból veszünk kettőt.

#####Mit nevezünk szegmentált memóriakezelésnek?
   - Egymástól független címtereket hozunk létre, ezeket szegmenseknek nevezzük.
   - Minden szegmensnek megvan a saját 0-tól kezdődő címtartománya.
   - 2 részből áll az elérési címük : szegmens címből és offset címből.
   
#####Mi a valós idejű ütemezés lényege?
   - Garantáljuk adott határidőre a válaszadást.
   - Hard Time - nem módosítható határidők
   - Soft Real Time - kis mértékű időbeli eltolódás tolerálható.
   - A programot több kisebb folyamatokr a bontják.

#####Milyen processzor védelmi szinteket ismer, hol használjuk ezeket?
   - Intel 80286: minden utasítás egyenlő
   - Intel 80386:
      - 4 szintet különböztetünk meg, ebből 2-t használunk: kernel mód, felhasználói mód.
      - Kernel mód: felügyelt mód
      - Felhasználói mód: oprendszer, feladatok
   - A Unix és Windows világ is ezt használja.

#####Ismertesse a "probléma figyelmen kívül hagyása" módszert! Hol alkalmazzák? ("strucc" módszer)
   - Holtpont kezelési módszer
   - Egyszerűen figyelmen kívül hagyuk és reménykedünk, hátha nem okoz gondot
   - Nagyon ritkán alakul ki és költséges a figyelése, ezért nem is figyelünk rá
   - Windows, Unix ezt használja.

#####Mi az MFT?
   - Master File Table
   - Ezzel kezdődik az NTFS partició
   - 16 attribútum ad egy fájl bejegyzést, minden attribútum max 1kb.
   - Ha ez nem elég, akkor egy attribútum mutat a folytatásra. Nincs fájlméret maximum.

#####Mi a probléma a kölcsönös kizárás szigorú váltogatásos megvalósítással?
   - Egy folyamat blokkolhatja saját magát.

#####Milyen fájlrendszer specifikus fájlokat ismer? Hol találhatók átalában?
   - Karakter,blokk fájlok
   - /dev könyvtárban találhatóak

#####Mit nevezünk fájlrendszernek, mi köze van az FCFS ütemezéshez?
   - A számítógépes fájlok tárolásának és rendszerezésének a módszere.
   - A sorrendi ütemezéssel olvashatunk és írhatunk a lemezre, aminek a rendszerét a fájlrendszer adja.

#####Mit nevezünk kritikus tevékenységnek/programterületnek/szekciónak?
   - Kritikus programterület, szekció, az a rész mikor a közös erőforrást (memóriát) használjuk.

#####Mire szolgálnak a lapozási algoritmusok?
   - Ha nincs egy virtuális című lap a memóriában, akkor egy lapot ki kell dobni, és berakni ezt az új lapot.

#####Mi a különbség folyamatok és szálak között? Van egyáltalán?
   - A szál egy folyamaton belüli utasítás sor. Lehet több is egy folyamaton belül
   - csak a folyamatoknak van: címtartománya, globális változója, gyermek folyamata, szignálkezelője...
   - csak szálnak van: utasításszámláló, regiszterek, verem

#####Ismertesse a laptáblák szerepét! Vam köze a TLB-Hez?
   - A virtuális címtér lapokra van osztva,laptábána tároljuk a lapokat. Ezeken keresztül tudjuk elérni a memória lapjait.  64 bites címezésnél ez már megvalósíthatatlan, ezért használunk TBL-t mellette.

#####Miért hasznos a kölcsönös kizárás üzenetküldéses megvalósítása?
   -
#####Mire használható a monitor?
   - Kölcsönös kizárásra, magasabb szinten. Akkor használható jól, ha CPU-knak közös memóriájuk van.

#####Mire jó a "Dirty-bit", hol használják?
   - Az MMU (Memory Management Unit) a lapok kezelésénél használja
   - Ha a dirty bit 1 akkor módosult a lapkeret memória, azaz lemezre íráskor tényleg ki kell írni.

#####Mi a CHS-LBA címzés közti különbség? Van egyáltalán?
   - CHS korlát 504MB
   - LBA minden szektor egyedi számot kap.
   - A BIOS a megszakítások paramétereit az átalakított geometriából lemez geometriává alakítja CHS-nél
   - míg szektor számmá LBA-nál.

#####Mit értünk monopol módú eszköz alatt?
   - Megszakíthatatlan, egyedi használatú eszköz.
   - 
#####Mit jelent az "interleave" fogalma?
   - Lemezek forgási sebessége miatt a blokkok nem feltétlenül szomszédosak
   - Interleave: párosával „szomszédosak”

#####Mi a FAT, van-e MBR-je?
   - File Allocation Table. Fájlrendszer típus. Láncolt listás nyilvántartás.
   - MBR (Master Boot Record) egy külön része a merevlemeznek, nincs összefüggésben a fájlrendszerekkel.

#####Mit takar, mire jó az alábbi algoritmus részlet, mi a jellemzője?
   ![TSL példa](/images/TSL01.png)
   - Példa TSL-re! (Test and Set Lock: Akkor hajtódik végre, amikor egy folyamat a kritikus szekcióba akar lépni.)

#####Mondj példát láncolt szerkezetű fáljrendszerre!
   - FAT (File Allocation Table) [32]

#####Jellemezze a real time multitask rendszert röviden!
   - Olyan operációs rendszerekre jellemző, amelyek egyszerre több folyamatot/szálat tudnak futtatni.
   - Az ütemező dönti el, hogy melyik folyamat futhat, de a látszattal ellentétben mindig csak egy folyamat fut.

#####Mi a hardver RAID és a szoftver RAID közti különbség, mi a működésük lényege?
   - Ha oprendszer nyújtja, akkor szoftver RAID
   - Ha külső vezérlőegység, akkor hardver RAID

#####Mi az oka a 2TB HDD címzési határnak, Van ilyen egyáltalán?
   - MBR mérete: 512 bájt
   - 13-14-15-16. bájt: Szektorok száma
   	- 4 bájt: 4 GB * 512 = 2 TB

#####Honnan származik az op.rendszer virtualizáció, mik a jellemzői, mi köze a virtuális memóriakezeléshez?
#####Mire szolgálnak a lapozási algoritmusok?
#####Miért hasznos a kölcsönös kizárás üzenetküldéses megvalósítása?
#####Mire használható a monitor?
#####Mit takar az alábbi algoritmus részlet, mi a baj vele, ha van?
	while(1)
	{
		while(kovetkezo!=1);
		kritikus_szekcio();
		kovetkezo = 0;
		nem_kritikus_szekcio();
	}

#####Milyen jellemző fájlrendszer elhelyezési stratégiákat ismer? Melyik veszteséges?
#####Mi a memóriiakezelő feladata dinamikus memória használat során?
#####Mi az oka, hogy bizonyos helyzetben üzenetekkel biztosítjuk a kölcsönös kizárást?
#####Mi a virtuális memóriakezelés és a virtuális gép közti különbség?
#####Melyik állítás lehet igaz? Miért?
	- A: Szoftveresen kezelem le a hardver megszakítást.
	- B: Hardveresen kezelem a szoftver megszakítást.
#####Írja le egy operációs rendszer boot folyamatát!
#####Mi az eszközmeghajtó program?
#####Mi a mutex és egy egyszerű egész közti különbség? Van egyáltalán?

### Egyebek:

#####Regiszter
   - A regiszterek a CPU gyorsan írható/olvasható, ideiglenes tartalmú, általában 2-4 bájt feldolgozására alkalmas tárolóegységei.

#####Megszakítások
   - Szoftveres és hardveress megszakítás azonos.
   - Hardveres megszakítás esetén amennyiben a megszakításkérés teljesíthető, a kezdeményező eszköz használhatja a CPU-t.
   - Szoftveres megszakítás esetén a főprogram futását egy alprogram szakítja meg. Majd ha végzett, a főprogram tovább fut.

#####Feladat maszkolása
   - megszakítások engedélyezése, letiltása.

#####Nem maszkolható feladatok
   - súlyos hardver hiba, pl.: memóriahiba, vagy tápfeszültség kimaradás esetén keletkezik.

#####Operációs rendszer
   - Olyan program, ami egyszerű felhasználói felületet nyújt, eltakarva a rendszer eszközeit.

#####API (Application Programming Interface)
   - Egy program vagy rendszerprogram eljárásai és ezek dokumentációi, amelyet más programok felhasználhatnak.

#####Firmware
   - A gyártó által a hardverbe épített szoftver. (pl.: távkapcsoló)

#####Middleware
   - Operációs rendszer feletti réteg

#####

#####

#####

### Források:
   - előadás diák
   - iNfeRuS4 innen: elte.sharq.hu

# kidolgozikma
Ez a kód Oldal Gábor kódja, a Green Fox akadémia discord szerverén osztotta meg, ebből csináltam magamnak egy másolatot a későbbi tanulmányozás végett.

A Pen created on CodePen.io. Original URL: [https://codepen.io/gvandor/pen/LYMJXQE](https://codepen.io/gvandor/pen/LYMJXQE).

Oldal Gábor — tegnap 14:02-kor
No ezt nem fogom tudni most megmutatni, de korábban láthattuk, hogy a .btn-group a legnagyobb elemünk, ami 664px széles. 45px a gap, ami a nav, és a napok között foglal helyet. A nav pedig mindössze 133px széles a jelenlegi betüméret, és betűcsalád mellett.
[14:03]
Gyakorlatilag a nagy gridünk (main) kellene ez esetben egy oszlopossá tenni a mobilos nézethez, és sajnos a napokat kell ugyanígy megoldanunk, mivel a 360px jelenleg a "legkisebb" mobil szélesség, amit valaki is használ.
[14:04]
A jelenlegi kód a nagy méretre van beállítva.
[14:05]
Kikommentezünk sorokat, hogy későbbre meglegyen, mikor odaérek, és így már kisebb eszközön is szépen fog kinézni. ￼
[14:09]
￼
￼
Oldal Gábor — tegnap 14:10-kor
És ez egy érdekes része az átírásnak. Más a kódom, mégis ugyanaz az elrendezés. Ez, hogy lehet?
[14:11]
Az átírt résszel nincs is baj. Viszont, ami utána jön ebben az esetben implicit (automatikusan) létrehozza ugyanezt az elrendezést.
[14:12]
Headerre meg van adva, hogy a második oszlopban kezdődjön, még akkor is, ha csak 1 oszlopot definiáltunk. Valójában oszlop definíció nélkül is működhet.
[14:13]
￼
[14:13]
És igen, működik.
[14:15]
Header column-start kiütése.
[14:15]
￼
[14:16]
Elméletben a h1 span levétele után már oszlopos elrendezésbe kerülünk.
[14:16]
￼
[14:17]
És igen, bármennyire is nem így tűnik.
￼
Oldal Gábor — tegnap 14:19-kor
A napok egy igen széles része a dolognak, így azt is 1 oszlopossá tenném. Igaz, hogy lehetne 2-3 nap is egy sorban, de nem tükrözné a napok hétben betöltött szerepét. Természetesen úgy is lehet.
[14:21]
82px széles egy gomb, és 15px van köztük, meg a szélen, mint padding. Az 15+82+15+82+15+82+15=306px. Egy 360px-es sorba simán beleférne
[14:25]
Mivel a main block típusú, és megmondtuk neki, hogy a lehető legkisebb legyen a tatalmához mérten, a szélességére vonatkozó szabályt (min-content) kiveszem, így a legnagyobbra fog törekedni.
Kép
A nevek jól néznek ki a h1 is, a többi nem igazán. Nézzük 100%-on.
Kép
Értelem szerűen a napoknál a navnál maradnia kell a flexnek, különben nem lesznek stretchelve, és nem férne el különben kettőnél több egy sorban. Az is természetesen megoldás, hogy 2, aztán 1 elem soronként, de nem feltétlen a leg tetszetősebb.
Ha szimplán kiveszem, ezt az eredményt kapjuk, mivel inline elemek.
Kép
Erről jut eszembe, ez igen zavaró, és általában listába tesszük őket, amit már ezer éve megtehettünk volna.
Oldal Gábor — tegnap 15:05-kor
Kép
A helyzet hasonló. Bár már most nem inline elembe vannak csomagolva, így jelenleg másképp is viselkednek.
Innentől kezdve viszont át kell írni pár szabályt, mivel a listára is fel kell aggatni pár dolgot, és nagyon nem jó már az inline <a> elem.
Az <a> elem kattinthatósága miatt, a zöldrészen belül muszáj, hogy az <a> elem része legyen. Átnézve a{} szabályait a cursor szabály nem kell, mivel <a> alapból mutatóujjas ikont kap, ha fölé visszük az egeret.
Kipróbáljuk block szintűként. Nem szeretjük az inline-blockot, vannak bizonyos esetekben érdekes mellékhatásai. 
Oldal Gábor — tegnap 15:13-kor
Kép
Állítsuk be a listás alapértelmezett dolgokat "normálisra".
ul rendelkezik egy fenti, lenti margóval, egy bal oldali paddinggal, és a listaelemek jelzésével. Ezeket írjuk felül.
Kép
ul{
  margin:0;
  padding:0;
  list-style-type:none;
}
a list-style-type egyébként az li elemek tulajdonsága, de öröklődik automatikusan, így nem kell külön kijelölőt írni neki.
Kép
Oldal Gábor — tegnap 15:21-kor
Nincs eltartás. gap-hez minimum flex kell, így az li elemek margózása helyett inkább ezt javasolnám.
Kép
Ha így tetszik, akkor jó.
Kép
Oldal Gábor — tegnap 15:44-kor
Kivettem az oszlopos elrendezést, túl hosszúra nyúlik.
364.85px széles lesz így maga az ul, és ugyan 360px szélesre van állítva az ablak, de annak része a görgetősáv, így kb. 21px nem fért ki. 5 + 16 scrollbar.
.btn osztályunkra is alkalmaznám a listás dolgot. Így szoktuk alapon. Sokszor jól is van úgy, itt részben felesleges, mivel egyáltalán nem foglalkozunk a hátterekkel, keretekkel.
A jó most ebben, hogy a div innentől kezdve nem kell. Ul átveszi a szerepét.
Oldal Gábor — tegnap 15:56-kor
Kép
ul lett az új .btn-group. Itt javítsuk azt is, hogy mint gomb csoport több is van ilyen, mégsem adtuk nekik ezt a classt. A funkciójára sem utal. A hónap napjai, mint days-of-month.
Kép
Igaz a html-ben nem lett átírva még, de ul-re "hasonló" szabályokat írtunk.
Oldal Gábor — tegnap 16:03-kor
Ha nem tetszene így, megtehetjük, hogy mondjuk a napoknál 3 gomb egymás mellett jelenjen meg.
grid template kell hozzá 3 x 1fr-rel days-of-monthon.
Több nem férne el ezen a szélességen.
Kép
82-ről 93.6667-re nőtt a gombok szélessége.
Ez volt a legkisebb felbontás, amire fel vagyunk készülve bármelyik is tetszik az elrendezésből.
Oldal Gábor — tegnap 16:10-kor
Következő szélességi állomásunk nem az eszközök leggyakoribb felbontásából fog adódni, hanem a tartalmunkból. A nav 365px széles lenne, ha egy sorban lenne. Egy kis kerekítgetés, és legyen 400px.
min-width: 400px:
Oldal Gábor — tegnap 18:06-kor
Annak ellenére, hogy próbál körültekintő lenni az ember, nem mindig sikerül. Szerintem vétettem pár hibát, amit most megpróbálok kijavítani. Ugy, ahogy csinálom, úgy írom.
Egyrészt minden hivatkozás listából ul-t csináltam.
Az ul-ek lehetnének az elemei a nagy egész main-nek, plusz  a h1, de akkor jelentés nélkül maradnának, azon felül, hogy listák.
Oldal Gábor — tegnap 18:13-kor
Másik, hogy pont az újabb elemek miatt a css kijelölőim már nem jók, de azt most fogom megnézni. 🙂
Először, ott a main, a mindent is tároló elemünk. Van rajta margin, de minek, mivel a lehető legnagyobb lesz, és paddinggal van megoldva az eltartás.
Kép
Másik, hogy bármennyire is kicsi, még így is lehet nagyobb az eltartás a széleken, vagy pont ellenkezőleg.
Oldal Gábor — tegnap 18:21-kor
Kép
Mobilon nem néz ki rosszul, de még 5px esetén is elveszítjük az árnyékolást a lap alján. Igazából mobilon nem annyira látványos ez, mert elég nehéz hover effektet elérni. 
Másik lehetőség a %-os eltartás. Ennek is van értelme. Egy bizonyos szintig a képernyőmérettel együtt nő a margó is.
Oldal Gábor — tegnap 18:29-kor
Kép
És természetesen a gap-pel is lehet még játszani.
Egyébként akkor esett le, hogy valami nem jó, mikor <a>-ról leszedtem a display: blockot. 
Oldal Gábor — tegnap 18:45-kor
Kép
Nagyon nem így kellett volna kinéznie.
main>header>ul>li>a: 
Az <a>-ra aggatott tulajdonságok a displayt leszámítva jók.
ul-nél csak a margin, padding, és list style-nak kell maradnia, a többit egyénenként kell kezelni. Azok nem mindenhol közös tulajdonságok.
Kép
header helyett a flex tulajdonságok elméletben li-re kellenek headeren belül. Header innentől kezdve szerintem nem is kell.
Oldal Gábor — tegnap 18:55-kor
header li-re kell a flex: 1 0 0
nav ul{
  display: flex;
  flex-direction: column;
  gap: 15px;
}
days of month az jó, mert ul lett az új div.
És <a>-ra a display tulajdonság is kell, jelenleg block;
Kép
Oldal Gábor — tegnap 19:04-kor
Éppenhogy átlépve a 400 képpont szélességet, azonnal kékre váltanak a gombok, mert ezt állítottam be. Erre írok újabb tulajdonságokat, mint ígértem.
Kép
Az elrendezés, itt annyiban fog változni, hogy a nav elemei már elférnek egymás mellett.
Oldal Gábor — tegnap 19:44-kor
Kép
Írtam korábban, hogy mi mekkora, csak kitöröltem, mert nem működött. Ám közben rájöttem mi a baj. Nagyjából 450px-ben kell meghatározni a következő töréspontot, mert különben nem férnek el a nav elemei egymás mellett túlcsordulás nélkül. 15px eltartást is megenged a széleken. Annál nem sokkal többet. 
Viszont összeesik. "Szabi terv." Újra meg kell adnunk egy méretet.
Ráadásul <a> elemre kell alkalmazni.
Kép
Kép
Oldal Gábor — tegnap 19:51-kor
Látszik, hogy az a elem kisebb, mint li. Ul-en van flex. Li-n viszont nincs, ami a-t tartalmazza. Avagy ide most fel kell vennünk.
Kép
A transition all 0.4s sem jó, mert így váltásnál az <a> elem animálódik, és igen kelemetlen ugrást okoz.
Kép
all javítva árnyékra.
Oldal Gábor — tegnap 21:02-kor
Sakkozgatva, és nézve, 700px-nél is elég kellemesen néz ki: 
Kép
A következő megálló valahol itt lesz, ahol is a days-of... 7 oszlopra válik szét.
Kép
800 a határ talán beleférünk.
Oldal Gábor — tegnap 21:11-kor
Itt a header szabályai maradnak, a h1-é is, és a navot is gondolnám, hogy megfelelő lesz. Az egyetlen, amivel most foglalkozni kell a days...
Mivel mobil nézetben ez a kódja:
.days-of-month {
  /*width: max-content;*/
  display: grid;
  /*grid-template-columns: repeat(7, 1fr);*/
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
}
gyakorlatilag a 2 kikommentezett sort kell érvényesítenünk. 
Kép
Elsőre jónak is tűnt, de nem egészen ezt vártam.
664px széles így, ezért egy kis eltartás végett a képernyő széleitől 700px-től aktiválom ezt az elrendezést.
Kereken 700px-en:
Kép
Oldal Gábor — tegnap 21:20-kor
Van némi túlcsordulás. Jobb alul ki van emelve, hogy kb. 35px a bal margó, illetve a jobb is. És ez az 5 százalék az, amiért a túlcsordulás megtörténik. A mainen felül kell írni, most automatikusra, hogy felül is maradjon valamennyi, meg alul is persze. Én elsőre preferálnám a 15px-elt.
Ehhez azért még kell egy width: min-content is.
700px:
Kép
1200px
Kép
Oldal Gábor — tegnap 21:30-kor
Következő megálló 1200px elsőre.
Most az eredeti állapotot kellene visszaállítani, ami a reszponzív elrendezések előtt volt.
Main, grid szabályok.
A kiemelt sort kell egyedül betenni, és a többi kommentet most már lehet törölni. Csak ez hiányzik az egyel kisebb breakponthoz képest.
Kép
Ez így jó is. A grid ismét 2 oszlopos.
Kép
Oldal Gábor — tegnap 21:37-kor
Az alap css ez:
header {
  /*grid-column-start: 2;*/
  /*display: flex;
  flex-wrap: wrap;
  gap: 15px;*/
}
header ul {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}
 
A kikommentezett flex sorok átkerültek ul-hez. Így azok törölhetőek és az egyetlen megmaradt is, csak a grid-column-start-ot kell érvényre juttatni az új viewport szélességen.
Kép
Ez is megvan.
h1 hasonlóan span:
Kép
Navra vonatkozó szabályok:
Ezzel indultunk:
nav ul {
  display: flex;
  flex-direction: column;
  gap: 15px;
  /*width: max-content;*/
}
Aztán később ez került be:
nav ul {
    flex-direction: row;
}
nav li {
  flex: 1 0 0;
  display: flex;
}
nav a {
  width: max-content;
  flex: 1 0 0;
}
 
Oldal Gábor — tegnap 21:45-kor
Így olyan, mintha most ez lenne:
nav ul {
  display: flex;
  /*flex-direction: row; az alapértelmezett, mintha nem is írtuk volna le.*/
  gap: 15px;
}
/*stb.*/
Ebből újra oszlopot kell csinálnunk.
Kép
Tulajdonképpen kész. Mind ugyanakkora.
main is pont a széléig ér.
Oldal Gábor — tegnap 21:52-kor
Kép
kb. 843px széles.
Kerekítek 900px-től lesz ez az elrendezés.
Teljes kód: https://codepen.io/hirszerzesharcos/pen/poqKMrg?editors=0100
Oldal Gábor — tegnap 22:02-kor
Egy body min-width-tel biztosítottam még azt, ha valaki túl kicsiben nézné, akkor ne a zöld gombok végéig tudjon görgetni jobbra, hanem a kis margó végéig, mintha az is része lenne az oldalnak. 



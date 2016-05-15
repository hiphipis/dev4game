
Programavimo mokymosi užduotis
========================
Tikslas - susipažinti su kolekcijomis.

Teorija
-------
Kaip taisyklė šiuolaikinės programos manipuliuoja dideliais vienarūšies informacijos kiekiais.
Paprastai vienos rūšies duomenys programoje būna pasidedami taip, kad būtų galima patogiai pasiekti
kiekvieną atskirą duomenų įrašą. Ankstesnėse programavimo kalbose tam buvo plačiai naudojami
duomenų masyvai. Šiuolaikinės programavimo kalbos (Java, C++, etc.) taip pat turi
masyvų aprašymo galimybes. Tačiau programuojant sudėtingesnius algoritmus dažnai prireikia
ne tik keisti masyvo elementų turinį, bet ir manipuliuoti pačiais masyvo elementais: įterpti
naują reikšmę į tam tikrą poziciją masyve; pašalinti masyvo elementą; išplėsti masyvą; ir t.t. ir pan.
Tokiems veiksmams atlikti masyvai nėra labai patogus mechanizmas. Todėl šiuolaikinės kalbos
turi ir standartinių algoritmų rinkinį skirtą palengvinti tokias manipuliacijas duomenimis.
Kaip taisyklė šie rinkiniai vadinami standartinėmis kolekcijų bibliotekomis.
Apie stadartinę Java programavimo kalbos kolekcijų biblioteką galima pasiskaityti
<http://www.tutorialspoint.com/java/java_collections.htm> ir
<https://docs.oracle.com/javase/tutorial/collections/>.

Panagrinėkime paprastą pavyzdį:
```java
import java.util.*; // Įtraukiame visą pagalbinių (util) funkcijų biblioteką

public class CollectionsDemo {

   public static void main(String[] args) {
      List<Integer> l1 =	// Aprašome kintamąjį l1, kuris rodys į Integer tipo sąrašą (List)
          new LinkedList<Integer>();	// Sukuriame susietų (Linked) elementų tipo sąrašą (List) ir priskiriame kintamąjam l1
      l1.add(10);	// į sąrašą patalpiname reikšmę '10'
      l1.add(2);	// į sąrašą patalpiname reikšmę '2'
      l1.add(30);	// į sąrašą patalpiname reikšmę '30'
      System.out.println();
      System.out.println(" LinkedList Elements");
      System.out.print("\t" + l1);	// Atspausdiname visus sąrašo elementus
   }
}
```
Įvykdžius šią programą gausime štai tokį rezultatą:
```

 LinkedList Elements
        [10, 2, 30]
```
Į ką reikėtų dar atkreipti dėmesį šioje elementarioje programėlėje:

1. Aprašant kintamąjį **l1** kaip tipas nurodyta **_interface_** rūšies klasė **_List_**.
**_interface_** rūšies klasės ypatingos tuom, kad jose (kalbant supaprastintai) būna tik
sąrašas funkcijų, kurias turėtų įgyvendinti kažkokia kita **_class_** rūšies klasė, tačiau
pačių funkcijų "kūnų" **_interface_** rūšies klasėse nebūna. Mūsų nagrinėjamo pavyzdžio
atveju tą funkcijų sąrašą įgyvendina **_LinkedList_** klasė, kurios objektą ir sukuriame.
Toks atskyrimas yra patogus tuom, kad esant reikalui galima parinktį kitokį funkcijų
įgyvendinimo būdą, kuris būtų efektyvesnis konkrečiu atveju. Kaip pvz. galima paminėti,
jog standartinėje Java kolekcijų bibliotekoje be **_LinkedList_** dar yra **_ArrayList_**
kuris įgyvendina tuos pačius **_List_** metodus viduje naudodamas standartinius masyvus
ir yra efektyvesnis už **_LinkedList_**, kai tiksliai žinome, koks didžiausias galimas
kolekcijos elementų kiekis.
2. Aprašant kolekcijų kintamuosius ir kuriant pačias kolekcijas yra naudojami taip vadinami
šablono (angl.k.: _template_) parametrai, kurie nusako, kokio tipo elementai bus saugomi
kolekcijoje. Mūsų pavyzdyje tai yra **_Integer_** tipas, kuris užrašytas tarp ženklų < ir >
šalia kolekcijos tipų pavadinimų _List<**Integer**>_ ir _LinkedList<**Integer**>_ . Pirmosiose Java
programavimo kalbos versijose nebuvo šablonų parametrų mechanizmo, todėl kolekcijų klases
būtų galima naudoti ir nenurodant šių parametrų. Tačiau naudojant šiuos parametrus gaunama
visa eilė privalumų, todėl labai rekomenduojama juos naudoti.
3. Galbūt kils klausimas: kodėl kolekcijų parametrui buvo nurodyta **_Integer_** tipo klasė,
o ne tiesiog **_int_** tipas? Atsakymas yra paslėptas Java kalbos konstrukcijoje: **_int_**
tipas yra primityvus (skaliarinis, ne objektinis) tipas, todėl šio tipo reikšmėmis neįmanoma manipuliuoti
kaip pilnaverčiais objektais. Tuo tarpu **_Integer_** tipas yra pilnavertė klasė ir jos
pagrindu sukurtais egzemplioriais galima manipuliuoti kaip objektais. Visas standartinių
kolekcijų bibliotekos mechanizmas yra paremtas darbu su atskirais objektais, todėl
paprasto **_int_** negalima patalpinti į kolekciją, o **_Integer_** galima.
4. Tiesa, skaitant toliau programos tekstą, akivaizdžiai matyti, kaip į kolekciją yra talpinami
**_int_** tipo konstantos, pvz. sakinyje **l1.add(10);**. Kolekcija kaip ir skirta saugoti
**_Integer_** tipo reikšmes - kodėl kompiliatorius šioje vietoje nediagnozuoja klaidos,
o sukompiliuota programa sėkmingai veikia? Šioje vietoje suveikia speciali Java programavimo
kalbos savybė: Java programos kompiliatorius žino, kad **_Integer_** klasė yra ypatinga
(kaip ypatinga yra ir pvz. **_String_** klasė) ir moka automatiškai paversti į ir iš **_int_** tipo.
Šis automatinio vertimo mechanizmas vadinamas "autoboxing and unboxing" ir veikia tik su
tam tikromis klasėmis, pagrindinių tipų "antrininkėmis", žr. <https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html>.
5. Sąrašo elementai yra atspausdinami pasinaudojant kolekcijos parūpinama (standartine) funkcija
**_toString()_**. Jeigu kolekcijos rezultatus reikia atspausdinti kitaip, reikia atitinkamą
programos kodą pasirašyti pačiam.

Kaip kolekcijos rezultatų peržiūros ir spausdinimo pavyzdį panagrinėkime šią funkcija:
```java
  static void printAllSeparated(List<Integer> list, String sep) {
    boolean pirmas = true;
    for(Integer elementas: list) { // Šiame cikle peržiūrėsime visus sąrašo "list" turimus elementus
      if (pirmas) // Jeigu tai pirmas elementas
        pirmas = false; // skirtuko nespausdinsime
      else
        System.out.print(sep); // jeigu tai nebe pirmas elementas - spausdiname skirtuką tarp elementų
      System.out.print(elementas); // atspausdiname elementą
    }
    System.out.println(); // užbaigiame eilutę.
  }
```
Kaip matyti, pati funkcija nėra labai sudėtinga. Vienintelis dalykas kuris joje gali
atrodyti neįprastai, tai **_for_** ciklas. Čia naudojamas taip vadinama **_for-each_** ciklo
variacija, kurią beja galima pritaikyti ne tik kolekcijoms, bet ir masyvams,
žr. <http://docs.oracle.com/javase/1.5.0/docs/guide/language/foreach.html>. Tai tikrai
daug patogiau, negu pačiam apsirašinėti visus ciklo kintamuosius.

Užduotis
--------
1. Patobulink aukščiau parašytą programą, kad ji vietoje eilutės, atspausdintos standartiniu būdu,
atspausdintų eilutę kolekcijos reikšmių atskirtų per kabliataškį ir tarpą, t.y. taip:  
  ```
    LinkedList Elements
      10; 2; 30
  ```
2. Naudodamas kolekciją atspausdink [ankstesnės užduoties](../step003/task.md) metu surastų pirminių daugyklių sąrašą tokiu pavidalu (pvz. kai n==6):  
  ```
  6! = 2 * 3 * 2 * 2 * 5 * 2 * 3
  ```
Atspausdinamų dauginamųjų tvarka nėra svarbi, svarbu, kad būtų atspausdinta tiek kiek jų yra ir kokie yra.

Programavimo užduotis
=====================
Parašyti Javą programą pagal [olimpiadinę užduotį](task.md).

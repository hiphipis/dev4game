
Programavimo mokymosi užduotis
========================
Tikslas - pagerinti sugebėjimus tinkamai (tvarkingai) organizuoti parašytą programinį kodą. 

Teorija
-------
Java programavimo kalboje programinis kodas yra organizuojamas naudojant du pagrindinius mechanizmus:

1. Išskiriant svarbias klases į atskirus failus.
2. Apjungiant susijusias klases į klasių paketus.

Reikia pastebėti, kad Java kalba viename faile leidžia aprašyti tik vieną *public*, t.y. matomą kitoms 
klasėms, klasę. Ir iš kitos pusės reikalauja, kad kiekviena *public* klasė būtų aprašyta atskirame
faile. Tačiau be įprastų *public* rūšies klasių egzistuoja kitokių rūšių klasės, kurias galima
aprašinėti tame pačiame faile. Šiame tekste kitokių rūšių klasių nenagrinėsime ir apsiribosime
tik *public* rūšies klasėmis.

Rašant dideles programas tokių *public* rūšies klasių būna suskaičiuojama tūkstančiais.
Kad būtų lengviau susigaudyti ir prižiūrėti tokį didelį klasių kiekį, klasės paprastai
yra apjungiamos į klasių paketus, pagal atliekamas funkcijas, pvz.:

1. Klasių paketas skirtas duomenų įrašymui į (nuskaitymui iš) duomenų bazę.
2. Ataskaitų modulio klasių paketas.
3. Vartototojo sąsają realizuojančios klasės.
4. **interface** rūšies klasės, aprašančios programuotojišką sąsają (API) į programą.
5. **class** rūšies klasės, įgyvendinančios programuotojišką sąsają (API) į programą.

Pateikti paketų pavyzdžiai yra skirti tik iliustruoti ir tikrai neišsemia visos kriterijų įvairovės
kuri naudojama grupuojant klases į paketus.

Klasių paketai sudaromi tokiu būdu:

1. Paketui suteikiamas pavadinimas. Pavadinimą sudaro vienas arba keli žodžiai, kurie įprastai rašomi
iš mažosios raidės, atskirti tašku. Pvz.:
  - myapp
  - myapp.database
  - myapp.reports
  - myapp.api
2. Kiekviena paketo pavadinimo dalis atspindi katalogą. T.y., jeigu turime klasę *MyClass*, kuri priklauso
paketui *myapp.database*, tai failas *MyClass.java* turės būti patalpintas kataloge *myapp/database*
3. Paketo, kuriam priskiriama klasė, pavadinimas įrašomas Java klasės failo pradžioje. Pvz.:
  ```java
  package myapp.database;

  public class MyClass {
  }
  ```  
4. Kai rašant programą norima pasinaudoti kita klase ar jos metodais reikia importuoti norimos
klasės apibrėžimą. Pvz.: 
  ```java
  package myapp;
  
  import myapp.database.MyClass;

  public class MyApp {
  }
  ```
5. Importuoti galima vieną pasirinktą klasę, kaip parodyta pavyzdyje aukščiau, arba visas paketo klases,
vietoje klasės nurodant tiesiog žvaigždutės simbolį:
  ```java
  import java.util.*; // Importuojame visas paketo java.util klases
  import myapp.database.MyClass; // Importajame vienintelę klasę MyClass iš paketo myapp.database
  ```
6. Norint panaudoti klases, kurios priklauso tam pačiam paketui, jų importuoti nereikia.

Ne visada tikslus klasių grupavimas į paketus būna žinomas prieš pradedant programuoti.
Todėl šiuolaikiniai įrankiai, kaip pvz. Eclipse IDE, turi pagalbines priemones, kurios leidžia
patogiai pergrupuoti jau sukurtas klases į paketus. Tam naudojami kontekstinio meniu "Refactor" submeniu
komandos:

- "Move" iškviečiama klavišais < Alt+Shift+V > leidžia perkelti klasės __failą__ į bet kurį paketą.
- "Rename" iškviečiama klavišais < Alt+Shift+R > leidžia pervardinti klasės __failą ir klasę__.

Užduotys
--------
Šios dalies praktinė užduotis bus suijusi su visomis iki tol rašytomis programomis - jas reikės
suorganizuoti į paketus taip, kad atrodytų kaip vieno didesnio projekto dalys:

1. Kiekvienai pamokai sukurk po atitinkamą paketą *dev4game.stage01.step001" ir t.t.
2. Perkelk į paketą visas su atitinkama pamoka susijusias programas.
3. Pervardink programas taip, kad jų pavadinimai būtų užrašyti taip vadinamuoju *CamelCase* - kai
atskiri žodžiai iš kurių susideda klasės pavadinimas rašomi iš didžiosios raidės.
4. Pervardindamas programas taip pat pridėk prie pavadinimo žodį *Readme* jeigu programėlė
buvo suskurta pagal sąlygas iš readme.md failo ir žodį *Task* jeigu programėlė buvo sukurta
pagal sąlygas iš task.md failo, pvz.: "ReadmeKolekcijaDeque.java".
5. Šią pamoką atitinkančiame pakete parašyk programą, kuri iš eilės įvykdytų visas programėles, 
parašytas ankstesnėse pamokose. Prieš prieš vykdydama kiekvieną programėlę, programa
turi atspausdinti trumpą informaciją, kokia programėlė bus vykdoma ir, jeigu reikia, paaiškinti
kokius veiksmus vartotojas turės atlikti programėlės veikimo metu.

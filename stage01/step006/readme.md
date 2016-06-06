
Programavimo mokymosi užduotis
========================
Tikslas - pagilinti kolekcijų naudojimo žinias.

Teorija
-------
Ankstesnėse užduotyse nagrinėta **List** klasė skirta dirbti su objektų sąrašais
ir iš esmės leidžia su sąrašu atlikti tik labai paprastus veiksmus: pridėti arba
išmesti sąrašo elementą, surasti objektą arba peržiūrėti visus elementus iš eilės.
Programuojant dažnai prireikia sudėtingesnių funkcijų, todėl stadartinėje Java programavimo
kalbos kolekcijų bibliotekoje yra daugiau klasių (žr.:
<http://www.tutorialspoint.com/java/java_collections.htm> ir
<https://docs.oracle.com/javase/tutorial/collections/>). Paminėsiu pagrindines:

1. **List** - jau nagrinėti paprastieji sąrašai.
2. **Set** - aibės kolekcija, pasižyminti tuo, kad joje vienos reikšmės objektas
gali būti įdėtas tik vieną kartą. Kitaip tariant kiek vienodų ar skirtingų reikšmių
elementų bedėtume į **Set** rezultate jame bus išsaugotos tik unikalios reikšmės.
3. **SortedSet** - aibės kolekcija, pasižyminti tomios pačiomis savybėmis kaip paprasta
**Set** klasė, tik turinti tą papildomą savybę, jog išsaugotus elementus surūšiuoja
didėjimo kryptimi.
4. **Map** - verčiant pažodžiui skambėtų kaip "žemėlapio" kolekcija. Kuom gi ypatingas
paprastas žemėlapis? O gi tuom, kad žinant koordinates gali pasakyti koks objektas pagal
tas koordinates yra pavaizduotas žemėlapyje. Panašiai ir **Map** klasė leidžia
"surišti" du objektus: vienas - dar vadinamas raktu (angl.: _key_) - atlieka koordinačių
vaidmenį; kitas - dar vadinamas reikšme (angl.: _value_) - atlieka objekto vaidmenį.
Rezultate į **Map** yra dedamas ne vienas objektas, o jų pora: _(raktas, reikšmė)_.
Ir norint surasti reikšmės objektą užtenka žinoti raktą, su kuriuo jis įdėtas į **Map**.
Viskuom kitu (indeksavimu, greita paieška) pasirūpina kolekcijos klasė.
5. **SortedMap** - analogiška **Map** kolekcijai, tik užtikrina, jog poros _(raktas, reikšmė)_
kolekcijoje išsaugomos raktų didėjimo tvarka.
6. **Queue** - objektų eilę atvaizduojanti kolekcija. Savo funkcionalumu panaši į
**List** klasę, tačiau turinti papildomus metodus darbui su objektais. Dažniausiai
naudojama, kai reikia surikiuoti į eilutę objektus ir juos iš eilės apdoroti.
Toks metodas dar vadinamas FIFO (First In First Out) eile - pirmas patekęs į eilę
objektas pirmas ir išimamas iš eilės apdorojimui.
7. **Deque** - dar viena objektų eilėms atvaizduoti skirta kolekcija. Nuo **Queue**
skiriasi tuo, kad turi metodus, kurie leidžia manipuliuoti objektais tiek eilės
pradžioje tiek gale. Todėl **Deque** pagalba galima nesunkiai realizuoti objektų
apdorojimą tiek aukščiau minėtu FIFO metodu, tiek steko arba LIFO (Last In First Out)
metodu, kai paskutinis įdėtas elementas išimamas pirmas.

Aukščiau paminėtos klasės yra **interface* rūšies klasės. Klases, kurios
įgyvendina šias kolekcijas, susirasti oficialioje dokumentacijoje palieku skaitytojui :)

Užduotys
--------
Naudojant kolekcijas parašyti šias programėles:

1. Programėlė, kuri skaito sveikus teigiamus skaičius ir įvedus nulį parašo visus
skirtingus skaičius didėjimo tvarka (**SortedSet<Integer>**).
2. Programėlė, kuri prašo įvesti šachmatų figūras lentoje. Įvedama paeiliui šachmatų
lentos langelio pavadinimas ir figūros pavadinimas. Įvedimo pabaiga žymima nurodant
langelio pavadinimą 'gg'. Pabaigus įvedimą programa atspausdina visas figūras
šachmatų lentoje (naudojant paprastą kolekcijos spausdinimą), pvz.:
  ```
  langelis: e2
  figūra: pėstininkas
  langelis: e8
  figūra: valdovė
  langelis: gg

  Šachmatų lenta:
    {e2=pėstininkas, e8=valdovė}
  ```
3. Patobulink [ankstesnę užduotį](../step005/readme.md) apie atvirkštinį teksto
spausdinimą ir pritaikyk joje vietoje **List** klasės **Deque**.


Projekto užduotis
========================
Mūsų žaidimų lenta jau yra pakankamai funkcionali, kad galėtume pradėti ją naudoti - laikas apsirašyti žaidimo figūras.
Pradėkime nuo to kokias šachmatų figūrų klases galėtume apsirašyti. Natūralu būtų apsirašyti kiekvienai figūros
rūšiai po vieną klasę, nes kiekviena figūra turi savo naudojimo žaidime ypatybes. Turime tokias figūras: 

- Karalius
- Valdovė
- Rikis
- Žirgas
- Bokštas
- Pėstininkas

Atitinkamai matyt turėtume apsirašyti tokias klases:

```java
// NB: kiekviena klasė turi būti aprašyta atskirama *.java tipo faile

/** Klasė aprašanti karaliaus figūrą
*/
public class ChessKing {...}

/** Klasė aprašanti valdovės figūrą
*/
public class ChessQueen {...}

/** Klasė aprašanti rikio figūrą
*/
public class ChessBishop {...}

/** Klasė aprašanti žirgo figūrą
*/
public class ChessKnight {...}

/** Klasė aprašanti bokšto figūrą
*/
public class ChessRook {...}

/** Klasė aprašanti pėstininko figūrą
*/
public class ChessPawn {...}

```

Tačiau kai apsirašysime šias šešias klases iškils klausimas: o kaip jas įdėti į žaidimų lentos langelį?
Žinoma, būtų galima į klasę _BoardCell_ įdėti po metodą kiekvienos figūros pastatymui ant to laukelio, pvz.:

```java
package dev4game.stage02.chess.board;

class BoardCell {
    // Aiškumo dėlei esamos savybės ir metodai praleisti
    // <....>

    public void setFigureKing(ChessKing fig) {...};

    public void setFigureQueen(ChessQueen fig) {...};

    public void setFigureBishop(ChessBishop fig) {...};

    // ir t.t. visoms kitoms figūroms
}    
```

Tačiau kas atsitiks, jeigu vėliau norėsime panaudoti žaidimų lentą kitam, ne šachmatų, žaidimui?
Teks tokiu pat principu pridėti ir kito žaidimo figūrų pastatymo metodus. Taip gausime, kad žaidimų
lentos langelis turi žinoti (būti susijes su) apie visas įmanomas visų žaidimų figūras. Tai tikrai
būtų labai nepatogu ir nelogiška, nes juk net realiame gyvenime žaidimų lentai jokio skirtumo,
ką mes ant jos padėjome: žirgą, šaškę ar tiesiog paprastą akmenėlį.

Todėl turėtų būti geresnis būdas pastatyti šachmatų figūrą į langelį. Mes pasinaudosime objektinio 
programavimo ypatybe vadinama _polimorfizmu_: to paties objekto sugebėjimu prisistatyti įvairių rūšių objektais.
Mūsų atveju idėja skambėtų taip: apibrėžkime tipą kuris būtų visų figūrų apibendrinimas ir išmokykime konkrečių
figūrų klases pristatyti save kaip apibendrintą figūros tipą. Tam mes panaudosime anksčiau paminėtas
_interface_ rūšies klases. Šios rūšies klasės ir buvo sugalvotos tam, kad tarnautų tokiais apibendrintais
modeliais. Apsirašykime apbendrintos figūros klasę: 

```java
package dev4game.stage02.chess.game;

/** Apibendrinta žaidimo figūra
*/
public interface GameFigure {
    /** Pasakykime figūrai kokiame laukelyje ji pastatyta
    * @param langelio kuriame stovi figūra objektas
    */
    public void setCell(BoardCell cell);

    /** Sužinokime kokiame laukelyje figūrai pastatyta
    * @returns langelio kuriame stovi figūra objektas
    */
    public BoardCell getCell();
}
```

Tiesą sakant - tai ir yra pilnas šios klasės aprašymas. Viso labo tik metodų skirtų susieti figūrą su langeliu pavadinimai.
Tai, kad nėra metodų kūnų yra _interface_ rūšies klasių ypatybė: jos skirtos nustatyti tik kokie metodai turi būti
įgyvendinti norint save pateikti šiuo apibendrintu tipu, tačiau patį metodo įgyvendinimą palieka tai konkrečiai
klasei, kurios objektas norės prisistatyti šiuo apibendrintu _interface'u_.

Turint tokį apibendrintą tipą laukelio klasėje užteks parašyti viso labo tik du metodus, skirtus dirbti su žaidimo 
figūromis - _setter'į_ ir _getter'į_:

```java
package dev4game.stage02.chess.board;

import dev4game.stage02.chess.game;

public class BoardCell {
    // Aiškumo dėlei esamos savybės ir metodai praleisti
    // <....>

    public void setFigure(GameFigure fig) {...};

    public GameFigure getFigure() {...};
}    
```

Tokiu būdu laukelio klasei visiškai nesvarbu kokią figūrą mes ant jos pastatysime. Tau belieka į laukelio klasę
įtraukti reikalingas savybes figūrai išsaugoti, bei parašyti metodus ir _JavaDoc_  stiliaus dokumentaciją kiekvienam metodui. 

Į lentos langelį kaip ir mokame pastatyti figūrą, bet kaip pvz. žirgo klasė turėtų prisistatyti apibendrinta žaidimo figūrą?
Tam reikia pasakyti, kad žirgo klasė įgyvendina visus metodus aprašytus apibendrintame _interface'e_:

```java
package dev4game.stage02.chess.game;

/** Klasė aprašanti žirgo figūrą
*/
public class ChessKnight implements GameFigure {

    /** Pasakykime figūrai kokiame laukelyje ji pastatyta
    * @param langelio kuriame stovi figūra objektas
    */
    public void setCell(BoardCell cell) {
        ...
    };

    /** Sužinokime kokiame laukelyje figūrai pastatyta
    * @returns langelio kuriame stovi figūra objektas
    */
    public BoardCell getCell() {
        ...
    };
}

```

Žodis __implements__ po klasės pavadinimo yra raktinis žodis, kuris pasako, jog klasė įgyvendina toliau išvardintų _interface'ų_
metodus. Mūsų atveju yra _ChessKnight_ igyvendina vienintelio _GameFigure_ metodus, tačiau taikomosiose programose neretai
pasitaiko, kad viena klasė įgyvendina keletos _interface'ų_ metodus. Pastaruoju atveju visų įgyvendinamų _interface'ų_ pavadinimai
surašomi per kablelį, pvz.:

```java
public class MuchPolymorficClass implements Contract1Interface, AnotherContractInterface, YetAnotherInterface {...}
``` 

Reikia pastebėti, kad jeigu klasė deklaruoja, jog įgyvendina apibendrintą _interface'ą_, tai ji privalo įgyvendinti visus jame deklaruotus metodus.
Priešingu atveju Java kalbos kompiliatorius praneš apie klaidas.

Uždaviniai
----------

1. Patobulinti _BoardCell_ klasę taip, kad ji mokėtų priimti apibendrintą žaidimo figūrą. Jeigu vietoje figūros objekto pateikiama _null_ reikšmė tai traktuojama, 
kad nuo langelio nuimama figūra ir jis lieka tuščias. 
2. Patobulinti _BoardCell_ metodą _toString_ taip, kad grąžintų ir langelio, ir joje pastatytos figūros informaciją tokioje formoje
    - kai langelyje pastatyta figūra, pvz. E2 pastatytas baltas pėstininkas: 

        ```
        { n: E2; c: w; f: { n:ChessPawn; c:w; }; }
        ```

    - kai langelyje nėra pastatytos figūros: 
        ```
        { n: E2; c: w; }
        ```

3. Parašyti pėstininko, žirgo ir valdovės figūrų klases. Figūros turi mokėti:
    - pasakyti kokiame langelyje stovi (_null_ reikšmė traktuojama, kad figūra nuimta nuo lentos)
    - grąžinti savo savybes (rūšį, spalvą) metodo _toString_ pagalbą kaip simbolinę eilutę tokioje formoje: 

        ```
        { n:ChessPawn; c:w; }
        ```
4. Parašyti programėlę _Test03Figure_ kurioje sukurti 4x4 žaidimų lentą (A1:D4), B1 pastatyti baltą žirgą, B2 pastatyti juodą pėstininką ir C3 pastatyti baltą valdovę.
Atspausdinti visą žaidimų lentą. 

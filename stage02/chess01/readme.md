
Projekto užduotis
========================
Programavimas gali būti labai įdomus bei smagus užsiėmimas, todėl didelė dalis programuotoju mėgaujasi savo darbu.
Nepaisant šio emocinio aspekto, kurį kai kurie žmonės priima kaip "darbo kietumą" (_cool job_), programavimas
yra skirtas spręsti įvairius praktinius uždavinius. Todėl, kad būtų įdomiau toliau  mokytis programuoti, visos šios 
serijos užduotys turės vieną temą, kurią sąlyginai galima būtų pavadinti projektu: šachmatų žaidimas.

Pradėsime nuo pagrindinio šachmatų žaidimo elemento - žaidimo lentos. Žaidimo lenta, kaip žinia susideda iš langelių,
kuriems aprašyti reikia sukurti atitinkamą klasę:

```java
package dev4game.stage02.chess.board;

public class BoardCell {
    // Čia reikėtų išrašyti objekto savybes
    ...

    /** Žaidimo lentos langelio konstruktorius
    *   @param board žaidimų lentos, kuriai priklauso langelis, objektas
    *   @param column lentos stulpelio, kuriame yra langelis, pavadinimas
    *   @param row lentos eilutės, kurioje yra langelis, numeris
    *   @param color langelio spalvos kodas: 'b' arba 'w' 
    */
    public BoardCell(GameBoard board, char column, byte row, char color) {...};

    /** Metodas grąžinantis langelio pavadinimą
    *   @returns langelio pavadinimas susidedantis iš sujungto stulpelio ir eilutės nr., pvz. "E2" arba "F6"
    */
    public String getName() {...};

    @Override // Naudojant standartinį spausdinimą, spausdiname pagrindines savybes: vardą ir spalvą
    public String toString() { return "{" + getName() + ":" + getColor() + "}"; };

    /** Metodas grąžinantis žaidimų lentos, kuriai priklauso langelis, objektą 
    *   @returns žaidimo lentos objektas
    */
    public GameBoard getBoard() {...};

    /** Metodas grąžinantis langelio spalvą
    *   @returns 'b' juodiems langeliams ir 'w' baltiems
    */
    public char getColor() {...};

    /** Metodas patikrinantis ar langelis baltas
    *   @returns true jeigu spalva 'w' 
    */
    public boolean isWhite() {...};

    /** Metodas patikrinantis ar langelis juodas
    *   @returns true jeigu spalva 'b' 
    */
    public boolean isBlack() {...};
}
```  

Aukščiau pateiktoje klasėje nėra aprašytos klasės savybės ir funkcijų kūnai - jų parašymas ir yra pirmoji šio projekto užduotis.
Antroji užduotis bus sugalvoti, kaip analogiškai užpildyti šachmatų lentos klasę:

```java
package dev4game.stage02.chess.board;

/** Žaidimo lenta saugo ir valdo langelių, iš kurių ji sudaryta, objektus
*/
public class GameBoard {
    // Čia reikėtų išrašyti objekto savybes
    ...

    /** Žaidimo lentos objekto konstruktorius
    */
    public GameBoard() {...};

    /** Metodas pridėti naują langelį į lentą
    *   @param lentos langelio objektas
    */
    public void addCell(BoardCell cell) {...};

    /** Metodas grąžinantis langelio objektą pagal stulpelio pavadinimą ir eilutės numerį
    *   @param column lentos stulpelio, kuriame yra langelis, pavadinimas
    *   @param row lentos eilutės, kurioje yra langelis, numeris
    *   @returns laukelio objektas
    */
    public BoardCell getCell(char column, byte row) {...};

    /** Metodas grąžinantis langelio objektą pagal jo pavadinimą
    *   @param langelio pavadinimas susidedantis iš sujungto stulpelio ir eilutės nr., pvz. "E2" arba "F6"
    *   @returns laukelio objektas
    */
    public BoardCell getCell(String name) {...};

    /** Metodas grąžinantis visus langelius lentoje
    *   @returns lentos langelių kolekcija 
    */
    public List<BoardCell> getCells() {...};
}
```  

Ir trečioji užduotis bus pakete _dev4game.stage02.chess.test_ parašyti programėlę _Test01Board_, kuri sukurtų 
žaidimo lentos objektą ir jį užpildytų langeliais taip, kad rezultate gautusi maža 4x4 žaidimo lenta su langeliais A1..D4.
Programėlė veikimo pabaigoje turėtų atspausdint visą celių kolekciją gautą iš metodo _getCells()_.

Hint: vieną objektą galima įdėti į kelias skirtingas kolekcijas ir/arba masyvus tuo pačiu metu, kad vėliau būtų galima
pasinaudoti ta kolekcija ar masyvu, kuri (-is) patogesnė kažkokiam veiksmui atlikti.

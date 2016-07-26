Projekto užduotis
========================
Kadangi jau turime figūras ir mokame jas pastatyti ant žaidimų lentos langelio, pats laikas būtų išmokyti jas vaikščioti
po žaidimų lentą. Pradžioje apsirašykime visus teoriškai įmanomus kiekvienos figūros ėjimus. Kaip būtų patogiausia tai padaryti?
Prisiminkime, kad turime apsiraše klasę _Consts_, kurioje surašytos visos įmanomos judėjimo kryptys.
Tačiau vien tik to neužtenka, nes kai kurios figūros gali judėti ne per vieną langelį (pvz. valdovė), o
kitos apskritai šokinėti zigzagais (žirgas). Pavyzdžiui žirgo ėjimus galima būtų aprašyti žirgo klasėje taip:

```java
    static final int movements[][] = {
        {Consts.N, Consts.N, Consts.E},
        {Consts.N, Consts.N, Consts.W},
        {Consts.S, Consts.S, Consts.E},
        {Consts.S, Consts.S, Consts.W},
        {Consts.N, Consts.E, Consts.E},
        {Consts.N, Consts.W, Consts.W},
        {Consts.S, Consts.E, Consts.E},
        {Consts.S, Consts.W, Consts.W}
    }
```

Čia mes aprašome statinę klasės savybę, kurioje nurodome visas galimas __teorines__ figūros judėjimo kryptis.
Kadangi savybė yra statinė, tai ji bus bendra visiems tos klasės objektams ir kuriant objektus jos nereikės atskirai inicializuoti.
Tačiau skirtingos klasės (pėstininko, žirgo, valdovės, etc.) turės savo individualų galimų ėjimų sąrašą.
Ir čia prisiminkime, kad žaidimų lentoje mes operuojame apibendrinta _GameFigure_ klase. Kaip padaryti, kad gave ant
langelio stovinčią žaidimo figūrą galėtume sužinoti, kaip ji gali judėti? Sprendimas paprastas - į apibendrintą klasę
įtraukime atitinkamą metodą:

```java
    /** Sužinokime visus teoriškai įmanomus figūros ėjimus
    * @returns sąrašas teoriškai įmanomų ėjimų
    */
    public int[][] getAllMovements();
```

Ir po atitinkamą metodą parašykime konkrečių figūrų klasėse.

Taigi turime kur __teoriškai__ figūros gali judėti, bet ne visi ėjimai praktikoje galimi. Pavyzdžiui figūros negali iškeliauti
už žaidimų lentos ribų; dauguma figūrų gali judėti tik tiek kiek joms netrukdo kitos figūros, tačiau žirgas gali šokinėti virš 
langeliuose stovinčių figūrų ir pan. Kažkas turi nuspręsti, į kuriuos langelius figūra gali šokti sekančiu ėjimu.
Tas žinias atitinkamų metodų ir savybių pavidalu būtų galima įdėti į konkrečias figūrų klases. Bet vėlgi - kaip naudojamos 
figūros priklauso nuo žaidimo, kurį žaidžiame, taisyklių. Todėl būtų visai logiška sukurti klasę, kuri atspindėtų patį
žaidimą ir jo taisykles:

```java
package dev4game.stage02.chess.game;

/** Klasė aprašanti šachmatų žaidimą
*/
public class ChessGame {
    // Tarp klasės savybių turėtų būti žaidimo lenta ir ant jos stovinčios figūros 
    // <....>

    /** Metodas grąžinantis žaidimų lentos, kurioje žaidžiamas žaidimas, objektą 
    *   @returns žaidimo lentos objektas
    */
    public GameBoard getBoard() {
        ...
    };

    /** Metodas ant žaidimo lentos pastatantis pateiktą figūrą
    *   @param laukelio ant kurio pastatoma figūra pavadinimas
    *   @param žaidimo figūros objektas
    */
    public void addFigure(String cellName, GameFigure figure) {
        ...
    }
    
    /** Metodas grąžinantis visas žaidime dalyvaujančias figūras
    * @returns visų žaidime dalyvaujančių figūrų sąrašas 
    */
    public List<GameFigure> getFigures() {
        ...
    };
    
    /** Pasakykime į kokius laukelius, remiantis žaidimo taisyklėmis, gali judėti figūra
    * @param žaidimo figūrą, kuria norime pajudinti
    * @returns langelių, į kuriuos galima perkelti figūrą sąrašas 
    */
    public List<BoardCell> getPossibleMoves(GameFigure figure) {
        ...
    };
    
    /** Perkelkime figūrą iš esamo laukelio į nurodytą laukelį
    * @param žaidimo figūrą, kuria norime pajudinti
    * @param žaidimo figūrą, kuria norime pajudinti
    */
    public void moveFigureTo(GameFigure figure, BordCell cell) {
        ...
    };

}
```

Įgyvendinus šios klasės metodus, būtų galima parašyti štai tokį primityvų žaidimą vykdančią funkciją - judinti pirmą 
galinčią judėti žaidimo figūrą pirma galima judėjimo kryptimi :

```java
    public void runGame(ChessGame game) {
        while (true) {
            boolean moved = false;
            List<GameFigure> figures = game.getFigures();
            if (figures.size() == 0) // Žaidime nėra figūrų su kuriomis galima žaisti
                break;

            for (GameFigure figure: figures) {
                List<BoardCell> destCells = game.getPossibleMoves(figure);
                if (destCells.size() == 0)
                    continue;
                
                game.moveFigureTo(figure, destCells.get(0));
                moved = true;
                break;
            }

            if (!moved) // nebėra galimų ėjimų - baigiam funkciją
                return;
        }
    }
```

Uždaviniai
----------

1. Patobulinti apibendrintą, pėstininko, žirgo ir valdovės figūrų klases, kad jos mokėtų pasakyti galimas judėjimo kryptis.
2. Įgyvendinti _ChessGame_ klasę pridedant reikiamas savybes ir realizuojant nurodytus metodus.
3. _ChessGame_ klasės metodas _moveFigureTo_ perkeldamas žaidimo figūrą iš vieno laukelio į kitą turi atspausdinti figūrą ir jos judėjimą, pvz.:

    ```
    { n:ChessPawn; c:w; } E2 -> E4
    ```
4. Parašyti programėlę _Test04Game_, kurioje būtų sukuriamas šachmatų žaidimas su vieninteliu žirgu ir įvykdoma aukščiau parašyta žaidimo funkcija _runGame_

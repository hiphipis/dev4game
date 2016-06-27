
Projekto užduotis
========================
Tęsiame šachmatų žaidimų lentos programavimą. Kol kas mūsų turima šachmatų lenta moka tik talpinti langelius ir 
juos grąžinti - po vieną pagal vardą arba visus iš karto. Mums gi, galvojant apie veiksmų žaidime realizavimą,
reikėtų mokėti nesunkiai pasiekti šalia esantį langelį. Tam į laukelio klasę _BoardCell_ būtų patogu įtraukti
papildomus metodus.

Gal jau pastebėjai ankstesnėje užduotyje, kad metodai turi panašų vardo formatą:

- setPropertyName - vadinamasis _setter_ metodas, skirtas nustatyti savybės pavadintos _propertyName_ reikšmę
- getPropertyName - vadinamasis _getter_ metodas, skirtas gauti savybės pavadintos _propertyName_ reikšmę 
- isTested - taip pat _getter_ metodas, bet naudojamas tada kai tikrinama savybė yra _boolean_ tipo

Toks vardų užrašymas, dar žinomas kaip _JavaBean konvencija_, nėra privalomas Java programavimo kalboje, 
tačiau _de facto_ yra visuotinai priimtas ir naudojamas kaip gero programavimo stiliaus standartas.
Mes irgi toliau turėsime jo laikytis.

Jeigu paimtume žaidimų lentos langelį, tai bendriausiu atveju jį galėtume apsupti aštuoniais kaimyniniais langeliais.
Sužymėkime juos sąlyginai pasaulio kryptimis ('x' - langelis, kurio kaimynus nagrinėjame):

| | | |
|:--:|:--:|:--:|
| NW | N | NE |
| W  | x | E  |
| SW | S | SE |

Tekstiniai pavadinimai yra patogūs skaitant programos tekstą, tačiau nepatogūs užrašant veiksmus. Daug patogiau būtų
jeigu mes galėtume jais naudotis kaip skaitinėmis konstantomis. Tuo tikslu apsirašysime klasę, kurioje aprašinėsime
visas šachmatų programose naudojamas konstantas. 

```java
package dev4game.stage02.chess;

public class Consts {
    public static final int N = 0; 
    public static final int S = 1; 
    public static final int W = 2; 
    public static final int E = 3; 
    public static final int NW = 4; 
    public static final int NE = 5; 
    public static final int SW = 6; 
    public static final int SE = 7;
    public static final int MAX_DIRECTIONS = 7; 
}
```

Ši klasė kol kas nėra didelė, joje aprašytos tik devynios konstantos. Panagrinėkime ką vienos konstantos aprašyme 
reiškia visi tie raktiniai žodžiai (nagrinėkime konstantą _NW_):

- __public__ reiškia, kad konstantos aprašymas bus pasiekiamas klasėms iš kitų paketų - naudosime visur, kur tik reikės
- __static__ reiškia, kad tai ne objekto, bet klasės savybė. T.y. norint pasinaudoti šia savybe nereikia kurti 
objekto, ją galima pasiekti iškarto rašant su klasės pavadinimu _Consts.NW_.
- __final__ reiškia, kad šios savybės, po jos inicializavimo, niekas keisti nebegali. Konstantos juk tokios ir yra, tiesa?
- __int__ yra konstantos tipas
- __NW__ yra konstantos pavadinimas
- __4__ yra konstantos reikšmė

Jeigu dabar laukelio klasėje apsirašytume savybę _neighbors_ kaip 8 laukelių masyvą, tai jame, naudodami šias konstantas, galėtume 
sutalpinti visus langelio kaimynus. Tam tau reikia _BoardCell_ klasę papildyti atitinkama savybe ir šiais metodais:

```java
    /** Nustato laukelio kaimynus
    *   @param direction nurodo kuris laukelio kaimynas nustatomas. Naudoti Consts.{N,S,W,E,...} konstantas
    *   @param neighbor kaimyninė celė 
    */
    public void setNeighbor(int direction, BoardCell neighbor) {...}
    
    /** Grąžina laukelio kaimyną
    *   @param direction nurodo kuris laukelio kaimynas grąžinamas. Naudoti Consts.{N,S,W,E,...} konstantas
    *   @returns kaimyninė celė 
    */
    public BoardCell getNeighbor(int direction) {...}
```

Tai ir yra pirmoji užduotis. Jai patikrinti testinių programėlių pakete parašyk programėlę _Test02Cell_ kurioje
sukonstruok 8x8 žaidimo lentą ir atspausdink, kokius laukelius grąžins šie metodai:

1. Ėjimas žirgu iš A1:

    ```java
        // lenta yra GameBoard tipo objektas 
        BoardCell cell2 = lenta.getCell('A1').getNeighbor(Consts.N).getNeighbor(Consts.N).getNeighbor(Consts.E);
        // atspausdinti cell2
    ``` 
2. Ėjimas rikiu iš H8:

    ```java
        // lenta yra GameBoard tipo objektas 
        BoardCell cell2 = lenta.getCell('H8').getNeighbor(Consts.SW).getNeighbor(Consts.SW).getNeighbor(Consts.SW);
        // atspausdinti cell2
    ``` 
3. Ėjimai valdove iš D4:

    ```java
        // lenta yra GameBoard tipo objektas
        for(int direction=0; direction <= Consts.MAX_DIRECTIONS; direction++) {
            BoardCell cell2 = lenta.getCell('D4').getNeighbor(direction);
            // atspausdinti cell2
        }
    ``` 

Rezultatai tuėtų būti šie laukeliai:

1. B3
2. E5
3. D5 D3 C4 E4 C5 E5 C3 E3

Tiesa, kad parašyti testinę programėlę tau reikės metodo, kuris sukonstruotu ir tarpusavyje prasmingai susietų visus laukelius.
Tokio metodo parašymas ir bus tavo antroji užduotis: parašyti statinį (klasės) metodą klasėje _GameBoard_, kurį iškvietus
būtų sukonstruojama ir grąžinama žaidimų lenta. Metodo iškvietimas turėtų atrodyti taip:

```java
    String stulpeliai = "ABCDEFGH";
    int    eiluciu = 8;
    GameBoard lenta = GameBoard.createBoard(stulpeliai, eiluciu);
```  

Šį metodą turėtum panaudoti, kai rašysi testinę programėlę pirmąjai užduočiai.

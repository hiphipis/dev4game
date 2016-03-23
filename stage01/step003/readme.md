
Programavimo mokymosi užduotis
========================
Tikslas - išmokti naudoti funkcijas.

Teorija
-------
Programos rašymo metu daugelis veiksmų suprogramuojama kviečiant įvairias funkcijas.
Kai kada funkcijos rezultatui suskaičiuoti yra patogu iškviesti tą pačią funkciją su šiek tiek
pakeistais parametrais ir jos rezultatą panaudoti galutiniam funkcijos rezultato suskaičiavimui.
Pavyzdžiui, norint suskaičiuoti n-tąjį aritmetinės progresijos narį, galima pasinaudoti tokia
funkcija:

```java
int ntasisArPrgNarys(int pirmasisNarys, int d, int n) {		// Skaičiuojame n-ąjį aritmetinės progresijos narį
	if ( n > 1 ) 											// Pradedant nuo antrojo, kiekvieną aritmetinė sprogresijos narį
		return ntasisArPrgNarys(pirmasisNarys, d, n-1) + d;	//    galima suskaičiuoti prie ankstesnio nario pridedant progresijos skirtumą d.
	else if ( n == 1 )										// Pirmasis narys
		return pirmasisNarys;								//    visada grąžinamas toks koks yra.
	else													// Visais kitais atvejais
		return 0;											//    grąžinamas 0.
}
```

Funkcijos iškvietimas iš tos pačios funkcijos yra vadinamas rekursija.
Rekursijos būdu dažniausiai galima sudėtingus ciklus, o kartais gauti ir paprastesnį programos kodą.
Daugiau pasiskaitymui: <https://github.com/linasp/leidinys-9-10-kl/blob/master/source/rekursija.rst>

Užduotys
--------
1. Be kompiuterio pagalbos išanalizuok ir paaiškink (užrašyk komentarus), ką atlieka šios funkcijos:
	```java
		String f(String s) {		// ka gražins toks funkcijos iškvietimas: f("sedek"); ?
			if (s.length() > 1)
				return g( s.substring(1) ) + s.charAt(0);
			else if (s.length() == 0)
				return "";
			else
				return s.charAt(0);
		}
		
		void g(int[] m, int ix) {	// ką pagamins toks funkcijos iškvietimas: g( new int[] {1, 2, 4, 4}, 1 ); ?
			if (ix < m.length) {
				int v = m[x];
				g(m, ix+1);
				m[ m.length - ix - 1 ] = v;
			}
		}
	```
2. Naudodamas rekursijos metodu parašyk funkciją n-tajam [ankstesnės užduoties](../step002/task.md) sekos nariui surasti.

Programavimo užduotis
=====================
Parašyti Javą programą pagal [olimpiadinę užduotį](task.md).

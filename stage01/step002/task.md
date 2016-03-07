Užduotis
========
Originali užduotis iš http://www.lmio.mii.vu.lt/?act=getFile&id=204

Lietuvos mokiniu informatikos olimpiada
Respublikinis etapas (1) • 1990-1991 m. • VIII–XII kl. seka-01

Nulių ir vienetų seka
---------------------

Nulių ir vienetų seka generuojama šitaip. Rašomas nulis – tai pirmasis sekos narys. Po to
prie sekos prirašoma (pakartojama) jau esanti invertuota seka (t. y. nuliai pakeisti vienetais,
o vienetai – nuliais). Taigi su kiekvienu žingsniu seka dvigubai pailgeja. Žemiau parodyta,
kaip formuojama seka:

```
0
0 1
0 1 1 0
0 1 1 0 1 0 0 1
0 1 1 0 1 0 0 1 1 0 0 1 0 1 1 0
```

**Užduotis.** Parašykite algoritma n-ajam sekos nariui rasti.

**Pavyzdžiai.**

|Pradiniai duomenys|Rezultatai|
|------------------|----------|
|3                 |1         |

**Ribojimai.** 1 <= n <= 30 000.


---
marp: true
theme: default
paginate: true
headingDivider: 2
header: Consultes SQL (I).
---

# La clàusula GROUP BY

![bg contain opacity:.4](images/sqlogo.png)

# La clàusula GROUP BY

Amb la clàusula **GROUP BY** podem agrupar les files pel valor de determinada columna, i les funcions d'agrupament se calcularan per a cada grup i no per a totes les files de la taula.

# La clàusula GROUP BY

<h3>Exemple</h3>

En la base de dades de cines tenim la taula **sala** amb l'estructura:

- codigo (identificador del cine)
- lletra (identificador de la sala)
- butaques (quantitat de butaques de la sala)

Suposem que volem saber quantes butaques hi ha, en total, en el cine 1. Farem:
```sql
SELECT SUM(butaques) FROM sala WHERE codigo=1;
```
I si volem saber quantes butaques hi ha en el cine 2:
```sql
SELECT SUM(butaques) FROM sala WHERE codigo=2;
```

# La clàusula GROUP BY

I així, cine per cine. Però si tenim molts cines, i volem saber quantes butaques en total hi ha en cada cine, hi ha alguna manera de fer-ho que no siga anar sumant-les un a un? Sí, utilitzant la clàusula **GROUP BY** per a que primer agrupe les sales per cine, i després sume les butaques per cada cine.
```sql
SELECT codigo, SUM(butaques) FROM sala GROUP BY codigo;
```

!!!note "Exercici 3"  

Fes una consulta que mostre els números de cine i, al costat, quantes sales té cada cine.

# La clàusula HAVING amb GROUP BY

De vegades volem fer una consulta amb **GROUP BY** però que no mostre tots els grups, sino només els grups que compleixen una condició.

!!!Warning "Compte!"
Hem de diferenciar entre una consulta que primer agafe les files que compleixen una condició i després les agrupe (la condició aniria en el WHERE abans del GROUP BY) i una consulta que després d'agrupar mostre els grups que compleixen una condició (la condició del grup anirà amb HAVING després del GROUP BY)</div>

# La clàusula HAVING amb GROUP BY

<h3>Exemple</h3>

Per exemple, recordem que la consulta
```sql
SELECT codigo, SUM(butaques) FROM sala GROUP BY codigo;
```
mostraba els números de cine, i al costat quantes butaques hi havia en total en cada cine. I si volem mostrar només els cines que tinguen més de 200 butaques en total?

# La clàusula HAVING amb GROUP BY

Seria un error fer:
```sql
SELECT codigo, SUM(butaques) WHERE butaques > 200 FROM sala GROUP BY codigo;
```
perquè com la condició està en el **WHERE**, per tant només agafará les sales que tinguen més de 200 butaques. Nosaltres no volem això, volem saber quantes butaques tenen tots els cines, i **després** mostrar només els cines que tinguen més de 200 butaques **entre totes les sales**. Lo correcte és:
```sql
SELECT codigo, SUM(butaques) FROM sala GROUP BY codigo HAVING SUM(butaques)>200;
```

!!!note "Exercici 4"  

Fes una consulta que mostre els números de cine i, al costat, quantes sales té cada cine però que no mostre els cines que tinguen només una sala. 
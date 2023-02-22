---
marp: true
theme: default
paginate: true
headingDivider: 2
header: Consultes SQL (I).
---

# Funcions d'agrupament

![bg contain opacity:.4](images/sqlogo.png)

# Funcions d'agrupament

Ja sabem com fer, per exemple, un llistat de lo que cobren els empleats. Amb
```sql
SELECT souEmp FROM empleats;
```
mostraríem el sou de tots els empleats, i amb
```sql
SELECT DISTINCT souEmp FROM empleats;
```
fem que cada sou, encara que diferents empleats cobren el mateix, només aparega una vegada.

# Funcions d'agrupament

I com fer, per exemple, que ens mostre el sou major de tots? I el més baixet? I el sou mig de tots els empleats?

Per fer eixe tipus de càlculs que no afecten a una fila sino a vàries files, però que han de tornar un valor únic (no un per fila), hem d'utilitzar les **funcions d'agrupament**.

# Funcions d'agrupament

Les principals funcions d'agrupament són:

<table><thead><th>FUNCIÓ</th><th>Utilitat</th></thead>
<tr><td>MAX</td><td>Torna el màxim de la columna o expressió indicada</td></tr>
<tr>
<tr><td>MIN</td><td>Torna el mínim de la columna o expressió indicada</td></tr>
<tr><td>SUM</td><td>Torna la suma total de la columna o expressió indicada</td></tr>
<tr><td>AVG</td><td>Torna la mitja de la columna o expressió indicada</td></tr>
<tr><td>COUNT</td><td>Torna la quantitat de vegades que apareix el valor o expressió indicada</td></tr></table>

# Funcions d'agrupament

<h3>Exemple</h3>

Quin és el sou més alt que se paga als nostres empleats?
```sql
SELECT MAX(souEmp) FROM empleats;
```
I si volem que el mateix llistat mostre també el sou més baixet?
```sql
SELECT MAX(souEmp) AS "Sou màxim", MIN(souEmp) AS "Sou mínim" FROM empleats;
```

# Funcions d'agrupament

Podem combinar les funcions d'agrupament amb qualsevol condició. Quin és el sou més alt que se paga als pintors?
```sql
SELECT MAX(souEmp) AS "Sou màxim pintors" FROM empleats WHERE ofiEmp="Pintor";
```
Quin és el sou mig dels conserges?
```sql
SELECT AVG(souEmp) AS "Sou mig conserges" FROM empleats WHERE ofiEmp="Conserge";
```
Quants fontaners tenim en la taula d'empleats?
```sql
SELECT COUNT(*) AS "Fontaners" FROM empleats WHERE ofiEmp="Fontaner";
```

# Funcions d'agrupament

Com hem vist, si no anem a comptar res especial, només files, posem `COUNT(*)`.

De vegades sí que voldrem comptar alguna cosa específica. Per exemple, quants oficis diferents hi ha a la taula d'empleats?

Per llistar els oficis distints que hi ha a la taula fem:
```sql
SELECT DISTINCT ofiEmp FROM empleats;
```
Per comptar-los, podem fer:
```sql
SELECT COUNT(DISTINCT ofiEmp) FROM empleats;
```

# Altres funcions

![bg contain opacity:.4](images/sqlogo.png)

# Altres funcions

En SQL disposem també de moltes altres funcions que podem utilitzar en les nostres consultes. Algunes d'elles són:

<table><thead><th>FUNCIÓ</th><th>UTILITAT</th></thead>
<tr><td>ABS(x)</td><td>Torna el valor absolut d'una quantitat</td></tr>
<tr><td>CEIL(x)</td><td>Arredoneix un número per dalt</td></tr>
<tr><td>CHAR_LENGTH(x)/LENGTH(x)</td><td>Torna quans caràcters té la cadena x</td></tr>
<tr><td>CONCAT(x,y)</td><td>Concatena les cadenes x i y</td></tr>
<tr><td>CURDATE()</td><td>Torna la data actual</td></tr>
<tr><td>CURTIME()</td><td>Torna l'hora actual</td></tr>
<tr><td>DATE_ADD(data,interval)</td><td>Suma un interval a una data</td></tr>
<tr><td>DATE_FORMAT(data,format)</td><td>Li dona format a una data</td></tr>
<tr><td>DATEDIFF(data1,data2)</td><td>Torna la diferència entre dues dates</td></tr>
<tr><td>DAYNAME(data)</td><td>Torna el nom del dia de la semana d'una data</td></tr>
<tr><td>DAYOFMONTH(data)</td><td>Torna el dia del mes d'una data</td></tr>
<tr><td>DAYOFWEEK(data)</td><td>Torna el número del dia de la setmana d'una data</td></tr>
<tr><td>DAYOFYEAR(data)</td><td>Torna el número del dia de l'any d'una data</td></tr>
<tr><td>DIV(x,y)</td><td>Torna la divisió entera entre x i y</td></tr>
<tr><td>FLOOR(x)</td><td>Arredoneix un número per dalt</td></tr>
<tr><td>FORMAT(x,decimals)</td><td>Torna un número formatat al número de decimals indicat</td></tr>
<tr><td>IF(condició,valor1,valor2)</td><td>Torna un valor en funció de si la condició és verdadera o falsa</td></tr>
<tr><td>IFNULL(x,y)</td><td>Torna x si no és null, i torna y si x és null</td></tr>
<tr><td>LOWER(cadena)</td><td>Converteix la cadena a minúscules</td></tr>
<tr><td>MOD(x,y)</td><td>Calcula el resto de la divisió entre x i y</td></tr>
<tr><td>MONTH(data)</td><td>Torna el número del mes d'una data</td></tr>
<tr><td>MONTHNAME(data)</td><td>Torna el nom del mes d'una data</td></tr>
<tr><td>POW(x,y)</td><td>Torna el valor de x elevat a y</td></tr>
<tr><td>RAND()</td><td>Torna un número aleatori</td></tr>
<tr><td>REGEXP</td><td>Avalua si una cadena compleix un patró</td></tr>
<tr><td>REVERSE(cadena)</td><td>Torna la cadena al revés</td></tr>
<tr><td>SQRT(x)</td><td>Torna l'arrel quadrada de x</td></tr>
<tr><td>STRCMP(x,y)</td><td>Compara dues cadenes</td></tr>
<tr><td>SUBSTR()</td><td>Torna una part d'una cadena</td></tr>
<tr><td>TRIM(x)</td><td>Elimina els espais inicials i finals d'una cadena</td></tr>
<tr><td>UPPER(cadena)</td><td>Converteix la cadena a majúscules</td></tr>
<tr><td>WEEK(data)</td><td>Torna la setmana de la data</td></tr>
<tr><td>YEAR(data)</td><td>Torna l'any de la data</td></tr>
</table>

Hi ha moltes més funcions que podeu trobar a la documentació de MariaDB.

[Funcions SQL integrades en MariaDB](https://mariadb.com/kb/en/built-in-functions/)

# JSON i MariaDB

![bg contain opacity:.1](images/sqlogo.png)

Des de 2016 l'estándar SQL deixa guardar en les taules informació en format JSON. Per tant, també han aparegut funcions per treballar amb objectes de tipus JSON.

Pots veure les funcions de MariaDB per treballar amb informació en format JSON en el següent enllaç:

[Funcions JSON en MariaDB](https://mariadb.com/kb/en/json-functions/)

!!!note "Exercici 2"  

Si en la base de dades **cines** tenim una taula **cine** amb l'estructura:

- codigo (un id del cine)
- nombre (el nom del cine)
- ciudad (el nom de la població on està el cine)

Com podem comptar quants cines hi ha en la taula?

Com podem comptar quantes ciutats hi ha que tinguen cine?


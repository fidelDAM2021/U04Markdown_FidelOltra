---
marp: true
theme: default
paginate: true
headingDivider: 2
header: Consultes SQL (I).
---
# SQL DDL
<!-- _paginate: false -->
<!-- _header: ''-->
<!-- _footer: 'IES Jaume II el Just' -->
<style> h1 {color:blue;}
h3 {color:green;} 
table {padding:0px;margin:0px;}
th {color:white;font-weight:bold;background-color:blue;}
div.comentari
{ width:80%;margin:10px auto;border:2px solid red;
color
: green; }
</style> 

![bg contain opacity:.7](images/sqlogo.png)

# SQL DQL

Com ja sabeu, **SQL** (***structured query language***) és el llenguatge que ens permet comunicar-nos, directament o a través d'una aplicació, amb la base de dades. Com hem vist en l'anterior unitat, dins del llenguatge SQL podem trobar diferents subconjunts d'instruccions que formen subseccions de SQL. Entre elles està DQL, que integra totes les instruccions que utilitzem per realitzar consultes sobre la base de dades.

# La instrucció SELECT

La instrucció bàsica per fer consultes sobre les dades que tenim a la base de dades s'anomena **SELECT**. La seua sintaxi és:
```sql
SELECT columnes FROM taula WHERE condició;
```
La clàusula **WHERE** i la condició no són obligatoris, però si no posem cap condició se mostraran totes les files de la taula.

# SELECT: triar les columnes

No és obligat especificar les columnes que volem veure. Si posem un asterisc (*), la consulta les tornarà totes. Així, una instrucció com:
```sql
SELECT * FROM cine;
```
Ens mostrarà totes les files amb totes les columnes de cada fila de la taula **cine**.

Si tenim una taula **empleats** amb la següent estructura:
```
idEmp, nomEmp, cognomEmp, souEmp
```
Podem veure només el nom i els cognoms fent:
```sql
SELECT nomEmp,cognomEmp FROM empleats;
```

# Condicions: la clàusula WHERE

No sempre volem veure totes les files de la taula. Per a fer el filtre utilitzem la clàusula **WHERE** i una o més condicions.

Per exemple
```sql
SELECT * FROM empleats;
```
ens mostra tota la informació de tots els empleats. Mentre que
```sql
SELECT * FROM empleats WHERE souEmp > 1000;
```
mostra només els empleats que cobren més de 1000€ al mes

# Condicions: operadors de comparació

En la clàusula **WHERE** podem posar qualsevol expressió que tinga sentit i que se puga avaluar a verdader o fals. Així, podem utilitzar operadors de comparació com 

<table>
<thead><tr><th>OPERADOR</th><th>SIGNIFICAT</th><th>OPERADOR</th><th>SIGNIFICAT</th></tr></thead>
<tr><td>></td><td>Major que</td>
<td><</td><td>Menor que</td></tr>
<tr><td>>=</td><td>Major o igual que</td>
<td><=</td><td>Menor o igual que</td></tr>
<tr><td>=</td><td>Igual que</td>
<td>!=</td><td>Diferent que</td></tr>
</table>

<h3>Exemples:</h3>

```sql
...WHERE souEmp >= 1000;
...WHERE souEmp !=800;
``` 

# Condicions: operador LIKE

També tenim un operador específic de SQL que s'anomena **LIKE** i que ens permet preguntar si una columna conté un valor (no si és igual, sino si el conté).

Per exemple, si fem:

```sql
SELECT * FROM empleats WHERE nomEmp="Jose";
```
només obtindrem empleats amb el nom **Jose**. Ara bé, si fem

```sql
SELECT * FROM empleats WHERE nomEmp LIKE "%Jose%";
```
apareixeran també els empleats amb noms com "Jose Antonio", "Maria José", "José Luis", etc.

# Condicions: operador LIKE

El caràcter % fa de comodí de 0,1 o més digits. També podem utilitzar el guió baix ("_") per fer de comodí de només un digit. 

<h3>Exemple:</h3>

Per llistar tots els empleats que el seu nom comence per F:

```sql
SELECT * FROM empleats WHERE nomEmp LIKE "F%";
```
Ara no posem el % del principi, perquè si el posem ens mostrarà tots els noms que continguen la lletra "F", no només els que comencen per "F".

# Condicions: operador LIKE

<h3>Exemple:</h3>

Per buscar tots els empleats que el nom comence per S i acabe per Z i a més el cognom tinga 8 lletres, en lloc de fer
```sql
WHERE cognomEmp LIKE "F%Z"
```
que ens tornaria tots els empleats que els cognoms comencen per F i acaben en Z, hauríem de fer
```sql
WHERE cognomEmp LIKE "F______Z"
```
(amb 6 guions baixos) que ens tornarà els empleats que el seu cognom comence per F, acabe en Z i entre mig de la F i la Z tinguen exactament 6 caràcters.

# Operadors lògics

Podem utilitzar els operadors lògics per preguntar per 2 o més condicions en el mateix WHERE, o també per preguntar si no se compleix una condició. Els operadors lògics, com sabreu, són:

<table><thead><th>OPERADOR</th><th>SIGNIFICAT</th>
<tr><td>AND</td><td>I lògic. Si separem dues condicions amb **AND** s'han de complir les dues|</td></tr>
<tr><td>OR</td><td>O lògic. Si separem dues condicions amb **OR** només en que una siga certa el total ja és cert</td></tr>
<tr><td>NOT</td><td>Negació. Nega la condició que ve després</td></tr></table>

# Operadors lògics

Per exemple, volem llistar els empleats que el nom comence per "F" i que els cognoms continguen la lletra "z". 
```sql
SELECT * FROM empleats WHERE nomEmp LIKE "F%" AND cognomEmp LIKE "%z%";
```
Volem llistar els empleats que no tinguen la lletra "z" en els cognoms:
```sql
SELECT * FROM empleats WHERE cognomEmp NOT LIKE "%z%";
```

---
tags: [API]
---

<h1 id="weather-app">Weather App</h1>
<p>L’applicazione presente nella repository è una REST API in grado di fornire informazioni meteorologiche precedentemente salvate in un dataset che contiene: dati storici, attuali e previsioni future (tutte relative ad un periodo prestabilito).</p>
<h3 id="dataset">Dataset</h3>
<p>Il dataset, che contiene dati relativi alle città di Trieste, Ortona e Venezia, è costruito con due differenti modalità :</p>
<ul>
<li>dati-attuali &amp; dati-storici vengono già parsati come oggetti JSONArray tramite la rotta “/save” dell’app SpringBoot</li>
<li>previsioni-future sono raccolte dalla rispettiva  API di OpenWeather così come sono, mediante una chiamata al client Postman ( e successivamente parsate tramite l’app SpringBoot )</li>
</ul>
<h3 id="previsioni-dal-01012021-al-10012021">Previsioni dal 01/01/2021 al 10/01/2021</h3>
<ul>
<li>dati storici :	  01/01 - 05/01</li>
<li>dati attuali :	  06/01 - 10/01</li>
<li>previsioni future : 06/01 - 10/01</li>
</ul>
<h2 id="formato-dei-dati-restituiti">Formato dei dati restituiti</h2>
Metadati relativi ai dati del dataset :
<pre><code>{
"date": "2021-01-06 12:00:00",
"visibility": 7000.0,
"cityname": "Venice",
"timeUNIX": 1609934400,
"wind": {
		"speed": 2.9
	}
 }
</code></pre>
<p>Metadati relativi ai dati delle statistiche sui dati storici:</p>
<pre><code>{
"visibilityStats": {
	"visibilityMax": 10000.0,
	"visibilityMin": 300.0,
	"visibilityAverage": 7660.0,
	"visibilityVariance": 1.41424E7
	},
"speedStats": {
	"speedMax": 1.77,
	"speedMin": 0.82,
	"speedAverage": 1.456,
	"speedVariance": 0.123450400000000002
	}
}
</code></pre>
<p>Metadati relativi ai dati delle statistiche sulle previsioni future:</p>
<pre><code>{
    "attendibilità": {
        "speed": false,
        "visibility": true
    },
    "numeroGiorni": 5,
    "soglia_errore": "50.0%",
    "cityId": 3
}
</code></pre>
<p>In particolare:</p>
<ul>
<li>“<strong>date</strong>” indica la data del giorno a cui fanno riferimento i dati riportati;</li>
<li>“<strong>visibility</strong>” indica il valore numerico che esprime la visibilità relativa a quella città in quel giorno;</li>
<li>“<strong>cityname</strong>” indica la città;</li>
<li>“<strong>timeUnix</strong>” indica la data espressa in secondi a partire dal 1° gennaio 1970;</li>
<li>“<strong>speed</strong>” indica il valore numerico che esprime la velocità del vento relativa a quella città in quel giorno;</li>
</ul>
<p>Considerando invece i metadati relativi alle statistiche sui dati storici:</p>
<ul>
<li>“<strong>visibilityMin</strong>”, “<strong>visibilityMax</strong>”, “<strong>visibilityAverage</strong>” e “<strong>visibilityVariance</strong>” indicano rispettivamente il valore minimo,  massimo, la media e la varianza delle visibilità dei giorni presi in considerazione.</li>
<li>“<strong>speedMin</strong>”, “<strong>speedMax</strong>”, “<strong>speedAverage</strong>” e “<strong>speedVariance</strong>” indicano rispettivamente il valore minimo, massimo, la media e la varianza delle velocità del vento dei giorni presi in considerazione.</li>
</ul>
<p>Considerando invece i metadati relativi alle statistiche sulle previsioni future:</p>
<ul>
<li>“<strong>attendibilità</strong>” contiene la risposta sull'attendibilità delle previsioni future rispetto ai dati attuali.</li>
<li>“<strong>speed</strong>”, “<strong>visibility</strong>” sono gli attributi di cui viene valutatat l'attendibilità delle previsioni future.</li>
<li>“<strong>numeroGiorni</strong>” indica la quantità di giorni sulla quale vengono calcolate le statistiche.</li>
<li>“<strong>soglia_errore</strong>” evidenzia qual è la soglia di errore del risultato.</li>
<li>“<strong>cityId</strong>” indica il numero di rifermento della città scelta (1 per Trieste, 2 per Ortona e 3 per Venezia).</li>
</ul>
<h2 id="statistiche">Statistiche</h2>
<p>
</p><p>
Le statistiche che la REST API restituisce si distinguono in:</p>
<ul>
<li>
<p>statisticherelative ai dati storici (attraverso un file JSON vengono illustrati i valori descritti in precedenza, ovvero media, varianza, valori minimi e massimi). La città e il periodo da valutare vengono scelti dall’'utente.</p>
</li>
<li>
<p>
</p></li></ul><ul>
<li>
statistiche relative ai dati futuri (attraverso un file JSON viene mostrato all’utente se le previsioni, in base ai dati raccolti, sono state attendibili oppure no). L’utente inoltre sceglierà la soglia di errore attraverso la quale si valuterà l’attendibilità.</li>
</ul>
<h2 id="rotte-dellapplicazione">Rotte dell’applicazione</h2>
<table>
<thead>
<tr>
<th>Tipo di chiamata</th>
<th>Rotta</th>
</tr>
</thead>
<tbody>
<tr>
<td>1) <strong>GET</strong></td>
<td>/metadata/weather</td>
</tr>
<tr>
<td>2) <strong>GET</strong></td>
<td>/metadata/stats</td>
</tr>
</tr>
<tr>
<td>3) <strong>GET</strong></td>
<td>/save</td>
</tr>
<tr>
<td>4) <strong>POST</strong></td>
<td>/weather/current</td>
</tr>
<tr>
<td>5) <strong>POST</strong></td>
<td>/weather/historical</td>
</tr>
<tr>
<td>6) <strong>POST</strong></td>
<td>/weather/forecast</td>
</tr>
<tr>
<td>7) <strong>POST</strong></td>
<td>/stats/historical</td>
</tr>
<tr>
<td>8) <strong>POST</strong></td>
<td>/stats/forecast</td>
</tr>
</tbody>
</table><ol>
<li>Restituisce all’utente i metadati relativi al dataset</li>
<li>Restituisce all’utente i metadati relativi alle statistiche, sia storiche che future</li>
<li>E’ servita per salvare i dati nel dataset<br>
<em>Nota</em>: ciò che viene restituito da questa chiamata viene 		      sovrascritto nel dataset.</li>
<li>Restituisce i dati attuali</li>
<li>Restituisce i dati storici</li>
<li>Restituisce le previsioni future</li>
<li>Restituisce le statistiche fatte con i dati storici</li>
<li>Restituisce le statistiche relative alle previsioni</li>
</ol>
<h2 id="filtri">Filtri</h2>
<p>L’utente può filtrare i dati restituiti dalle chiamate scegliendo la/le città da restituire e il periodo da considerare.<br>
Per le chiamate 4, 5 e 6 il body (in formato JSON) deve essere del tipo seguente:</p>
<pre><code>{
    "primaCitta": &lt;n1&gt;,
    "ultimaCitta": &lt;n2&gt;,
    "giornoIniziale": &lt;n3&gt;,
    "giornoFinale": &lt;n4&gt;
}</code></pre>
<p>I numeri <strong>n1</strong> e <strong>n2</strong> devono essere compresi tra 1 e 3 (1 per Trieste, 2 per Ortona e 3 per Venezia), in questo modo l’utente può scegliere quali città mostrare.<br>
I numeri <strong>n3</strong> e <strong>n4</strong> invece devono essere compresi tra 1 e 5 ( giorni che vanno dal 01/01 al 05/01 per i dati storici, dal 06/01 al 10/01 per i dati attuali e dal 06/01 al 10/01 per le previsioni), così facendo l’utente può scegliere il periodo da considerare.</p>
<p><em>Nota</em>: n2 deve essere necessariamente maggiore o uguale di n1 (quest’ultimo caso se si vuole considerare una sola città), così come n4 deve essere maggiore o uguale di n3.</p>
<p>
</p><p>
Per la chiamata 7 si utilizza lo stesso body, ma in questo caso <strong>n1</strong> e <strong>n2</strong> devono essere uguali, in quanto le statistiche possono essere fatte solo per ogni singola città.</p><br>
La chiamata 8 ha il seguente body (sempre in JSON):
<pre><code>{
    "primaCitta": &lt;n1&gt;,
    "ultimaCitta": &lt;n2&gt;,
    "giornoIniziale": &lt;n3&gt;,
    "giornoFinale": &lt;n4&gt;,
    "soglia_errore": &lt;n5&gt;
}</code></pre>
<p>Valgono gli stessi criteri di scelta per n1, n2, n3 e n4.<br>
<strong>n5</strong> deve essere un numero compreso tra 0 e 100, e sta ad indicare la percentuale di soglia di errore.</p>
<h1 id="uml">UML</h1>

## Use Case Diagram

![alt text](/assets/img/USE%20CASE%20DIAGRAM.png)

## Class Diagram

![alt text](/assets/img/CLASS_DIAGRAM.png)

## Sequence Diagram

![alt text](/assets/img/SEQUENCE_DIAGRAM_1.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0MDYyNzE4NiwxNzE3ODY0OTEwXX0=
-->
## Librerie esterne
Per il funzionamento dell'applicazione importare nell'IDE le seguenti librerie: - json-simple-1.1 - junit5.</p> 
<p><em>Nota</em>: la libreria json-simple-1.1 è presente nei file della repository.</p> 

## Contributors:
- Colleluori Federico 50%
- Camplese Francesco 50%
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTYyNTg3NDA1XX0=
-->

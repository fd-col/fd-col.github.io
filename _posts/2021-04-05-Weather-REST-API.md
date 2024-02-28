---
tags: [API]
---

<p>The application in the repository is a REST API that can provide weather information previously saved in a dataset that contains: historical, current, and future forecast data (all related to a predetermined period).</p>
<h3 id="dataset">Dataset</h3>
<p>The dataset, which contains data for the cities of Trieste, Ortona and Venice, is constructed with two different :</p>
<ul>
<li>dati-attuali (current data) &amp; dati-storici (historical data) are already parsed as JSONArray objects via the route “/save” of SpringBoot app</li>
<li>previsioni-future (futures forecast) are collected from the respective OpenWeather API as is, via a call to the Postman client (and subsequently parsed via the SpringBoot app)</li>
</ul>
<h3 id="previsioni-dal-01012021-al-10012021">Forecast from 01/01/2021 to 10/01/2021</h3>
<ul>
<li>current data :	  01/01 - 05/01</li>
<li>historical data :	  06/01 - 10/01</li>
<li>future forecast: 06/01 - 10/01</li>
</ul>
<h2 id="formato-dei-dati-restituiti">Format of returned data</h2>
Metadata related to the dataset data :
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
<p>Metadata related to historical data statistics data:</p>
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
<p>Metadata related to future forecast statistics data:</p>
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
<p>In detail:</p>
<ul>
<li>“<strong>date</strong>” indicates the date of the day to which the reported data refer;</li>
<li>“<strong>visibility</strong>” indicates the numerical value expressing the visibility relative to that city on that day;</li>
<li>“<strong>cityname</strong>” indicates the city;</li>
<li>“<strong>timeUnix</strong>” indicates The date expressed in seconds as of January 1, 1970;</li>
<li>“<strong>speed</strong>” indicates the numerical value expressing the wind speed relative to that city on that day;</li>
</ul>
<p>Considering instead the metadata related to historical data statistics:</p>
<ul>
<li>“<strong>visibilityMin</strong>”, “<strong>visibilityMax</strong>”, “<strong>visibilityAverage</strong>” e “<strong>visibilityVariance</strong>” denote the minimum, maximum, mean, and variance, respectively, of the visibilities of the days considered.</li>
<li>“<strong>speedMin</strong>”, “<strong>speedMax</strong>”, “<strong>speedAverage</strong>” e “<strong>speedVariance</strong>” indicate the minimum, maximum, mean, and variance of the wind speeds of the considered days, respectively.</li>
</ul>
<p>Considering instead the metadata related to future forecast statistics:</p>
<ul>
<li>“<strong>attendibilità</strong>” Contains the answer on the reliability of future forecasts compared to current data.</li>
<li>“<strong>speed</strong>”, “<strong>visibility</strong>”Are the attributes of which the reliability of future forecasts is evaluated.</li>
<li>“<strong>numeroGiorni</strong>” indicates the amount of days over which statistics are calculated.</li>
<li>“<strong>soglia_errore</strong>” highlights what the error threshold of the result is.</li>
<li>“<strong>cityId</strong>” indicates the reference number of the chosen city (1 for Trieste, 2 for Ortona, and 3 for Venice).</li>
</ul>
<h2 id="statistiche">Statistics</h2>
<p>
</p><p>
The statistics that the REST API returns are distinguished into:</p>
<ul>
<li>
<p>statistics related to historical data (through a JSON file the values described above, i.e., mean, variance, minimum and maximum values, are illustrated). The city and period to be evaluated are chosen by the user.</p>
</li>
<li>
<p>
</p></li></ul><ul>
<li>
statistics related to future data (through a JSON file, the user is shown whether the predictions, based on the collected data, were reliable or not). The user will also choose the error threshold through which the reliability will be evaluated.</li>
</ul>
<h2 id="rotte-dellapplicazione">Application routes</h2>
<table>
<thead>
<tr>
<th>Call type</th>
<th>Route</th>
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
<li>Returns to the user the metadata related to the dataset</li>
<li>Returns metadata related to statistics, both historical and future, to the user</li>
<li>It was used to save the data in the dataset<br>
<em>Note</em>: what is returned by this call is overwritten in the dataset.</li>
<li>Returns current data</li>
<li>Returns historical data</li>
<li>Returns future data</li>
<li>Returns statistics made from historical data</li>
<li>Returns statistics related to forecasts</li>
</ol>
<h2 id="filtri">Filters</h2>
<p>The user can filter the data returned from the calls by choosing the city(ies) to return and the period to consider.<br>
For calls 4, 5, and 6, the body (in JSON format) must be of the following type:</p>
<pre><code>{
    "primaCitta": &lt;n1&gt;,
    "ultimaCitta": &lt;n2&gt;,
    "giornoIniziale": &lt;n3&gt;,
    "giornoFinale": &lt;n4&gt;
}</code></pre>
<p>The numbers <strong>n1</strong> e <strong>n2</strong>must be between 1 and 3 (1 for Trieste, 2 for Ortona, and 3 for Venice), so the user can choose which cities to show.<br>
The numbers <strong>n3</strong> e <strong>n4</strong> instead must be between 1 and 5 ( days ranging from 01/01 to 05/01 for historical data, 06/01 to 10/01 for current data, and 06/01 to 10/01 for forecasts), so by doing so the user can choose the period to be considered.</p>
<p><em>Note</em>: n2 must necessarily be greater than or equal to n1 (the latter case if only one city is to be considered), just as n4 must be greater than or equal to n3.</p>
<p>
</p><p>
For call 7 the same body is used, but in this case <strong>n1</strong> e <strong>n2</strong> must be equal, as statistics can only be made for each individual city.</p><br>
Call 8 has the following body (again in JSON):
<pre><code>{
    "primaCitta": &lt;n1&gt;,
    "ultimaCitta": &lt;n2&gt;,
    "giornoIniziale": &lt;n3&gt;,
    "giornoFinale": &lt;n4&gt;,
    "soglia_errore": &lt;n5&gt;
}</code></pre>
<p>The same selection criteria apply for n1, n2, n3 e n4.<br>
<strong>n5</strong> must be a number between 0 and 100, and it stands for the percentage of error threshold.</p>
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

## External libraries

<p>For the application to work, import the following libraries into the IDE: - json-simple-1.1 - junit5.</p> 
<p><em>Note</em>: the library json-simple-1.1 is present in the files of the <a href="https://github.com/fd-col/Weather-App">repository</a>.</p>

## Contributors:

- Colleluori Federico 50%
- Camplese Francesco 50%
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTYyNTg3NDA1XX0=
-->

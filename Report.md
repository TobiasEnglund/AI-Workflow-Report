# Rapport: Arbetsflöde för AI-projekt

## Datainsamling

För att starta ett AI-projekt krävs det först och främst data. Data kan samlas in i olika format som CSV, JSON, eller XML och lagras på olika sätt, t.ex i datalager, datasjöar och molndatalager. Varje lagringssätt har fördelar och nackdelar och stödjer olika dataformat samt är optimerade för olika användningsfall.  

[Källa](https://www.analytixlabs.co.in/blog/data-acquisition/#The_Data_Acquisition_Process)

Data kan även samlas in på egen hand genom t.ex sensorer, webbskrapning eller manuella metoder (så som enkäter).

**Scenario:** I vårt fall skulle vi vilja samla data om huspriser, t.ex:

- Antal rum
- Storlek i kvadratmeter
- Geografiskt läge
- Närhet till skolor, parker, kollektivtrafik, m.m
- Ålder på huset
- Renoveringshistorik

Vi skulle kunna hitta data om detta från offentliga register eller genom webbskrapning på t.ex Hemnet.se eller liknande webbsidor. Vi skulle kunna ha en kombination av strukturerad data (t.ex antal rum) och ostrukturerad data (t.ex textbeskrivningar). Vi hade kunnat samla datan i ett molndatalager, t.ex Google BigQuery.

## Datavisualisering

Efter datasamling är det viktigt att visualisera datan för att identifiera mönster och anomalier. Det finns flera metoder för detta, inklusive tabeller och stapeldiagram, som kan vara användbara för att snabbt identifiera anomalier eller jämföra värden från olika kategorier. 

[Källa](https://www.ibm.com/topics/data-visualization)

**Scenario:** I vårt scenario kan vi använda tabeller för att snabbt identifiera anomalier och stapeldiagram för att jämföra medianhuspriser i olika områden. Vi kan även använda ett spridningsdiagram i kombination med linjär regression för att se ifall det finns något samband mellan husstorlek och pris. För datavisualiseringen kan vi använda Matplotlib i Python.

## Databearbetning

För att datan ska kunna användas effektivt måste den ofta bearbetas och förberedas. Det sker i 3 steg:

1. **Formatering:** Det första steget är att se till att den insamlade datan är i ett lämpligt format. Textdata kan till exempel lagras i CSV- eller XLS-filer, medan bilddata kan sorteras i kataloger.
2. **Rengöring:** Efter formateringen måste datan rengöras, vilket innebär borttagning av felaktig eller ofullständig data, hantering av saknade värden, eliminering av dubbletter och korrigering av strukturella fel och anomalier.
3. **Funktionsteknik:** Det här steget kan inkludera hantering av kategoriska data (t.ex "one-hot encoding"), skalning av funktioner, reducering av dimensioner, val av funktioner och skapande av nya funktioner (t.ex inpackningsmetoder, filtermetoder eller inbäddade metoder).  

[Källa](https://labelyourdata.com/articles/data-collection-methods-AI#step_1_data_acquisition)

**Scenario:** I vårt fall kan vi skapa en CSV-fil där vi samlar data om alla "features," vilket skulle göra det enkelt att bearbeta datan med Pandas i Python. När vi rengör datan kan vi leta efter outliers, t.ex hus med orimliga priser.

## Linjär Regression

Linjär regression är en typ av övervakad maskininlärningsalgoritm som fokuserar på att hitta ett linjärt förhållande mellan en beroende variabel och en eller flera oberoende variabler. Målet är att hitta den bästa linjära ekvationen för att förutsäga värdet på den beroende variabeln. Linjens lutning indikerar hur mycket den beroende variabeln förändras när en oberoende variabel förändras.  
[Källa](https://www.geeksforgeeks.org/ml-linear-regression/)

**Scenario:** I vårt scenario passar linjär regression perfekt. Vår beroende variabel skulle i detta fallet vara huspris, och de oberoende variablerna skulle vara resterande data, dvs antal rum, storlek på huset, osv. Genom att använda linjär regression kan vi t.ex se hur huspriset förändras för varje extra rum eller geografiskt läge. För att utföra detta kan vi använda scikit-learn.

## Driftsättning

Efter att modellen är tränad är nästa steg att driftsätta den för att den ska kunna användas i en app eller tjänst. Att implementera en maskininlärningsmodell sker i flera steg:

1. **Förberedelse av driftsättningsmiljön:** Detta steget inkluderar installation av nödvändiga bibliotek och paket, ofta i en isolerad virtuell miljö.
2. **API-konstruktion:** Här byggs ett API för att interagera med modellen. Det tar emot förfrågningar, inputdata och returnerar modellens svar.
3. **Modell-serialisering:** För att API:et ska kunna använda modellen måste den först serialiseras, oftast med verktyg som "joblib" i Python.
4. **Server- eller molnval:** Här väljer utvecklaren i vilken miljö appen ska köras. Det kan vara på en egen server eller en molnplattform, t.ex AWS eller Azure ML.
5. **Testning i produktionsliknande miljö:** Innan modellen driftsätts är det viktigt att testa hela flödet i en miljö som efterliknar den slutliga produktionsmiljön.
6. **Driftsättning:** Efter att modellen har testats flyttas koden och datan till produktionsmiljön som utvecklaren valde i steg 4 (förutsatt att testresultaten var positiva) och driftsätts.
7. **Övervakning och underhåll:** När modellen är live krävs kontinuerlig övervakning. Detta kan göras genom att spåra API-användning, prestandamått och undersöka potentiella fel.  

[Källa](https://www.projectpro.io/article/machine-learning-model-deployment/872)

**Scenario:** Vi skulle kunna använda en molnserver, t.ex AWS, för att förbereda en virtuell miljö. Vi kan använda ett ramverk, t.ex Flask, för att bygga ett API. API:et tar emot den insamlade datan (antal rum, storlek, osv). Vi kan serialisera modellen med "joblib" och lagra den på samma molnserver. Innan vi driftsätter modellen kan vi testa den i en produktionsliknande miljö. Ifall det fungerar som det ska i testerna så kan vi driftsätta vår modell. Det är även viktigt att vi övervakar och underhåller modellen! Vi kan t.ex implementera loggning för att hålla koll på modellens prestanda och för att hitta eventuella problem.

## Teknologier i Maskininlärningsprocessen

Det finns mängder med teknologier och verktyg som kan användas i olika steg av maskininlärningsprocessen.

**Scenario:** I vårt scenario har vi använt dessa:

1. **Google BigQuery:** För att lagra och hantera vår data i ett molndatalager.
2. **Python:** Det huvudsakliga programmeringsspråket vi använder i kursen.
3. **Pandas:** För databearbetning och rengöring av vår dataset.
4. **Matplotlib:** För datavisualisering där vi använde tabeller, stapeldiagram och spridningsdiagram.
5. **Scikit-learn:** För att träna vår linjära regressionsmodell.
6. **Flask:** För att bygga ett API för vår modell.
7. **AWS:** Som molnserver, där vi förbereder vår virtuella miljö, lagrar den serialiserade modellen och driftsätter vårt API.
8. **Joblib:** För att serialisera vår tränade modell.

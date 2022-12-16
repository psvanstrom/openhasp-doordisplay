# openhasp-doordisplay

Implementation av en dörrdisplay som visar utomhus- och inomhustemperatur, busstider och skolmat. Byggd på en WT32-SC01-display med OpenHASP (https://openhasp.com) och Home Assistant (https://www.home-assistant.io/).

<img width="444" alt="image" src="https://user-images.githubusercontent.com/5547521/208207140-2e217786-7904-44ae-a059-6b8d6ce9ed81.png">


## Sensorer
| Sensor        | Beskrivning |
| ------------- |:-----|
| sensor.outside_temperature | Skapad med [Min/Max-integrationen](https://www.home-assistant.io/integrations/min_max/) som alltid tar det lägsta värdet av mina två utomhustemperatur-sensorer. |
| sensor.outside_temperature_min | Dygnets lägsta ute-temperatur, skapad med [Daily Sensor](https://github.com/jeroenterheerdt/HADailySensor) |
| sensor.outside_temperature_max | Dygnets högsta ute-temperatur, skapad med [Daily Sensor](https://github.com/jeroenterheerdt/HADailySensor) |
| sensor.inside_temperature | Skapad med [Min/Max-integrationen](https://www.home-assistant.io/integrations/min_max/) som tar medelvärdet av ett antal inomhustemperatur-sensorer|
| sensor.inside_temperature_min | Dygnets lägsta inne-temperatur, skapad med [Daily Sensor](https://github.com/jeroenterheerdt/HADailySensor) |
| sensor.inside_temperature_max | Dygnets högsta inne-temperatur, skapad med [Daily Sensor](https://github.com/jeroenterheerdt/HADailySensor) |
| weather.hem | Aktuellt väder från [Väder-integrationen](https://www.home-assistant.io/integrations/weather/) |
| sensor.hasl_* | Två busshållplatssensorer från [HASL-integrationen](https://github.com/hasl-sensor/integration) |
| sensor.skollunch_* | Scrape-sensorer som hämtar veckans skolmat från skolmaten.se |

## Installation 
1. Installera OpenHASP i Home Assistant och på displayen (https://openhasp.com/latest/)
2. Installera Daily Sensor och HASL (se länkar ovan)
3. Ladda upp [pages.jsonl](pages.jsonl) till displayen
4. Ladda ned fonten [Oswald-Heavy](https://www.dafontfree.net/oswald-heavy/f92294.htm) och ladda upp ttf-filen till displayen.
5. Ladda upp lämpliga väderikoner till displayen som matchar namnen som [väderintegrationen använder](https://www.home-assistant.io/integrations/weather/#condition-mapping). Jag utgick från dessa [ikoner](https://www.flaticon.com/packs/weather-1050).
6. Ladda upp lämpliga övriga ikoner
7. Konfigurera Home Assistant i `configuration.yaml` med innehållet i [openhasp.yaml](openhasp.yaml)
8. Modifiera så allt passar ditt hem

## Node-RED
Jag använder Node-RED för att automatisera på- och avslag av skärmen. Mellan 07:00 och 00:30 är skärmen på, därefter slås den av. Slås larmet på så slås displayen av och slås larmet på så slås displayen på om tiden är inom tidsintervallet. Varje timme körs `antiburn`-tjänsten på displayen för att förhindra inbränning. Varje navigering från startsidan startar en timer som ändrar tillbaka till startsidan efter 180 sekunder. Node-RED-flödet finns [här](nodered-flow.json).

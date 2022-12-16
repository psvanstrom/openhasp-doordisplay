# openhasp-doordisplay

Implementation av en dörrdisplay som visar utomhus- och inomhustemperatur, busstider och skolmat. Byggd på en WT32-SC01-display med OpenHASP (https://openhasp.com) och Home Assistant (https://www.home-assistant.io/).

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

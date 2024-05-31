# API repozitorius

API repozitorius skirtas API schemoms talpinti ir versijuoti, iš šiame
repozitoriume saugumų schemų atnaujinami API vartai.

API repozitorume talpinamos API schemos ir DSA duomenys skirti duomenų
apsikeitimui tarp informacinių sistemų. DSA atveju, talpinami tik tie duomenys,
kurių `access` yra daugiau už `private`, jei DSA yra parengtas naudojant uždarą
duomenų šaltinį, DSA lentelėje neturi būti užpildytas `source` stulpelis. DSA
`source` stulpelis gali būti užpildytas, jei DSA yra sukurtas iš kito API,
kuris yra skirtas duomenų apsikeitimui tarp informacinių sistemų.

Šiame repozitoriume API schemos talpinamos naudojant tokią failų ir katalogų
struktūrą:

    {group}/{form}/{org}/{catalog}/{resource}

Pavyzdžiui:

    datasets/gov/rc/ar/broker/config.yaml

`{resource}` gali būti duomenų rinkinys (duomenų failas) arba duomenų paslauga
(API).


### Duomenų teikimas pagal UDTS

Failų ir katalogų struktūros elementų paaiškinimai:

- `group` - duomenų šaltinių grupė, galimi variantai:
  - `datasets` - duomenys teikiami per UDTS arba duomenys teikiami statinių
    duomenų failų forma. Taikoma visosm naujai kuriamoms ar modernizuojamoms
    informacinėms sistemoms ir duomenų teikimo paslaugoms.
  - `services` - duomenys teikiami ne per UDTS, o per dinaminius API, tokius
    kaip SOAP, XML ar JSON API, taikoma visoms esamoms informacinėms sistemoms
    ir duomenų publikavimo paslaugoms.
- `form` - duomenų teikėjo organizacijos forma, galimi variantai:
  - `gov` - valstybinė organizaija
- `org` - sutrumpintas, Duomenų kataloge (data.gov.lt) registruotas
  organizacijos kodinis pavadinimas.
- `catalog` - sutrumpintas, Duomenų kataloge (data.gov.lt) registruotas
  informacinės sistemos kodinis pavadinimas.
- `resource` - sutrumpintas, Duomenų kataloge (data.gov.lt) registruotas
  duomenų rinkiio ar paslaugos kodinis pavadinimas.


### Duomenų teikimas ne pagal UDTS

Kiekviename `datasets/.../resource` kataloge, kai duomenys teikiami pagal UDTS,
pateikiami tokie failai:

- `config.yaml` - [duomenų agento ir API vartų konfigūracjos
  failas](https://atviriduomenys.readthedocs.io/spinta.html#konfiguravimas),
  naudoja `dsa.csv` failas duomenų šaltinių konfigūracijai.
- `dsa.csv` - [duomenų struktūros aprašas](https://ivpk.github.io/dsa/).
- `openapi/**/*.yaml` - API specifikacija
  [OpenAPI](https://spec.openapis.org/oas/latest.html)/YAML formatu,
  redaguojamas rankiniu būdu ir generuojama iš `dsa.csv` ir [UDTS
  šablono](https://ivpk.github.io/uapi/). UDTS šablon failus galima rasti [UDTS
  repozitoriume](https://github.com/ivpk/uapi).
- `openapi.json` - API specifickaija
  [OpenAPI](https://spec.openapis.org/oas/latest.html)/JSON formatu,
  generuojamas automatiniu būdu iš `openapi/**/*.yaml` failų.

Kiekviename `services/.../resource` kataloge, kei duomenys teikiami ne per
UDTS, pateikiami tokie failai:

- `config.yaml` - API vartų konfigūracijos failas.
- `openapi.json` - API specifikacija
  [OpenAPI](https://spec.openapis.org/oas/latest.html)/JSON formatu,
  generuojama automatiškai iš `openapi.yaml`.
- `service.wsdl` - API specifikacija WSDL formatu, jei duomenys teikiami per
  SOAP API.
- `schemas/` - JSON arba XSD schemos, naudojamos kartu su `openapi.json` ir
  `service.wsdl` failais.

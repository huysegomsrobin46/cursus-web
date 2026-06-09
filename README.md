# SASM Foundations — cursus-web

Dynamische Toledo-viewer voor SASM Foundations (UCLL).  
Live op: https://sasmfoundations.almoradi.be

## Hoe werkt het

Toledo-submodules linken naar URLs als:
- `https://sasmfoundations.almoradi.be/?week=01` — weekoverzicht
- `https://sasmfoundations.almoradi.be/?week=01&section=doelstellingen` — specifieke sectie

De pagina laadt het bijhorende `weeks/week-01.yml` en rendert de gevraagde sectie. Bij elke `git push` naar `main` deployt Vercel automatisch (~30 seconden).

## Content toevoegen of aanpassen

1. Open `weeks/week-XX.yml`
2. Pas de velden aan
3. `git push` naar `main` → Vercel deployt automatisch

## YAML-structuur

```yaml
week: 1
titel: "Titel van de week"
fase: A          # A, B of C
leerdoelen: [LD1, LD5, LD8]

wist_je_dat:
  tekst: "Prikkelend feit of quote"
  link: "https://..."   # optioneel
  bron: "Naam bron"     # optioneel

doelstellingen:
  - "Wat de student na deze week kan"

wat_weet_je_al:
  - "Activerende vraag"

leerinhoud:
  beschrijving: "Placeholder tekst"
  items: []
  # of met content:
  # items:
  #   - type: slides   # slides | video | pdf
  #     label: "Naam"
  #     url: "https://..."

tips_en_tricks:
  - "Praktische tip"

en_nu:
  tekst: "Instructie voor de opdracht"
  link: "https://github.com/SASM-Foundations/labo-week-XX"

test_jezelf:
  - "Begripsvraag"
```

## Lokaal testen

Fetch werkt niet via `file://` — gebruik een lokale server:

```bash
cd poc/cursus-web
python -m http.server 8080
# open http://localhost:8080/?week=01&section=doelstellingen
```

## Sectie-sleutels voor Toledo-links

| Sectie | URL-parameter |
|---|---|
| Weekoverzicht | *(geen `&section`)* |
| Wist je dat | `&section=wist-je-dat` |
| Doelstellingen | `&section=doelstellingen` |
| Wat weet je hier al over? | `&section=wat-weet-je-al` |
| Leerinhoud | `&section=leerinhoud` |
| Tips en tricks | `&section=tips-en-tricks` |
| En nu is het aan jou! | `&section=en-nu` |
| Test jezelf | `&section=test-jezelf` |

## Repo-structuur

```
cursus-web/
├── index.html        ← viewer (HTML + CSS + JS)
├── vercel.json       ← Vercel deployment config
├── README.md
└── weeks/
    ├── week-01.yml   ← volledige content week 1
    ├── week-02.yml   ← skeleton (invullen na contactles)
    └── ...
```

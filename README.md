# FamilieFlow 🏡

Gedeelde gezinsagenda + takenverdeling met punten. Eén HTML-bestand, geen installatie of build nodig.

## Bestanden

```
index.html                              ← de complete app (opmaak + code)
supabase/schema.sql                     ← database: alles in één keer (nieuwe installatie)
supabase/update-002-…, update-003-… ← alleen nodig als je schema.sql al eerder had uitgevoerd
```

## Eerst even proberen (zonder Supabase)

Dubbelklik op `index.html`. Je ziet **Probeer de demo**: een voorbeeldgezin met afspraken, taken en punten.
Alles werkt, maar de gegevens staan alleen in die browser en worden niet gedeeld. Met *Opnieuw* zet je de demo terug; met *Gezin → Demo afsluiten* ga je eruit.

## In 4 stappen online

**1. Supabase (database)**
- Maak een gratis project aan op supabase.com.
- Ga naar *SQL Editor* → plak de inhoud van `supabase/schema.sql` → *Run*.
- *Authentication → Providers → Email*: zet *Confirm email* uit als je zonder bevestigingsmail wilt testen.

**2. Gegevens invullen**
Open `index.html` en vul bovenaan in het script in:
```js
const SUPABASE_URL = "https://xxxx.supabase.co";
const SUPABASE_ANON_KEY = "eyJ...";
```
Je vindt ze in Supabase onder *Project Settings → API*. De anon key mag openbaar: de database-regels (RLS) zorgen dat ieder huishouden alleen zijn eigen gegevens ziet.

**3. GitHub**
- Maak een repository `familieflow` aan op github.com/new.
- *Add file → Upload files* → sleep `index.html` en de map `supabase` erin → *Commit*.

**4. GitHub Pages**
- Repository → *Settings → Pages* → Source: *Deploy from a branch* → branch `main`, map `/ (root)` → *Save*.
- Na ± 1 minuut staat de app op `https://JOUWNAAM.github.io/familieflow/`.
- Zet dat adres in Supabase bij *Authentication → URL Configuration* als **Site URL** en bij **Redirect URLs**.

Tip: open de link op je telefoon en kies *Zet op beginscherm*. Dan werkt het als een app.

## Wat zit erin

- **Huishouden** met uitnodigingscode én -link (code wordt automatisch ingevuld); kinderen zonder telefoon toevoegen als lid zonder account.
- **Agenda**: dag (tijdlijn), week en maand, filteren per gezinslid.
- **Taken** (dagelijks / wekelijks / eenmalig) met punten. Afvinken → kiezen wie het deed → punten direct op het bord.
- **Scores**: ranglijst per week/maand en verdeling in procenten.
- **Beloningswinkel**: ieder spaart punten op een eigen saldo en wisselt ze in (zakgeld, eten kiezen, taak laten overnemen…). De database controleert dat niemand onder nul komt; inwisselen is terug te draaien.
- **Gezamenlijk doel**: samen sparen, bijv. 400 punten per week = pizza-avond.
- **Geschiedenis**: verdiende (+) en ingewisselde (−) punten, wie, wat en wanneer.
- **Realtime**: vinkt iemand anders iets af, dan zie je het meteen.

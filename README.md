# Pokemon

We gaan een kleine website maken die Pokemons kan tonen. We gaan hiervoor gebruik maken van de [PokeAPI](https://pokeapi.co/).
Bij deze een klein stappenplan. Zoals steeds kan je er ook voor opteren om zelf aan de slag te gaan en dit te laten werken!

## Werken met git
Maak een GitHub repository aan en clone deze naar je computer.
De docent toont hoe je dit kan doen. Je kan dit ook eenvoudig zelf opzoeken (sommigen hebben dat vorig lab al gedaan).
Het zal zeker nuttig zijn om op deze manier te werken, zodat je steeds terug kan naar eerdere stappen als we dingen herwerken.

## Voorbereiding

Eerst ruimen we onze app op, zoals we al iedere keer deden.
- [ ] Verwijder alle components (maar laat het mapje zelf staan).
- [ ] Verwijder alle assets (maar laat het mapje zelf staan).
- [ ] Haal in de file `main.ts` de import naar de CSS (`import './assets/main.css'`) weg. Want we hebben die file net verwijderd.

We gaan vanaf nu ook in onze file `index.html` een paar dingen aanpassen.
- [ ] Update de `<title>` tag. Dit kan bv. `<title>Pokemon App</title>` worden.
- [ ] Download https://www.favicon.cc/?action=icon&file_id=883760 en zet deze `.ico`-file in map `public`. (Ja, je zal misschien een bestaande file moeten vervangen.)
Deze file wordt al ingeladen in onze `index.html`-file (`<link rel="icon" href="/favicon.ico">`).

Als laatste:
- [ ] Het kan geen kwaad om ook een CSS reset te doen. Dan hebben we alvast een goede basis om mee te werken.
We hebben al verschillende resets behandeld. We gebruik nu een keer: https://unpkg.com/tailwindcss@3.3.5/src/css/preflight.css. Download de CSS-file naar `/assets` en import deze in `main.js`.
- [ ] We zullen als font Work Sans gebruiken:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@400;600&display=swap" rel="stylesheet">
```
```scss
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}
```

## Aan de slag!
We gaan nu aan de slag met de API. We gaan eerst een lijst van Pokemons tonen.
- [ ] Van mij krijg je het logo (zie Leho). Deze kan je in `App.vue` zetten.
- [ ] In `App.vue` gaan we een functie maken die alle Pokemons kan ophalen.
```js
const getPokemons = async function (limit = 100000) {
  const data = await fetch(
    `https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`,
  ).then((r) => r.json())
}
```
Door een standaard waarde aan `limit` te geven, kunnen we optioneel een andere waarde meegeven en zo dus minder Pokemons tegelijk opvragen.
- [ ] Zet de limit voorlopig op `12`.
- [ ] Maak een variabele (ref) `pokemons` aan. Deze zal een array van Pokemons bevatten als we de data hebben opgehaald.
- [ ] Als de data geladen is, gaan we de Pokemons in de variabele `pokemons` steken.
- [ ] Met deze data kunnen we aan de slag. Toon een overzicht van alle Pokemons.
Start met de naam van elke Pokemon te tonen.
- [ ] Maak een component `Pokemon.vue` aan. Deze zal een Pokemon tonen, met meer informatie.
We kiezen er dus voor om deze keer in een component aan de slag te gaan.
- [ ] Importeer de component in `App.vue` en gebruik deze om de Pokemons te tonen. Toon opnieuw de naam van elke Pokemon.
- [ ] Toon ook de afbeelding van elke Pokemon.
Met de volgende url kan je een afbeelding ophalen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/1.gif` (vervang `1` door het nummer van de Pokemon).

In deze component gaan we een Pokemon tonen, met ook telkens een knopje om de Pokemon 'om te draaien'. We tonen ook een knopje 'meer info', maar dat zal nog niet werken.
Start eerst met het maken van de layout in `scss`:
- [ ] Bovenaan tonen we telkens de (geanimeerde) afbeelding van de Pokemon.
  - Trek deze foto met `0.5rem` naar beneden zodat dit op ons infokader zal rusten.
  - Geef de foto een vaste hoogte van `7rem`. De breedte mag je op `auto` laten staan. (Ik ga zelden een foto vergrootten, maar hier kan het net...)
- [ ] In het infokader zetten we de naam (h2), een checkbox (typ="checkbox") en een p-tag met de tekst 'Meer info'.
  - De naam krijgt een font-size van `1.5rem`. Met een font-weight van 600. Ik maak ook met CSS de eerste letter een hoofdletter.
  - De p-tag krijgt een margin-left van `auto`.
  - De code voor de checkbox is:
  ```scss
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    background: #111111;
    border-radius: 50%;
    height: 3rem;
    width: 3rem;
    cursor: pointer;
    margin-left: 1rem;
    transition: background 0.2s ease-in-out;
    color: white;

    &:hover {
      background: #808080;
    }

    &__input {
      display: none;
    }
  ```
  Ik toon een lucide icon als de checkbox aangevinkt is. Ik gebruik hierbij: `<RefreshCw />` en `<RefreshCcw />`.
- [ ] Maak de Pokemons ook responsive.
- [ ] Maak een variable aan om bij te houden of een component de voor- of achterkant toont. Bv. een ref `showBack` met een boolean of je de achterkant wil zien.
  - Zorg ervoor dat de checkbox de waarde van deze ref aanpast (v-model).
  - Gebruik de waarde van deze ref om te bepalen of je de voor- of achterkant toont:
  ```hmtl
    :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/  versions/generation-v/black-white/animated/${showBack ? 'back/' : ''}${pokemon.url.split('/')[pokemon.url.split('/').length - 2]}.gif`"
  ```

Als we nu de pagina openen, kan het zijn dat we eerst moeten wachten totdat de API data teruggeeft (dit kunnen we ook nadoen in Chrome). We kunnen dit oplossen door een loading state te maken.
- [ ] Maak een variabele (ref) `loading` aan. Deze zal een boolean zijn.
- [ ] Zet de waarde van `loading` op `true` voor we de data ophalen.
- [ ] Zet de waarde van `loading` op `false` als de data geladen is.
- [ ] Gebruik deze variabele om een loading state te tonen. Dit kan je doen door een `v-if` te gebruiken op de `div` waarin je de Pokemons toont.
- [ ] Maak een component `Loading.vue` aan. Deze zal een loading state tonen.
  - We voorzien een aantal 'lege' grijze pokemon kaarten.
  - Pak de Pokemon styling erbij en maak alles na, maar dan grijs en zonder inhoud.
- [ ] Importeer de component in `App.vue` en gebruik deze om de loading state te tonen.
- [ ] Maak de loading state responsive.
  TIP: Als je de loading-ref niet op true zet na het laden, kan je eenvoudig testen of de loading state werkt.
- [ ] Als je het goed gedaan hebt, verspringt er niets tussen de loading state en de Pokemons.

Er zijn in de API 1292 Pokemons, maar we tonen er slechts 12. We gaan dus moeten kunnen 'navigeren' tussen de verschillende pagina's.
- [ ] Maak een component `Pages.vue` aan. Deze zal de pagina's tonen.
  - [ ] We tonen een knopje om naar de vorige pagina te gaan.
  - [ ] We tonen een knopje om naar de volgende pagina te gaan.
- [ ] Maak een variabele (ref) `currentPage` aan. Deze zal een nummer bevatten.
- [ ] Maak een functie aan die de pagina kan verhogen of verlagen.
  - [ ] Zorg ervoor dat de functie de waarde van `currentPage` aanpast.
  - [ ] Let op dat je niet onder de 0 of boven de 107 kan gaan.
  - [ ] Gebruik een `emit` om in `App.vue` bij elke emit nieuwe data op te halen:
  ```js
  const getPokemons = async function (limit = 12, page) {
    const data = await fetch(
      `https://pokeapi.co/api/v2/pokemon/?limit=${limit}&offset=${page * 12}`,
    ).then((r) => r.json())
    pokemons.value = data.results
    loading.value = false
  }
  ```
- [ ] Importeer de component in `App.vue` en gebruik deze om de pagina's te tonen.
- [ ] Denk na over hoe je meer dan 12 tegelijk kan tonen. Maak een select-tag om 12, 16 of 20 Pokemons tegelijk te tonen.

# Todolijst

Een kleine todolijst, gemaakt als oefening voor het keuzedeel Verdieping software.

## Wat kan het

- Een taak toevoegen met een titel (verplicht) en een beschrijving (optioneel)
- Een taak afronden met **Done**. De taak verhuist naar de lijst **Done**
- Een afgeronde taak terugzetten (**Undo**) of verwijderen (**Delete**)
- Het aantal taken per lijst zien
- De taken blijven bewaard na verversen (localStorage)

Er staan 2 voorbeeldtaken in.

## Wat ik hiermee geoefend heb

| Onderdeel | Waar |
|---|---|
| `ref` | Taken en invoervelden |
| `v-model` | Titel en beschrijving |
| `v-for` met `:key` | De lijsten met taken |
| `v-if` | Lege lijst melden |
| `computed` | De lijsten "To do" en "Done" en de tellers |
| `watch` met `deep: true` | Taken opslaan in localStorage |
| `localStorage` | Taken bewaren en weer inladen |

## Starten


```sh
npm install
npm run dev
```

Open daarna het adres uit de terminal (meestal http://localhost:5173).

## Bestanden

- `src/App.vue`: alle code.
# todolijst-vue

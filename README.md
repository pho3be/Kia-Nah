# Kia-Nah

A matchmaker app made as a PoC when I was playing Honkai Impact.
Never finished because Mihoyo did put some similar system on the game a while after I started planning and building it
(Their system was reputation-based and it was really difficult to keep up with the latest game techniques as an individual)

It was originally writen in Lambda for Firebase using FireStore, but the backend code got lost and only the early HTML prototype stayed.
I ported it to SvelteKit as an exercise and for the sake of having some trace of it :D

## Install and use (local)

Once you've installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```


## Building (prod)

```bash
npm run build
```

## Updating the content
- Valkyries are stocked in a simple "json" file : `static/data/db.json`. 
- Their picture is loaded from the `static/img/card/{ShortName}.png` file (Where "ShortName" is the usual 2-letter or more nick given, like "SN", "CH" or "HoV")
- The database is generated from the "tier.csv" file
- All compositions where originally inputted on FireStore but I didn't backup them, so you're stuck with the basic static "default" one ... Unless you're interested on rebuilding this, but that would be madness !


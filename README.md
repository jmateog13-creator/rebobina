# 📼 Rebobina

El grup en dades, per a tutoria: els alumnes contesten des del mòbil unes preguntes ràpides i anònimes. Després el profe «rebobina» i la classe es veu a si mateixa, diapositiva a diapositiva (format *wrapped*, amb estètica pròpia de cinta de vídeo).

## Obrir

- **Profe (pantalla gran):** `index.html`. Tria el contingut i obre la sala.
- **Alumnes:** `movil.html`, o escanejant el QR, amb el codi de 4 números.
- **Previsualitzar sense sala:** `index.html?demo` i `movil.html?demo`.

## Com funciona la sala

- La pantalla gran mostra un **codi de 4 números** i un **QR**. Els alumnes hi entren des del mòbil, sense registrar-se ni iniciar sessió.
- Connexió en directe per Supabase Realtime (wss, port 443: passa el tallafoc de l'institut). Només s'envien missatges en directe: **no es desa res a cap base de dades**.
- Cada mòbil té un identificador aleatori. La pantalla del profe és l'única que compta vots i saldos, i valida tot el que arriba.
- `?demo` a la pantalla del profe simula alumnes per previsualitzar l'activitat sense sala.

## Flux

1. **Sala oberta:** cada alumne contesta al seu ritme, una pregunta per pantalla. Pot canviar les respostes fins que es rebobina. A la pantalla gran només surt «N han respost».
2. **◀◀ Rebobinar:** pantalla completa. Primer la portada i després una diapositiva per pregunta:
   - Numèriques: la mitjana (amb comptador animat), un histograma i, a la de pantalla, el total setmanal de la classe.
   - D'opcions: l'opció més triada en gran i barres amb percentatges.
3. **Final:** preguntes per comentar i **Descarregar resum (CSV)** per a la junta.

**Espai** o **→** avança, **←** torna enrere. També es pot clicar a la dreta o a l'esquerra de la pantalla.

## Privacitat

- Només agregats: mitjanes i percentatges, mai cap resposta individual ni cap nom.
- Una opció amb **menys de 3 vots no es destaca mai** (`MIN_DESTACAR`), i en cas d'empat surt «Opinions repartides».
- No es desa res enlloc. En tancar la sala, les respostes desapareixen. El CSV només conté totals.

## Preguntes

A `preguntes.json`. Només respostes tancades, sense text lliure, perquè no es pugui projectar res inadequat. Hi ha dos tipus:

- `num`: `min`, `max`, `pas`, `inicial` i `unitat`. Amb `diapo.setmana: true` s'hi afegeix el total setmanal de la classe.
- `opcio`: `opcions` (de 2 a 6).

`diapo.frase` admet `{classe}`. `diapo.extra` és una dada de context, per exemple les hores de son recomanades.

# TyFOAM Roadmap — Protocollo collaborativo

Questa roadmap (`index.html`, Gantt + sinottico → GitHub Pages) è una **dashboard di avanzamento collaborativo** per sviluppo **parallelo**. Leggi questo file prima di inserire o modificare task. Vale anche per agenti AI che operano sul repo.

## Owner
- `daniele@tyfoam.dev` (team `tyfoam`) — sviluppo principale.
- `lorenzo.tortora4@gmail.com` (team `lab`) — laboratorio fisica; avanzamenti paralleli.

I dati task stanno nel blocco `<script id="todo-data">` dentro `index.html` (JSON). Ogni task ha `id`, `owner`, `owner_team`, `stato` (Now/Next/Later), `dev_status`, `criticita`, `start`, `end`, `progress`, `descrizione`, `dependencies`.

## Workflow (branch + PR — modello A)
1. `main` = **release cumulativa pubblicata** (fonte di verità del Gantt live). NON pushare task nuovi direttamente su main.
2. Ogni owner lavora su un **branch** dedicato: es. `lorenzo/<argomento>`, `daniele/<argomento>`.
3. Apri una **Pull Request** verso `main`.
4. **Collision-check** (sotto) prima del merge — lo esegue l'AI/revisore.
5. Merge su `main` solo dopo clearance → la release cumulativa si aggiorna.

Così le incompatibilità emergono **al merge**, prima di finire nella release.

## Collision-check (obbligatorio prima di ogni merge)
1. **ID** — nuovo `id` = prossimo `TF-0XX` libero. MAI riusare o duplicare un id esistente.
2. **Doppioni / overlap scope** — niente task che ripete feature/file/descrizione di uno esistente (anche di un altro owner) → evita doppioni e rilavorazioni.
3. **Accavallamenti date** — stesso owner non può avere range `start`–`end` sovrapposti → risequenzia.
4. **Dipendenze** — niente cicli; un task non deve iniziare prima del suo prerequisito.
5. **Falsi positivi** — un task `done` contraddetto da un task nuovo = rework non dichiarato → segnalalo.
6. **Collisione file cross-owner** — se due owner toccano lo **stesso file di codice** in task paralleli → rischio merge-conflict in release → coordinare PRIMA del merge.

## Regole task
- `id` sequenziale `TF-0XX`, univoco e immutabile.
- `owner`/`owner_team` corretti (vedi sopra).
- `stato`: Now (sprint attivo) / Next / Later.
- `criticita`: Alta / Media / Bassa.
- Date `YYYY-MM-DD`, durate realistiche (cadenza giornaliera, pochi giorni per task).
- `dependencies`: lista id da cui il task dipende.

## In sintesi per un'AI collaboratrice
Prima di inserire task: leggi il JSON corrente, scegli il prossimo id libero, esegui i 6 check sopra contro i task esistenti, lavora su un branch, apri PR. Non toccare `main` direttamente.

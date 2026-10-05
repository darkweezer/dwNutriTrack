# NutriTrack (dwNutriTrack)

Einzelne HTML-Datei `index.html` (Tailwind, Chart.js 4.4.1, supabase-js 2), deutsche Oberfläche.
**Diese `index.html` ist der aktuelle Stand** – nicht die ältere Vorlage aus dem NutriTrack-Skill verwenden.
Repo: https://github.com/darkweezer/dwNutriTrack (Branch `main`), Pages: https://darkweezer.github.io/dwNutriTrack/

## Arbeitsweise
- Änderungen direkt in `index.html`, klein und gezielt (Edit), nicht neu schreiben.
- Auf diesem Rechner gibt es kein Node und kein Python: Syntax/Logik im Browser-Pane testen (Datei öffnen, per JS prüfen). localStorage ist dort gesperrt.
- Nach Freigabe durch den Nutzer: commit + `git push origin main`.
- Antworten auf Deutsch, kurz; sagen, was getestet ist und was nicht.

## Funktionen (Stand 10/2026)
Datumsnavigation, Flüssigkeit/Mahlzeiten/Energie-Karten mit Zielen, Schnellerfassung Trinken/Essen (bearbeitbar, Uhrzeit-Dialog, `autoCat`),
Tagesprotokoll mit Bearbeiten/Löschen, drei gestapelte Wochenverläufe (Trinken, Kalorien, Kaffee – Kaffee erkannt per ☕-Icon oder Name via `isCoffee`), JSON-Export/Import (zusammenführen/ersetzen), Supabase-Sync mit Login (☁️).

## Daten (localStorage)
- `nutritrack_data_v1`: `{ "YYYY-MM-DD": { meals:[{id,category,title,calories,time,notes,sid?,dirty?}], fluids:[{id,name,amount,time,icon,sid?,dirty?}] } }`
  `sid` = Supabase-Zeilen-id, `dirty` = lokal geändert, noch nicht hochgeladen.
- `nutritrack_fluid_goal`, `nutritrack_kcal_goal`, `nutritrack_quick_drinks`, `nutritrack_quick_food`
- `nutritrack_supabase` `{url,key}` (nur im Browser, nie in den Code), `nutritrack_sb_deletes` (Lösch-Warteschlange), `nutritrack_sb_auth` (Session)

## Supabase
- `food_logs`: id bigint, created_at timestamptz, meal_type text, description text, calories int, notes text
- `water_logs`: id bigint, created_at timestamptz, amount_ml int, type text, icon text
- RLS aktiv, Policy "nur angemeldet" (for all to authenticated). Login über Supabase Auth (E-Mail/Passwort).
- Sync: Push (Löschungen, neue, geänderte) → Pull (Server gewinnt außer bei `dirty`). Datum/Uhrzeit ↔ `created_at`.

## Offene Ideen
README, Dark Mode, Makronährstoffe, Profile/user_id, Erinnerungen, Ziele in Supabase.

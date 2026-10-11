# Promptomizer Blog

Der Blog unter **https://www.promptomizer.de/blog**. Seit 11.10.2026 ein eigenes Repo und ein eigenes
Vercel-Projekt (`promptomizer-blog.vercel.app`); die Hauptseite reicht `/blog` und `/blog/*` per Rewrite
hierher durch. Für Leser und Suchmaschinen ändert sich nichts: Canonical, Links und Sitemap zeigen auf
www.promptomizer.de.

## Aufbau

- `artikel/<slug>.json` – **die einzige Quelle**, eine Datei je Artikel. Felder: `slug`, `titel`,
  `titelAkzent` (optional), `kategorie`, `datum` (JJJJ-MM-TT), `aktualisiert` (optional), `autor`,
  `auszug`, `metaTitel` (optional), `inhalt` (HTML, erlaubt: h2, h3, p, ul, ol, li, pre, blockquote, a, strong).
- `artikel/_kategorien.json` – optional, Reihenfolge der Kategorie-Filter.
- `tools/build-blog.cjs` – erzeugt `dist/` (Übersicht, Artikelseiten, `blog/blog.css`, `blog/sitemap.xml`).
- `tests/blog-build-smoke.cjs` – läuft bei Vercel nach dem Build. Schlägt Build oder Test fehl, wird
  **nicht** ausgeliefert, der alte Stand bleibt online.
- Schrift, Grundstile, Favicon und Skripte kommen von der Hauptseite (gleiche Domain).

## Wer schreibt hier

Neue Artikel legt der **WorkDESK** an: ist ein Blogartikel im ContentDESK freigegeben, schreibt er zum
geplanten Termin `artikel/<slug>.json` (Commit „Blog: <Titel>“), wartet, bis die Seite online ist, und
meldet sie im SocialDESK als veröffentlicht. Sein Schlüssel darf nur in dieses Repo schreiben.
Von Hand: Datei anlegen oder ändern, lokal `node tools/build-blog.cjs && node tests/blog-build-smoke.cjs`, pushen.

Slug nie ändern (URL). Einen Artikel entfernen: Datei löschen und in der `vercel.json` der Hauptseite
eine Weiterleitung ergänzen.

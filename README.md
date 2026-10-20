# Persönlicher Hugo-Blog

Schlanke eigene Layouts, lokales CSS, keine Themes, kein JavaScript.
Voraussetzung: Hugo ≥ 0.158.0; der Pages-Workflow verwendet wie lokal Hugo 0.162.1.
CI benötigt nur Hugo Standard; Extended/Sass, Node.js und Go sind nicht nötig.
Fedora: `sudo dnf install hugo` (Installation selbst ausführen).
Alle folgenden Befehle im Projektverzeichnis ausführen.

## Lokal ansehen

```sh
hugo version
hugo server
```

Adresse: http://localhost:1313/ — Beenden mit Strg+C.
Ohne Beiträge zeigen Home und Blog einen Leerzustand.
`content/blog/_index.md` ist ausschließlich die technische Blog-Übersicht.

## Beiträge pflegen

Genau ein Befehl legt einen neuen Entwurf an:

```sh
hugo new content/posts/mein-artikel.md
```

Die erzeugte Markdown-Datei in einem Editor oder Obsidian öffnen.
In Obsidian dieses Projekt als eigenen Vault öffnen; keine privaten Vaults kopieren.
Titel und optional Tags/Beschreibung im YAML-Front-Matter ändern,
den Text darunter in normalem Markdown schreiben.
Obsidian-Wikilinks (`[[…]]`) und Embeds (`![[…]]`) funktionieren
nicht automatisch als reguläres Hugo-Markdown; normale Markdown-Links nutzen.
Lokale Bilder bei Bedarf unter `static/images/` ablegen und mit
`![Beschreibung](/images/datei.webp)` einbinden.

- Entwürfe lokal ansehen: `hugo server --buildDrafts`
- Veröffentlichen: in derselben Datei `draft: false` setzen.
  Das Datum darf für sofortige Veröffentlichung nicht in der Zukunft liegen.
- Aktualisieren: dieselbe Markdown-Datei bearbeiten und speichern.
- Löschen: ausschließlich die betreffende Markdown-Datei entfernen.
- Der Dateiname bildet die URL; für stabile Links später nicht umbenennen.

Details zum Zurückziehen: [CONTENT_WORKFLOW.md](CONTENT_WORKFLOW.md).
Home, Blog-Archiv, Tags, RSS und Sitemap entstehen automatisch.
About erst mit eigenem Text anlegen und dann das Menü in `hugo.toml` aktivieren.

## Produktions-Build

```sh
hugo --minify --cleanDestinationDir
```

Ergebnis: `public/` (nicht committen). Entwürfe bleiben ausgeschlossen.
`--cleanDestinationDir` entfernt auch Ausgaben inzwischen gelöschter Beiträge.
Bei Fehlern nennt Hugo die betroffene Datei; YAML-Einrückung und Titel prüfen.

## GitHub Pages später aktivieren

1. Selbst ein Repository `pzdenis.github.io` beim Konto `pzdenis` erstellen.
2. Projektdateien auf dessen Branch `main` übertragen; `public/` ausschließen.
3. Unter **Settings → Pages → Build and deployment → Source**
   **GitHub Actions** auswählen.
4. Workflow unter **Actions** prüfen; nach Erfolg https://pzdenis.github.io/ öffnen.

Nach der Einrichtung veröffentlicht jeder Push auf `main` über GitHub Actions.
Actions folgen der offiziellen Hugo-Anleitung; Hugo ist auf 0.162.1 fixiert:
https://gohugo.io/host-and-deploy/deploy-to-github-pages/

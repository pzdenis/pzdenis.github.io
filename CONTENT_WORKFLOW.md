# Artikel pflegen

Alle Befehle im Projektverzeichnis ausführen. Beiträge liegen unter `content/posts/`. Neue Standardbeiträge sind Markdown-Dateien.

## Anlegen und bearbeiten

```sh
hugo new content/posts/mein-artikel.md
```

Die Datei in einem Texteditor oder Obsidian öffnen. Das Archetype legt
`title`, `date`, `draft: true`, `tags: []` und `description` an.
Titel setzen, optional Tags/Beschreibung ergänzen und unterhalb des
Front Matters den eigenen Text schreiben. Der Dateiname bestimmt die URL;
für stabile Links nach der Veröffentlichung nicht umbenennen.

Obsidian: dieses Projekt als eigenen Vault öffnen. Normale Markdown-Links
und Bilder verwenden; `[[Wikilinks]]` und `![[Embeds]]` werden von Hugo
nicht automatisch wie in Obsidian aufgelöst. Keine privaten Vaults kopieren.

## Entwurf ansehen

`draft: true` beibehalten und lokal starten:

```sh
hugo server --buildDrafts
```

http://localhost:1313/ öffnen; Strg+C beendet die Vorschau.
`hugo server` zeigt nur veröffentlichte Beiträge.

## Veröffentlichen und ändern

In derselben Markdown-Datei `draft: false` setzen. Für sofortige
Veröffentlichung muss `date` in der Vergangenheit oder Gegenwart liegen.
Änderungen erfolgen ebenfalls direkt in dieser Datei.

Vor dem Übertragen prüfen:

```sh
hugo --environment production --minify --cleanDestinationDir --buildDrafts=false
```

Nach der erstmaligen GitHub-Einrichtung werden Änderungen nach Commit
und Push auf `main` automatisch gebaut und veröffentlicht.
Home, Blog, Tags, RSS und Sitemap aktualisieren sich automatisch.
`public/` wird nicht versioniert oder manuell hochgeladen.

## Zurückziehen oder löschen

Zum Zurückziehen `draft: true` setzen; die Markdown-Datei bleibt erhalten.
Zum endgültigen Löschen die betreffende Markdown-Datei entfernen.
Danach erneut bauen und die Änderung auf `main` übertragen.
Erst ein erfolgreiches Deployment entfernt den Beitrag von der Live-Site.
Der Workflow baut frisch und ohne Entwürfe; `--cleanDestinationDir`
entfernt bei lokalen Builds auch alte Ausgaben zurückgezogener Artikel.
Bereits heruntergeladene Kopien und fremde Feed-Caches bleiben außerhalb
der Kontrolle der Website.

## Quarto-Fachartikel

`content/posts/geldmarktkurve/` ist ein Hugo-Leaf-Bundle. `index.html`
enthält Front Matter und den aus Quarto übernommenen Artikelinhalt.
Hugo ergänzt Navigation, Metadaten und Seitenrahmen. Die Formeln liegen
als natives MathML vor, die Bilder sind eingebettet und `article.css`
gilt nur für diesen Beitrag.

Für Änderungen im separaten Quarto-Projekt rendern und den Artikelinhalt
ab der ersten Abschnittsüberschrift in `article.quarto` übernehmen. Front Matter und
Bewertungsstichtag bleiben im Bundle. Erst bei Freigabe den
Autorenplatzhalter ersetzen, `date` und `publishDate` mit dem tatsächlichen
Veröffentlichungsdatum ergänzen und `draft` auf `false` setzen. Danach
Produktions-Build und Sitemap prüfen.

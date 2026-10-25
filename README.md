# Videothek

Persönliche Bibliothek für YouTube-Videos. Eine einzige Datei (`index.html`), gehostet auf GitHub Pages. Die Daten liegen als `library.json` in einem separaten, privaten Repo.

## Einrichtung (ca. 10 Minuten)

### 1. Repo für die Seite anlegen (öffentlich)
1. Auf GitHub ein neues Repo anlegen, z. B. `videothek`, Sichtbarkeit **Public** (GitHub Pages ist im kostenlosen Plan nur für öffentliche Repos verfügbar).
2. `index.html` hochladen: *Add file → Upload files*, dann *Commit changes*.
3. *Settings → Pages*: unter **Source** „Deploy from a branch“ wählen, Branch `main`, Ordner `/ (root)`, *Save*.
4. Nach ein bis zwei Minuten ist die Seite erreichbar unter `https://<dein-name>.github.io/videothek/`.

Die Seite selbst enthält keine Daten. Wer die Adresse kennt, sieht nur eine leere Bibliothek.

### 2. Repo für die Daten anlegen (privat)
1. Neues Repo anlegen, z. B. `videothek-daten`, Sichtbarkeit **Private**.
2. Häkchen bei „Add a README file“ setzen, damit der Branch `main` existiert. Die `library.json` legt die Videothek selbst an.

### 3. Token erstellen
1. GitHub → Profilbild → *Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token*.
2. Name z. B. „Videothek“, Ablaufdatum nach Wunsch (bei Ablauf einfach ein neues eintragen).
3. **Repository access:** *Only select repositories* → nur `videothek-daten`.
4. **Permissions → Repository permissions → Contents:** *Read and write*. Sonst nichts.
5. Token erzeugen und kopieren (beginnt mit `github_pat_`).

### 4. Videothek verbinden
1. Die Seite öffnen → **Einstellungen**.
2. Besitzer (dein GitHub-Name), Daten-Repo (`videothek-daten`), Branch (`main`), Datei (`library.json`) und Token eintragen.
3. **Speichern & verbinden.** Oben rechts steht danach „Synchron“.

Auf jedem weiteren Gerät (z. B. Handy) einmal dieselben Einstellungen eintragen.

### 5. Optional: YouTube-API-Schlüssel für Upload-Datum und Dauer
Ohne Schlüssel holt die Videothek Titel und Creator automatisch. Mit Schlüssel auch Upload-Datum, Dauer und den Status (privat / gelöscht).

1. [Google Cloud Console](https://console.cloud.google.com/) → neues Projekt anlegen.
2. *APIs & Services → Library* → „YouTube Data API v3“ → *Enable*.
3. *APIs & Services → Credentials → Create credentials → API key*.
4. Den Schlüssel einschränken: *Application restrictions* → „Websites“ → `https://<dein-name>.github.io/*`; *API restrictions* → nur „YouTube Data API v3“.
5. Schlüssel in der Videothek unter **Einstellungen → YouTube-API-Schlüssel** eintragen.

Das kostenlose Kontingent (10.000 Einheiten pro Tag) reicht locker: ein Video abfragen kostet 1 Einheit, „Verfügbarkeit prüfen“ 1 Einheit pro 50 Videos.

## Bedienung
- **Video hinzufügen:** „+ Video“ oder eine YouTube-URL irgendwo auf der Seite einfügen (Strg/Cmd+V). Daten werden automatisch geholt.
- **Mehrere Videos auf einmal:** mehrere URLs (eine pro Zeile) einfügen, im Formular oder direkt auf der Seite, oder „+ Video → Mehrere hinzufügen“. Video- und Playlist-URLs lassen sich mischen; du wählst einzelne ab, setzt Genre/Format/Anspruch/Tags für alle und legst optional eine Reihe an.
- **Einordnen:** Unter **Listen** bearbeitest du Genre, Format und Anspruch (Name der dritten Kategorie frei wählbar) samt Beschreibung. Umbenennen ändert alle betroffenen Videos, gleicher Name führt zusammen. „Empfohlene Einteilung“ übernimmt die Liste aus `EINORDNUNG.md` und benennt eindeutige alte Werte automatisch um; der Rest erscheint in den Filtern als „alt“. Die **?**-Knöpfe öffnen die Einordnungshilfe, unter jedem Auswahlfeld steht die Kurzbeschreibung des gewählten Werts.
- **Mehrere Videos bearbeiten:** Filter oder Suche setzen, dann „X Videos bearbeiten“: Genre, Format, Anspruch, Status, Gesehen und Tags für alle Treffer auf einmal ändern. Die Seitenleiste „Einordnen“ zeigt Videos mit alten Werten oder ohne Genre/Format/Anspruch.
- **Schnell per Lesezeichen:** `https://<dein-name>.github.io/videothek/?add=` + Video-URL öffnet direkt das Formular.
- **Reactions:** Format „Reaction“ wählen, dann Original(e) aus der Bibliothek suchen oder deren URL einfügen. Neue Originale werden mit angelegt. Beim Verknüpfen werden das Genre (falls noch leer) und die Tags des Originals übernommen; du kannst sie danach anpassen.
- **Originale automatisch erkennen** (mit YouTube-API-Schlüssel): Beim Hinzufügen liest die Videothek die Videobeschreibung und schlägt verlinkte YouTube-Videos als Originale vor. Steht „React“/„Reaktion“/„reagiere“ im Titel, wird das Format direkt auf „Reaction“ gesetzt; sonst erscheint ein Hinweis „Als Reaction markieren“. Bei bestehenden Videos: Bearbeiten → „Originale in der Beschreibung suchen“.
- **Playlist importieren** (ohne Reihe): im Formular „+ Video“ unter der URL, oder eine Playlist-URL auf der Seite einfügen. Du wählst einzelne Videos ab, legst Genre/Format/Stimmung/Tags für alle fest, kannst sie direkt als gesehen markieren und optional zusätzlich eine Reihe anlegen.
- **Reactions ohne Original finden:** Seitenleiste „Reactions“ → „Ohne Original“. Ist das Original kein YouTube-Video (Twitch-Stream, TV-Sendung, Artikel …), hake im Formular „Original ist kein YouTube-Video“ an, optional mit Beschreibung und Link. Solche Reactions zählen nicht mehr als „ohne Original“.
- **Reactions über ihr Original finden:** Der Schalter in der Filterleiste lässt Reactions auch dann erscheinen, wenn ihr Original zum gewählten Genre oder Tag passt.
- **Reihen** (Tab „Reihen“) fassen zusammenhängende Videos zusammen:
  - *Serie* (feste Reihenfolge), *Playlist* (von YouTube übernommen) oder *Sammlung* (lose Zusammenstellung).
  - **Ganze Playlist importieren:** „+ Reihe“ → Playlist-URL → „Playlist laden“, oder die Playlist-URL einfach auf der Seite einfügen. Braucht den YouTube-API-Schlüssel. Ohne Schlüssel: Video-URLs zeilenweise einfügen.
  - **Standardwerte** (Genre, Format, Stimmung, Tags) gelten für alle Videos, die über die Reihe neu angelegt werden.
  - **Fortschritt** und „Weiterschauen“ springen zum ersten ungesehenen Teil; gelöschte Videos zählen nicht mit.
  - **Mit Playlist abgleichen** holt neu erschienene Folgen nach.
  - Reihenfolge mit ↑/↓ ändern; ✕ entfernt ein Video nur aus der Reihe, nicht aus der Bibliothek.
  - Im Video selbst: „Teil 3 von 12“ mit Vor/Zurück und „Zu Reihe hinzufügen“.
- **Abos** (Tab „Abos“, braucht den YouTube-API-Schlüssel) zeigen die neuesten Videos deiner Kanäle nach Tagen gruppiert, mit „Neu“ seit deinem letzten Besuch:
  - **+ Videothek** übernimmt ein Video als ungesehen, **Ausblenden** blendet es dauerhaft aus (gilt auf allen Geräten).
  - Filter nach Kanal, „★ Nur Favoriten“, „Nur neue“ und „Noch nicht in der Videothek“.
  - **Favoriten:** Stern neben einem Kanal in der Seitenleiste, in „Kanäle“ oder im Video-Detail. Favoriten stehen oben und sind im Feed mit ★ markiert.
  - **Regeln pro Kanal** unter „Kanäle“: *Nur Videos mit* (z. B. nur ein Team eines Liga-Kanals oder `Highlights, Folge`), *Ohne* (z. B. `Livestream, Trailer`), *Shorts ausblenden* sowie Genre, Format und Tags, die übernommene Videos bekommen. Kanäle mit „Nur Videos mit“-Regel werden tiefer durchsucht (letzte 150 Uploads statt 15).
  - Die Liste aktualisiert sich automatisch, wenn sie älter als 30 Minuten ist. Gezeigt werden Videos der letzten 60 Tage; angekündigte Premieren erscheinen erst, wenn sie online sind.
- **Breite Bildschirme:** Ab etwa 1500 px Breite dockt die Detailansicht rechts an, statt das Raster zu überdecken. Du kannst weiter stöbern und mit einem Klick auf ein anderes Video wechseln (schließen mit ✕ oder Esc).
- **Suche:** Taste `/` springt ins Suchfeld.

## Abos aus YouTube importieren (Google Takeout)
1. [takeout.google.com](https://takeout.google.com) öffnen und auf **Auswahl aufheben** klicken.
2. Ganz unten **YouTube und YouTube Music** anhaken, dann auf **Alle YouTube-Daten einbezogen** klicken, dort ebenfalls zuerst **Auswahl aufheben** und nur **Abos** anhaken. Mit **OK** bestätigen.
3. **Nächster Schritt → Export erstellen.** Nach ein paar Minuten kommt eine E-Mail mit dem Download.
4. ZIP entpacken. Die Datei liegt unter `Takeout/YouTube und YouTube Music/Abos/subscriptions.csv`.
5. In der Videothek: Tab **Abos → Kanäle → Abos aus Google Takeout importieren** → Datei wählen.

Neue Abos später einfach einzeln hinzufügen (Kanal-URL, @Handle oder ein Video des Kanals), oder im Video-Detail auf **Kanal in Abos aufnehmen** klicken. Ein erneuter Takeout-Import ergänzt nur fehlende Kanäle; Regeln bleiben erhalten.

**Kontingent:** Eine Aktualisierung kostet etwa 1 Einheit pro Kanal (3 bei Kanälen mit „Nur Videos mit“-Regel) plus 1 pro 50 Videos. Bei 100 Kanälen sind das rund 130 von 10.000 Einheiten am Tag.
- **Einstellungen → Fehlende Daten & Verfügbarkeit prüfen:** ergänzt leere Felder und markiert gelöschte oder private Videos.
- **Export/Import** als JSON für zusätzliche Backups. Jede Änderung ist außerdem ein Commit im Daten-Repo und lässt sich dort zurückverfolgen.

## Sicherheit
Token und API-Schlüssel werden nur im `localStorage` deines Browsers gespeichert und nur an GitHub bzw. Google gesendet. Trag sie nicht auf fremden oder geteilten Geräten ein. Das Token kann nur das Daten-Repo lesen und schreiben, sonst nichts.

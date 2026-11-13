# Präpositionen-Trainer

Ein Browser-Trainer für deutsche **Verben mit Präpositionen** (A1–C2). Du wählst die Präposition nicht aus einer Liste, sondern tippst sie direkt in den Satz ein, und zwar in der Form, die der Satz braucht (*zum*, *am*, *darauf*, *miteinander* …).

**Live-Demo:** https://cherkasovandrii.github.io/verben-mit-praepositionen-trainer/

## Funktionen

- **882 Verben** auf sechs Niveaus (A1 19 · A2 67 · B1 245 · B2 394 · C1 131 · C2 26), jeweils mit einem vollständigen Beispielsatz und dem Kasus (Akk. / Dat.).
- **Drei Themen, die getrennt trainiert werden:**
  - **Präpositionen**: Satzmodus, dazu ein Smalltalk-Modus mit 65 kurzen Dialogen, in denen du alle Lücken ausfüllst.
  - **da-/wo-Wörter** (176 Karten): *dafür, dagegen, davon, darauf, worüber, wovon* …
  - **-einander** (48 Karten): *miteinander, voneinander, aufeinander, ineinander* …
- **Vier Ansichten:**
  - **Karten**: ein Satz nach dem anderen.
  - **Blatt**: alle Sätze der gewählten Niveaus auf einer Seite.
  - **Quiz**: Multiple Choice wie bei Quizlet, also ein Satz mit Lücke und vier Antworten (Tasten `1`–`4`).
    - Jedes Niveau ist in nummerierte Quizze aufgeteilt, von den häufigsten Verben bis zu den seltenen.
    - Du wählst 5, 10, 15 oder 20 Fragen pro Quiz, und der Bestwert jedes Quiz wird gespeichert.
    - Pro Niveau gibt es außerdem ein Zufallsquiz.
  - **Verben**: eine durchsuchbare Liste mit deinem Lernstand.
- **Häufigkeit für B1–C2**: Jede Verbindung ist als *häufig*, *mittel* oder *selten* in der Alltagssprache markiert, in allen drei Themen.
  - Die Einstufung beruht auf der Häufigkeit des Verbs in deutschen Film- und Serienuntertiteln (OpenSubtitles). Sie ist danach korrigiert, wie oft das Verb genau mit dieser Präposition vorkommt.
  - Du kannst zuerst nur die häufigen Verbindungen trainieren und das Blatt sowie die Verbliste nach Häufigkeit sortieren.
  - Neue Karten kommen in der Reihenfolge von häufig nach selten.
  - A1 und A2 sind immer komplett dabei.
- **Wiederholung in Intervallen** (Lernkartei nach Leitner): Bekannte Karten kommen nach 1, 3, 7, 14 und 30 Tagen wieder, Fehler noch in derselben Runde.
- **Tolerante Antwortprüfung:**
  - `ue/ae/oe` zählen als Umlaute.
  - *zu dem* zählt für *zum*, mit dem Hinweis, dass die verschmolzene Form üblicher ist.
  - Umgangssprachliches *drauf, dran, drüber* wird akzeptiert.
  - Wo zwei Präpositionen richtig sind, wird auch die zweite akzeptiert.
  - Gezielte Hinweise bei typischen Fehlern: fehlende Verschmelzung, falscher Kasus, *auf das* statt *darauf*, fehlendes *-r-* bei *dar-*.
- **Alles per Tastatur**: Die Maus brauchst du nie (siehe unten).
- **Fünf Sprachen der Oberfläche**: standardmäßig Deutsch (mit einer deutschen Bedeutungserklärung statt einer Übersetzung), außerdem Russisch, Ukrainisch, Englisch und Arabisch (von rechts nach links).
- Helles und dunkles Design, funktioniert auch auf dem Handy.

## Tastenkürzel

| Taste | Karten | Blatt | Quiz |
|---|---|---|---|
| `Enter` | Antwort prüfen / nächste Karte | Zeile prüfen und zur nächsten springen | nächste Frage |
| `Esc` | „Weiß ich nicht“: Lösung zeigen | Lösung für diese Zeile zeigen | — |
| `1` / `2` | Akk. / Dat. wählen (prüft gleichzeitig) | — | — |
| `1`–`4` | — | — | Antwort wählen |
| `Tab` | nächste Lücke im Dialog | nächste Lücke | — |

Nach einer richtigen Antwort geht es nach etwa einer Sekunde automatisch weiter. Das lässt sich auf der Startseite abschalten.

## So wird der Fortschritt gespeichert

Alles bleibt in deinem Browser im `localStorage`, es wird nichts irgendwohin geschickt:

| Schlüssel | Inhalt |
|---|---|
| `praep-trainer-progress-v1` | Lernfortschritt jeder Karte |
| `praep-trainer-settings-v1` | Sprache, Niveaus, Thema, Häufigkeit, Rundenlänge, Schalter |
| `praep-trainer-quiz-v1` | Bestwert jedes Quiz |

Für jede Karte speichert der Trainer `[Fach, nächste Wiederholung, Versuche, Fehler, letzte Antwort]` unter dem Schlüssel `Modus|Karten-ID`, zum Beispiel `s|A2:warten auf`. Die Modi sind `s` (Satz), `d` (Smalltalk), `pa` (da-/wo-Wörter) und `ei` (-einander). Jedes Thema hat also seinen eigenen Fortschritt.

| Ereignis | Wirkung |
|---|---|
| Richtige Antwort | Die Karte rückt ein Fach weiter (max. 5); nächste Wiederholung nach 1, 3, 7, 14 oder 30 Tagen. |
| Fehler | Zurück in Fach 0; die Karte kommt drei Karten später in derselben Runde wieder. |
| Karte erreicht Fach 3 | Sie gilt als gelernt. |

Das Quiz verändert die Lernkartei nicht: Eine Antwort aus vier Möglichkeiten zu wählen ist leichter, als sie selbst zu tippen.

Der Fortschritt gilt für einen Browser auf einem Gerät. In privaten Fenstern, nach dem Löschen der Websitedaten oder unter einer anderen Domain fängst du bei null an. Mit dem Knopf **Fortschritt zurücksetzen** auf der Startseite löschst du ihn absichtlich.

Läuft die Seite als Claude-Artefakt auf claude.ai, wird der Fortschritt zusätzlich im Claude-Konto der Person gespeichert, die die Seite geöffnet hat. Ist das nicht möglich, bleibt er im Browser.

## Lokal starten

Kein Build-Schritt und kein Server nötig: `index.html` herunterladen und im Browser öffnen.

## Auf GitHub Pages veröffentlichen

1. Ein Repository anlegen und `index.html` sowie `README.md` hochladen.
2. Unter **Settings → Pages** die Option **Deploy from a branch** wählen, dann den Branch `main` und den Ordner `/ (root)`.
3. Nach etwa einer Minute ist der Trainer unter `https://<dein-name>.github.io/<repository>/` erreichbar.

Netlify Drop, Cloudflare Pages und Vercel funktionieren genauso, denn es ist eine einzige statische Datei.

## Projektstruktur

```
index.html   die ganze App: Markup, Styles, Skript und Daten
README.md
```

Die Kartendaten stecken als JSON in `index.html`, im Element `<script type="application/json" id="data">`, mit drei Arrays: `cards`, `da` und `ei`. Eine Karte sieht so aus:

```json
{
  "id": "B1:sich verlassen auf",
  "l": "B1",
  "b": "sich verlassen",
  "p": "auf",
  "c": "A",
  "f": 3,
  "q": 225.1,
  "ex": ["0Auf meinen besten Freund ", "1kann", "0 ich ", "1mich", "0 immer ", "2verlassen"],
  "ru": "полагаться на", "uk": "покладатися на", "en": "to rely on", "ar": "يعتمد على", "de": "jemandem vertrauen"
}
```

| Feld | Bedeutung |
|---|---|
| `l` | Niveau |
| `b` | Verb |
| `p` | Präposition |
| `c` | Kasus (`A` / `D`) |
| `f` | Häufigkeit: `3` häufig, `2` mittel, `1` selten (nur B1–C2) |
| `q` | Häufigkeit des Verbs pro Million Wörter in den Untertiteln (zum Sortieren innerhalb einer Stufe) |
| `ex` | der Beispielsatz, in Segmente zerlegt |
| `st` | optional: Smalltalk-Dialog im selben Segmentformat |
| `alt` | optional: weitere Präpositionen, die ebenfalls akzeptiert werden |

Jedes Segment in `ex` beginnt mit einem Kennzeichen:

| Kennzeichen | Bedeutung |
|---|---|
| `0` | normaler Text |
| `1` | hervorgehobenes Verb |
| `2` | die Lücke (ihr Text ist die erwartete Antwort) |

Die Karten-IDs ändern sich nie, deshalb bleibt der gespeicherte Fortschritt bei Datenänderungen erhalten.

## Quellen

Die Verblisten wurden aus mehreren Lernmaterialien zusammengestellt:

- die Übungen auf deutschlernerblog.de;
- die Verbliste aus *Kontext C1* (Klett);
- die PONS-Liste *Verben mit Präpositionen*;
- *137 Deutsche Präpositionen* von easy-deutsch.de;
- eine Liste zur Rektion der Verben.

Doppelte und rein wörtliche Verbindungen wurden entfernt. Alle Beispielsätze, Dialoge und Übersetzungen wurden eigens für dieses Projekt geschrieben. Die Häufigkeit der Verben stammt aus der Wortliste [FrequencyWords](https://github.com/hermitdave/FrequencyWords) (OpenSubtitles 2018).

## Technik

Reines HTML, CSS und JavaScript, ohne Frameworks und ohne Abhängigkeiten. Die einzigen externen Ressourcen sind die Schriften Onest, IBM Plex Sans Arabic und JetBrains Mono von Google Fonts.

# dna_blog

[English](README.md) | Deutsch

Gibt einem Repo die Regeln und das Template, um zu jedem Ticket einen
Blogbeitrag zu schreiben, und einen Skill, der ihn schreibt.

## Motivation

Ein Ticket ändert oft mehrere Repos. Ohne Regel bleibt offen, welches
Repo über die Änderung schreibt und was im Beitrag stehen darf. Die
Schicht sorgt dafür, dass jedes Repo eines Tickets vor dem Publish seinen
eigenen Beitrag schreibt: aus seiner Sicht, nur über seine eigenen
Änderungen, abgelegt unter `doc/blog/<yyyy>` neben dem Code, den er
beschreibt. Jeder Beitrag lässt sich für sich lesen, ohne zu wissen, wer
auf dem Repo aufbaut.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-blog   # TypeScript projects
dart pub add dev:dna_blog     # Dart projects
helix init
```

`helix init` legt einen Test ab, der die DNA bei jedem Testlauf
instanziiert und prüft. Er legt den Guide in `doc/guides/` ab, das
Template in `doc/templates/` und den Skill in `.claude/skills/blog/`.

Tippe vor dem Publish eines Tickets `/blog` in Claude Code. Der Skill
meldet, ob `doc/blog/<yyyy>` schon einen Beitrag zur Änderung enthält,
schreibt sonst einen nach `doc/blog/<yyyy>/<yyyy>-<mm>-<dd>-<title>.md`
und nennt die Datei zur Durchsicht.

## Guides

- `dna/doc/guides/blog-guide.md` — welche Repos eines Tickets einen
  Beitrag bekommen, was darin stehen darf, wo er abgelegt wird
  (`doc/blog/<yyyy>`) und wie er geschrieben wird: 60–100 Zeilen,
  umbrochen bei 80 Zeichen, Mermaid-Diagramme wo nötig

## Templates

- `dna/doc/templates/blog-template.md` — der Aufbau eines englischen
  Blogbeitrags: Motivation, Strategie, ein Abschnitt pro
  Umsetzungsschritt, Dependency-Updates und offene Punkte

## Skills

- `/blog` — meldet, ob das aktuelle Ticket in diesem Repo noch einen
  Beitrag braucht, und schreibt ihn; folgt dem Blog-Guide

## Umfang

Die Schicht schreibt nur englische Beiträge. Beiträge in anderen Sprachen
übernimmt [dna_translate](https://github.com/ggdna/dna_translate), das
auch das deutsche Template mitliefert. Der Guide verweist auf einen
Publish-Guide und einen Übersetzungs-Guide; er folgt ihnen nur, wenn das
Repo sie aus anderen Schichten hat.

## Schichten

Die Schicht ist orthogonal: `dna/_dna.json` nennt keine Eltern-Schichten.
Sie trägt nur ihr eigenes Thema und wird vom nutzenden Repo oder von der
Umbrella-Schicht seiner Organisation mit anderen Schichten kombiniert.

## Variablen

- `dnaCopyrightHolder` — der Name im Lizenzkopf jeder Datei;
  `mustOverride` in `dna/_dna.json` markiert ihn, daher setzt ihn jedes
  Repo, das diese Schicht einbindet, in seiner eigenen `dna/_vars.json`
- `dnaMermaidMarkdownBlock` — der Code-Fence, in den ein
  Mermaid-Diagramm gesetzt wird

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das
Repo instanziiert seine eigene DNA — nach Änderungen `dart test` laufen
lassen; vorher committen, denn eine Datei, die die DNA überschreiben
würde, darf keine uncommittete Arbeit enthalten.

Bearbeite die Dateien unter `dna/`, nicht ihre Kopien in `doc/` und
`.claude/`, die der Test überschreibt.

## Lizenz

MIT — siehe [LICENSE](LICENSE).

# iPhone Duo UX

Ein Skill für Claude mit den UI/UX-Regeln für Apps auf dem iPhone Duo: Faltzustände, Leistenachse und -kante, Reserved Regions, ArrangementView, StandBy und Widgets, Foundation Models, Punktmaße und Dynamic Type.

Der Skill ist als Prüfinstanz gedacht. Wer einen Screen, ein Rendering, einen Figma-Frame oder ein Konzept fürs Duo baut, bekommt damit die Maße, die Apple wirklich vorgibt, und die Stellen, an denen Apple bis heute schweigt.

## Inhalt

Eine Datei: [`iphone-duo-ux/SKILL.md`](iphone-duo-ux/SKILL.md), zehn Abschnitte.

| Abschnitt | Thema |
| --- | --- |
| 1 | Gerät und Anatomie: Displays, Auflösungen, Posen, Kameras, Touch ID |
| 1a | Design-Ressourcen von Apple und aus der Community |
| 1b | Maße, die Apple wirklich vorgibt (Dynamic Type, Tippziele, Kontrast) |
| 2 | Die sechs Best Practices der HIG als Prüfliste |
| 3 | Reserved Regions: Kamera-Ausschnitte und Falzregion |
| 4 | Split Views und Arrangement Views |
| 5 | Vertical Controls: Achse folgt der Orientierung, Kante ist die Außenkante |
| 6 | Hinge-API, Multitasking, Zugang zum zweiten Display |
| 7 | StandBy, Widgets, Live Activities |
| 8 | Freigaben und Biometrie |
| 9 | Foundation Models in iOS 27 |
| 10 | Arbeitsweise bei Screens und Renderings, zwei Checklisten |

## Installation

Für Claude Code oder Claude Cowork das Verzeichnis in den Skill-Ordner kopieren:

```bash
git clone https://github.com/GodModeAI2025/iPhoneDuo_Concept_Skill.git
cp -R iPhoneDuo_Concept_Skill/iphone-duo-ux ~/.claude/skills/
```

Projektweit statt benutzerweit: `.claude/skills/` im Repository ablegen.

Für Claude.ai lässt sich der Ordner als ZIP packen und als Skill hochladen:

```bash
cd iPhoneDuo_Concept_Skill && zip -r iphone-duo-ux.zip iphone-duo-ux
```

## Verwendung

Der Skill greift, sobald es um Screens, Renderings, Frames, Konzepte oder Prüfungen fürs Duo geht. Typische Einstiege:

- „Prüf diesen Screen gegen die Duo-Regeln.“
- „Welche Punktmaße gelten für das Innendisplay?“
- „Wo darf die Toolbar liegen, wenn das Gerät auf dem Tisch steht?“
- „Baue mir Frames für Figma nach den Duo-Vorgaben.“

## Zwei Dinge, die oft falsch laufen

**Die Punktmaße.** Innen sind es 669 × 951 pt, nicht 626 × 890. Das System rendert in 3x und skaliert auf das Panel herunter, wie früher bei den Plus-Modellen. Wer mit der alten Zahl rechnet, bekommt falsche Spaltenbreiten, falsche Raster und falsche Angaben zum Letterboxing.

**Die Leisten.** Die Achse hängt an der Orientierung, nicht an der Pose: außen immer vertikal, innen im Querformat vertikal, innen hochkant horizontal. Die Kante ist die Außenkante, bei einer einzelnen App also rechts. Nur die linke App eines Paars im Split View hat ihre Controls links.

Beide Punkte sind im Skill mit Quelle und der Notiz belegt, welche frühere Fassung was behauptet hat.

## Belegt, Konzept, Offen, Korrigiert

Jede Aussage im Skill trägt eine dieser vier Kennzeichnungen. Grundlage sind Apples HIG-Seite „Designing for iPhone Duo“, die HIG-Seiten zu Typography, Accessibility, Color und Layout, die Tech Talks 111461 bis 111466, das Newsroom-Material vom 9. September 2026, apple.com/iphone-duo mit den Specs, die Apple Design Resources und die Framework-Referenzen zu iOS 27.

Was Apple nicht dokumentiert, steht als offen drin und nicht als Zahl: die Breite der Falzregion, die Radien der Displayecken, die Maße der seitlichen Dynamic Island, das Verhalten der Tastatur in der Buch-Pose.

Ein offizielles Duo-Kit für Figma oder Sketch gibt es nicht. Wer danach fragt, meint das iOS-27-UI-Kit plus die Maße aus Abschnitt 1b.

## Stand

Geprüft am 18. September 2026. Die Quellenlage ändert sich mit jedem SDK-Update; wer den Skill weiterträgt, sollte die HIG-Seite und die Design Resources gegenlesen.

Ein Lesetrick aus dem Skill, der dabei hilft: Die HIG-Seiten liefern ohne JavaScript nur „requires JavaScript“. Die Inhalte stehen als JSON unter `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/<seitenname>.json`.

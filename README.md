# iPhone Duo UX

Ein Skill für Claude mit den UI/UX- und API-Regeln für das iPhone Duo: Leistenachse und -kante, Reserved Regions, Arrangement, Hinge, Punktmaße, Dynamic Type und Design-Ressourcen.

Der Skill ist als Prüfinstanz gedacht. Wer einen Screen, ein Rendering, einen Figma-Frame oder ein Konzept fürs Duo baut, bekommt damit die Maße, die belegten API-Namen und die Stellen, an denen Apple bis heute schweigt.

Seit dem 18. September 2026 sind die Angaben gegen das SDK 27.1 geprüft. Das verschiebt einiges: Namen aus Talks und Blogposts existieren im SDK teilweise nicht, und Details, die im Alltag zählen, stehen nirgends sonst.

## Inhalt

Eine Datei: [`iphone-duo-ux/SKILL.md`](iphone-duo-ux/SKILL.md), elf Abschnitte.

| Abschnitt | Thema |
| --- | --- |
| 1 | Gerät und Anatomie: Displays, Punktmaße, Posen, Touch ID |
| 1a | Design-Ressourcen von Apple und aus der Community |
| 1b | Maße, die Apple vorgibt (Dynamic Type, Tippziele, Kontrast) |
| 2 | Die sechs Best Practices der HIG als Prüfliste |
| 3 | Reserved Regions: Kamera-Ausschnitte und Falzregion |
| 4 | Split Views und Arrangement |
| 5 | Vertical Controls: Achse folgt der Orientierung, Kante ist die Außenkante |
| 6 | Hinge: Status, Winkel im Bogenmaß, Interaction-Handler |
| 7 | Multitasking und Zugang zum zweiten Display |
| 8 | StandBy, Widgets, Live Activities |
| 9 | Freigaben und Biometrie |
| 10 | Foundation Models in iOS 27 |
| 11 | Arbeitsweise bei Screens und Renderings, drei Checklisten |

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
- „Wie beobachte ich den Faltwinkel, ohne mir einen Retain-Cycle zu bauen?“

## Drei Dinge, die oft falsch laufen

**Die Punktmaße.** Innen sind es 669 × 951 pt, nicht 626 × 890. Beleg ist das Simulatorprofil: Es führt das Innendisplay mit 2007 × 2853 px bei Scale 3, das Panel selbst hat 1878 × 2670 px. Die kursierende Zahl rechnet mit dem Panel statt mit dem Renderpuffer.

**Die Leisten.** Die Achse hängt an der Orientierung, nicht an der Pose: außen immer vertikal, innen im Querformat vertikal, innen hochkant horizontal. Die Kante ist die Außenkante, bei einer einzelnen App also rechts. Nur die linke App eines Paars im Split View hat ihre Controls links. Wählbar ist die Kante nicht, `verticalBarEdge` ist readonly.

**Die API-Namen.** `toolbarVerticalEdge` existiert im SDK 27.1 nicht. `ArrangementView` und `onHingeChange` sind dort ebenfalls nicht auffindbar, die Arbeit läuft über `UIArrangementViewController` und `UIHingeInteraction`. Für Reserved Regions gibt es nur den UIKit-Weg.

## Belegt, Konzept, Offen, Korrigiert

Jede Aussage im Skill trägt eine dieser vier Kennzeichnungen. Grundlage sind Apples HIG-Seiten, die Tech Talks 111461 bis 111466, das Newsroom-Material vom 9. September 2026, apple.com/iphone-duo mit den Specs, die Apple Design Resources und seit dem 18. September 2026 das SDK selbst.

Was Apple nicht dokumentiert, steht als offen drin und nicht als Zahl: die Breite der Falzregion, die Radien der Displayecken, die Maße der seitlichen Dynamic Island, das Verhalten der Tastatur in der Buch-Pose.

Ein offizielles Duo-Kit für Figma oder Sketch gibt es nicht. Wer danach fragt, meint das iOS-27-UI-Kit plus die Maße aus Abschnitt 1b.

## Zwei Lesetricks aus dem Skill

Die HIG-Seiten liefern ohne JavaScript nur „requires JavaScript“. Die Inhalte stehen als JSON unter `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/<seitenname>.json`.

Auf einem Mac mit Xcode schlägt das SDK jede Seite und jeden Talk:

```bash
SDK=$(xcrun --sdk iphoneos --show-sdk-path)
grep -hoE ".{0,90}SYMBOL.{0,90}" "$SDK"/System/Library/Frameworks/{SwiftUI,UIKit}.framework/Modules/*.swiftmodule/arm64e-apple-ios.swiftinterface | sort -u
grep -rn "SYMBOL" "$SDK"/System/Library/Frameworks/UIKit.framework/Headers/
```

Beides prüfen: Eine Swift-Schnittstelle schweigt gelegentlich, während der Objective-C-Header die API führt. Gerätemaße stehen im Simulatorprofil unter `/Library/Developer/CoreSimulator/Profiles/DeviceTypes/`.

## Stand

Geprüft am 18. September 2026 gegen SDK 27.1. Die Quellenlage ändert sich mit jedem SDK-Update; wer den Skill weiterträgt, sollte die HIG-Seite, die Design Resources und die Framework-Schnittstellen gegenlesen.

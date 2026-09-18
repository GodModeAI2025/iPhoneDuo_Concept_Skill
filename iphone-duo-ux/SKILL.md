---
name: iphone-duo-ux
description: "UI/UX- und API-Regeln für das iPhone Duo, gegen SDK 27.1 verifiziert: Leistenachse und -kante, Reserved Regions, Arrangement, Hinge, Punktmaße, Dynamic Type, Design-Ressourcen – nutzen bei Screens, Renderings, Figma/Sketch-Frames, Konzepten oder Prüfungen für das Duo."
---

# iPhone Duo UX – Regeln, Quellen, Prüfmuster

Grundlage sind Apples HIG-Seiten („Designing for iPhone Duo“, Typography, Accessibility, Color, Layout), die Tech Talks 111461–111466, Apple Newsroom vom 9. September 2026, apple.com/iphone-duo(/specs), Apple Design Resources — und seit dem 18. September 2026 das **SDK selbst**. Wo Apple etwas nicht dokumentiert, wird es als Konzept markiert, nie als belegt.

**Zwei Lesetricks, die den Unterschied zwischen Raten und Zitieren machen:**

1. HIG-Seiten liefern ohne JavaScript nur „requires JavaScript“. Die Inhalte stehen als JSON unter `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/<seitenname>.json`.
2. Auf einem Mac mit Xcode ist das SDK die höchste Instanz — höher als jede Seite und jeder Talk. Existiert ein Symbol dort nicht, existiert es nicht:

```
SDK=$(xcrun --sdk iphoneos --show-sdk-path)
grep -hoE ".{0,90}SYMBOL.{0,90}" "$SDK"/System/Library/Frameworks/{SwiftUI,UIKit}.framework/Modules/*.swiftmodule/arm64e-apple-ios.swiftinterface | sort -u
grep -rn "SYMBOL" "$SDK"/System/Library/Frameworks/UIKit.framework/Headers/
```

Beides prüfen: Eine Swift-Schnittstelle kann schweigen, während der Objective-C-Header die API führt — genau so ist es bei Hinge. Gerätemaße stehen im Simulatorprofil unter `/Library/Developer/CoreSimulator/Profiles/DeviceTypes/`. Und `xcrun agent skills export` legt Apples eigene Agent Skills als Markdown ab; **`app-resizability`** ist darunter die offizielle Anleitung fürs Duo („preparing or optimizing an app for the foldable iPhone Duo“) und trägt den Satz, dass sie vorheriges Training überschreibt.

## 1. Gerät und Anatomie

- Zwei Displays mit je eigener Frontkamera. Außen 5,4" (1398×2034 px, 460 ppi), innen 7,6" (Panel laut Specs 1878×2670 px, 430 ppi).
- **Punktmaße (bestätigt):** außen **466×678 pt**, innen **669×951 pt**. Beleg ist `iPhone Duo.simdevicetype/Contents/Resources/capabilities.plist`: Es führt beide integrierten Displays mit 1398×2034 und **2007×2853** px bei `scale 3`, dazu `main-screen-pitch 460`. Das Innendisplay wird also in 3x auf 2007×2853 gerendert und auf das 1878×2670-Panel heruntergerechnet (Faktor ≈ 2,81). Beide Displays kommen auf ≈ 153 pt pro Zoll bzw. 0,166 mm je Punkt; ein 44-pt-Ziel ist ≈ 7,3 mm groß.
- Die Community-Zahl **626×890 pt ist falsch** (1878×2670/3 rechnet mit dem Panel statt mit dem Renderpuffer). Jede Rechnung darauf neu machen.
- Seitenverhältnisse: außen 1,455, innen 1,422. 16:9-Video innen quer: rund 20 % Balken; hochkant bleibt rund 60 % Restfläche.
- Gerätemodell `iPhone19,4`, Produktklasse V68, ab Runtime 27.1. Das Simulatorprofil führt `com.apple.touch-id` — Touch ID im Seitenknopf, kein Face ID. Entsperren auch per Apple Watch.
- Breite der Falzregion, Radien der Displayecken und Maße der seitlichen Dynamic Island: **offen**, in Renderings als stilisierte Zone, nie mit Zahl.
- Die äußere Kamera sitzt in der Ecke, ist immer sichtbar und vertikal mit den seitlichen Controls ausgerichtet. Die innere Kamera liegt hinter dem Display und erscheint nur bei aktiver Kamera.
- Apple Pencil (USB-C) kommt „later this year“, nicht zum Start.
- Posen laut HIG: „partially folded like a book, placed down on a surface, or standing on its edges“. apple.com nennt Landscape, Portrait, Closed, Seated, Standing. Ein „Zelt“ ist keine Pose mit API.
- StandBy startet auf beiden Displays, auch ohne Laden (Newsroom). Inhalte: Uhr, Fotos, Widgets, Live Activities — kein App-UI.
- Newsroom: „Lock Screen controls, the Dock on the Home Screen, and app navigation and controls now appear on the side to maximize vertical space for content.“

## 1a. Design-Ressourcen (geprüft 17. und 18.09.2026)

- Apple Design Resources: „iOS 27 and iPadOS 27“ UI Kit für Figma und Sketch, App-Icon-Templates. **Ein Duo-Kit für Figma oder Sketch gibt es nicht.** Wer danach fragt, meint das iOS-27-Kit plus die HIG-Maße; das ist freundlich richtigzustellen, nicht stillschweigend zu übergehen.
- Product Bezels „iPhone Duo“: nur Photoshop und PNG. Zwei Farben, fünf Ansichten; Innenrahmen 3093×2247 px um einen Ausschnitt von 2853×2007 px mit 120 px Rand, Außenausschnitt 1398×2034 px. Keine gefaltete, keine Tisch- oder Stand-Pose.
- Apple untersagt „Rendering in 3D or creating any simulation of an Apple product“. Also: stilisierte schematische Geräteform oder Apples Bezel-Datei unverändert — nie ein fotorealistischer Nachbau.
- App Store Connect: Screenshots 1398×2034 (außen) und 2007×2853 (innen), beide Orientierungen.
- Community-Kits auf Figma und über 37 GitHub-Repos: inoffiziell, vor dem SDK entstanden, ohne belegte Maße. Nie als Beleg zitieren.
- Eigene Frames: außen 466×678 pt, innen 669×951 pt bzw. 951×669 pt quer.
- Quellen: developer.apple.com/design/resources; 9to5mac.com/2026/09/09/apple-updates-design-resources-with-iphone-duo-and-iphone-18-pro-product-bezels; blakecrosley.com/blog/iphone-duo-day-two.

## 1b. Maße, die Apple vorgibt

In Screens und Renderings wird in Punkten gesetzt und mit ausgewiesenem Faktor skaliert („1 pt = 0,50 px“ unter dem Gerät). Dann sind diese Werte prüfbar:

| Größe | Wert | Herkunft |
| --- | --- | --- |
| Large Title | 34 / 41 pt | HIG Typography, Dynamic Type „Large“ |
| Title 1 · 2 · 3 | 28/34 · 22/28 · 20/25 pt | dieselbe Tabelle |
| Headline · Body | 17 / 22 pt (Headline Semibold) | Standardgröße ist 17 pt |
| Callout · Subhead | 16/21 · 15/20 pt | dieselbe Tabelle |
| Footnote · Caption 1 · 2 | 13/18 · 12/16 · 11/13 pt | **11 pt ist die Untergrenze** |
| Tippziel | 44 × 44 pt | HIG Accessibility; 28 × 28 pt absolutes Minimum |
| Kontrast | 4,5 : 1 bis 17 pt, 3 : 1 ab 18 pt oder fett | HIG Accessibility, WCAG AA |
| systemBlue | #0088FF hell / #0091FF dunkel | HIG Color — Apple rät ab, die Werte fest zu verdrahten; nur fürs Mockup |
| Schrift | SF Pro | HIG Typography; im Web über den System-Stack mit Fallback |
| Seitenrand | 16 pt | Konvention aus dem UI-Kit; die HIG-Layoutseite beziffert sie nicht |
| Leistendicke | 54 pt | Ableitung: 44 pt Ziel plus Luft. Apple nennt keine Zahl |

Farbe darf nie allein eine Information tragen (Diff, Status, Freigabestufe): immer zusätzlich Text, Symbol oder Form.

## 2. Die sechs HIG-Best-Practices

1. Build your app to resize – Size Classes, Layout Margins, Safe Area Insets; keine festen Breiten. Apples Skill `app-resizability` nennt die Altlasten, die dabei weichen müssen: `mainScreen`, `interfaceOrientation`, `userInterfaceIdiom`, Application- statt Scene-Lifecycle.
2. Create a consistent experience across displays – gleiche Funktionen auf beiden Displays; innen darf eine zusätzliche Hierarchieebene erscheinen.
3. Maintain the same functionality across device poses – Talk 111466: „You don't want to tie functionality to a specific pose.“
4. Follow the system's vertical layout – siehe Abschnitt 5.
5. Make your game playable in every device pose – Seitenverhältnis ändern statt Letterboxing.
6. Don't reinvent your app when it resizes.

## 3. Reserved Regions (im SDK 27.1 verifiziert)

- Drei Regionen: äußere Kamera (immer), innere Kamera (nur bei aktiver Kamera), Falzregion (nur teilweise gefaltet; die Mitte fällt weg).
- API: `view.reservedRegions(kind:options:)` liefert `[UIView.ReservedRegion]` mit `id` und `kind`. `UIView.ReservedRegion.Kind` kennt **`.division`** (Falz) und **`.occlusion`** (Kamera); `QueryOptions` kennt **`.includeInactive`**. Flach ist die Division-Region inaktiv mit Breite null. Eine SwiftUI-Entsprechung ist im SDK 27.1 nicht auffindbar — wer sie in SwiftUI braucht, brückt über UIKit.
- Systemkomponenten weichen selbst aus (HIG: „Components like alerts, context menus, and sheets automatically move to account for the fold“).
- Container bevorzugen, die sich selbst anpassen; in Rastern gerade Spaltenzahl; wichtige Elemente aus der Mitte halten; nur bewegen, was nötig ist.
- Scrollender Inhalt muss der Falz nicht ausweichen; Buttons in der Falz sind schwer zu treffen (Talk 111466).
- Displacement (Talk 111463): Buch-Pose → Alerts zur trailing Seite. Auf dem Tisch → oben Inhalt für Lesedistanz, unten interaktive Controls auf der stabilen Fläche (Talk 111466).

## 4. Split Views und Arrangement (im SDK 27.1 verifiziert)

- App-eigener Split View (`NavigationSplitView`/`UISplitViewController`) expandiert innen, kollabiert außen auf eine Spalte.
- **`UIArrangementViewController`** hält genau zwei Views über `ViewPlacement.primary` und `.secondary`. Anordnungen sind `UISplitArrangement` und `UIOverlayArrangement`, beide konform zu `UIArrangementViewController.Arrangement`. Wichtige Methoden: `setViewController(_:for:animated:)`, `viewController(for:)`, `placement(for:)`, `state(for:)`, `setViewProperties(_:for:)`, `updateArrangement(_:animated:)`. Ab iOS 27.1.
- Der SwiftUI-Name `ArrangementView` ist im SDK 27.1 **nicht auffindbar**; wer ihn nennt, kennzeichnet ihn als unbelegt.
- HIG: „Keep navigation outside of arrangement views.“ Keine Arrangement-View in ScrollViews. Nur einsetzen, wenn das Layout ohnehin wie HStack/VStack (split) oder ZStack (overlay) aussieht.

## 5. Vertical Controls – Achse und Kante

**Die Achse folgt der Orientierung, nicht der Pose.** Außen immer vertikal. Innen quer vertikal. Innen hochkant horizontal — HIG: „The exception is the inner display in portrait, which has enough vertical space to keep standard horizontal bars.“ Das gilt in jeder Pose: Auf dem Tisch mit waagrechter Falz steht das Innendisplay hochkant, also bleiben die Bars **horizontal** (Status und Toolbar oben, Tab Bar unten, nichts Tippbares in der Falz). *Korrigiert: Eine frühere Fassung sagte „Bars bleiben auch dort an der Seite“.*

**Die Kante ist die Außenkante, bei einer einzelnen App also rechts.** HIG: „The outer front-facing camera is in the corner and is always visible, vertically aligned with controls on the side.“ Und: „each one places controls along its outer edge, so the left app has controls on the left.“ Weil die Achse an der Hardware hängt, bleibt sie auch in RTL-Sprachen auf derselben Seite. Einzige linke Leiste in einem korrekten Rendering ist die linke App eines Paars. *Korrigiert: Frühere Renderings setzten die Leiste links.*

**Die Kante ist nicht wählbar.** Das SDK führt `UIVerticalBarEdge` mit `Unspecified`, `Leading` und `Trailing` (ab iOS 27.1) — aber `verticalBarEdge` ist **readonly**: „…vertical bar is currently visible“. Man liest die Kante und reagiert über `systemTraitsAffectingVerticalBarEdge` auf Änderungen. *Korrigiert: Eine frühere Fassung nannte `toolbarVerticalEdge` / `verticalBarEdge` als Stellschraube. `toolbarVerticalEdge` existiert im SDK 27.1 überhaupt nicht.*

- An der Seite liegen von oben nach unten: Dynamic Island, Statusleiste, Toolbar (inklusive Navigation), Tab Bar.
- Asymmetrie einplanen: Safe Areas nutzen, auch für die gegenüberliegende Kante in Split View. `safeAreaBar(edge:alignment:spacing:)` in SwiftUI hängt eigene Leisten korrekt in die Safe Area.
- Reihenfolge: oben Navigation (Back, Close), dann prominente Aktionen (Done), dann übrige Gruppen; das System setzt einen Abstand zwischen Elementen der früheren Top- und Bottom-Bar.
- Überlauf von unten nach oben; **`visibilityPriority(_:)`** mit `ToolbarItemVisibilityPriority` (im SDK verifiziert, auf `ToolbarContent` und `CustomizableToolbarContent`) steuert, was bleibt — häufige Aktionen und Elemente mit Badges zuerst.
- Volle Breite nur für nicht scrollende, immersive Layouts (Calculator: 5×4 statt 4×5); Hintergründe dürfen die volle Breite nutzen, scrollender Inhalt bleibt eingerückt.
- Gruppen über ToolbarItemGroup/UIBarButtonItemGroup statt manueller Abstände. Controls beim Inhalt lassen, den sie betreffen.
- Jedes Item mit Titel und Symbol; textbasierte Buttons minimieren, denn Text bleibt in einer horizontalen Bar.
- Bar-Compression: navigationsorientiert → Toolbar-Items ins Überlaufmenü, Tab Bar bleibt; aufgabenorientiert → Tab Bar minimieren, Toolbar bleibt. Dazu `ToolbarOverflowMenu` und `toolbarMinimizeBehavior` (Apples Skill `swiftui-whats-new-27` führt sie).
- Keyboard-Accessory-Bars bleiben an der Tastatur (Talk 111462). Tastaturverhalten in der Buch-Pose: **offen**.

## 6. Hinge (im SDK 27.1 verifiziert, UIKit)

- `UIHinge` ab iOS 27.1 (auch tvOS/visionOS, nicht watchOS): `status` und `angle`. `UIHinge.Status` kennt **vier** Fälle: `.unknown`, `.closed`, `.partiallyOpen`, `.fullyOpen`. Kein Pose-Enum.
- `angle` ist **im Bogenmaß**. Apple warnt ausdrücklich: Rate und Granularität der Updates sind Systempolitik und können sich ändern — wer nur zu/teilweise/offen braucht, nimmt `status`, nicht den Winkel.
- Beobachtet wird über `UIHingeInteraction(updateHandler:)`, per `view.addInteraction(_:)` an eine View gehängt. Der Handler bekommt `UIHingeInteraction.Update`; dessen **`hinge` ist optional und wird nil**, sobald die Interaktion eine Hierarchie verlässt, die Hinge-Updates liefert — diesen Fall behandeln. Der Handler wird gespeichert und entkommt: Retain-Cycles vermeiden. `enabled` schaltet ab; währenddessen werden Updates **nicht** nachgereicht, beim Wiedereinschalten kommt der aktuelle Zustand.
- Eine SwiftUI-Entsprechung (`onHingeChange`) ist im SDK 27.1 nicht auffindbar. *Korrigiert: Eine frühere Fassung führte sie als API.*
- Apple: Hinge-Daten für Interaktionen und Effekte; fürs Layout die Arrangement- und Region-APIs.

## 7. Multitasking und zweites Display

- Split View: zwei Apps nebeneinander, 50/50, App-Paare speicherbar, zwei Fenster derselben App, Drag-and-drop zwischen Apps. Auf dem Außendisplay können keine neuen Fenster erzeugt werden; `UIWindowScene.ActivationAction` blendet sich dort aus.
- Zweites Display für Drittanbieter nur über Scene Accessories: **`CameraCaptureAccessory<Content>: SceneAccessoryContent`** (SwiftUI, im SDK verifiziert) im `.sceneAccessory` — aber nur, solange die App innen im Vollbild läuft und eine Kamera-Session aktiv ist; Verfügbarkeit über `onAvailabilityChange`, UIKit `registerSceneAccessory(_:)`. Ohne Kamera gibt es keinen Weg auf das Außendisplay.

## 8. Außerhalb der App (StandBy, Widgets, Live Activities)

- StandBy zeigt zwei kleine Widgets nebeneinander skaliert oder eine Live Activity; nach Tipp die Lock-Screen-Darstellung bildschirmfüllend (`isActivityFullscreen`). Live Activities: kein Netzzugriff, max. 4 KB, bis 8 Stunden; Updates aus der App im Hintergrund oder per Push.
- Auf gesperrtem Gerät sind Buttons und Toggles in Widgets und Live Activities inaktiv. Freigaben deshalb nie auf Sperrbildschirm oder StandBy legen, sondern auf Home-Screen-Widgets (`Button(intent:)`, iOS 17) oder in die App. Den inaktiven Zustand zeigen und begründen, nicht verstecken.
- Tippziele schrumpfen nicht, weil die Fläche klein ist: auch im Widget gelten 44 pt.
- ControlWidget (iOS 18) für Kontrollzentrum, Sperrbildschirm und Aktionstaste; `LiveActivityIntent` startet eine Live Activity ohne App im Vordergrund. Timeline-Refresh per `WidgetCenter.reloadTimelines`, Budget grob 40–70 pro Tag; Widget-Extension ohne Modell, Inhalte vorberechnen.
- Hintergrundaudio: `AVAudioSession` `.record`/`.playAndRecord` plus `UIBackgroundModes` „audio“ nimmt weiter auf, wenn der Bildschirm sperrt; oranger Mikrofonpunkt. Ob SpeechAnalyzer im Hintergrund weiterläuft: **offen**.

## 9. Freigaben und Biometrie

- LocalAuthentication: Der Dialog ist Systemsache; anpassbar sind nur `localizedReason`, `localizedCancelTitle`, `localizedFallbackTitle`. Keine Positions-API auf iOS. Der Reason-Text wiederholt den Umfang, weil der Dialog Inhalt verdeckt.
- Muster: Stufe 1 (reversibel) per Tipp im Chat, Stufe 2 (irreversibel: löschen, senden, zahlen) zusätzlich per Touch ID im Seitenknopf. Die Freigabe eines Tool-Aufrufs gehört in `Tool.call(arguments:)`, wo der Aufruf auf die Entscheidung wartet; `onToolCall` im DynamicProfile ist nur ein Beobachtungs-Hook (Abbruch per Throw).

## 10. Foundation Models (iOS 27) – belegte Fakten

- `SystemLanguageModel` auf dem Gerät (Kontext 4K laut Doku, 8192 laut Session 241), kein Reasoning, unbegrenzt. `PrivateCloudComputeLanguageModel`: 32K Kontext, Reasoning `light`/`moderate`/`deep`, Tageslimit mit `quotaUsage` (`isLimitReached`, `status`, `resetDate`, `limitIncreaseSuggestion`), Entitlement `com.apple.developer.private-cloud-compute`; Zugang nur für Entwickler im App Store Small Business Program mit unter 2 Mio. Erstdownloads.
- `LanguageModel`- und `LanguageModelExecutor`-Protokolle für fremde Modelle; Anthropic- und Google-Swift-Pakete angekündigt („soon“), Bedrock nirgends genannt.
- `ToolCallingMode`: `.allowed` (Default), `.required`, `.disallowed`. `DynamicProfile` mit `model`, `reasoningLevel`, `toolCallingMode`, `historyTransform` und Hooks `onPrompt`, `onToolCall`, `onToolOutput`, `onResponse`. `rollingWindow` und `Skills` kommen aus foundation-models-utilities (experimentell).
- `Attachment` nur für Bilder (CGImage, CIImage, CVPixelBuffer, URL), kein Audio. LoRA-Adapter-Toolkit endet mit 26.0.0 und ist mit 27 inkompatibel.
- `LongRunningIntent` verlängert App Intents über 30 s hinaus, Fortschritt erscheint automatisch als Live Activity, Hintergrund-GPU möglich.
- Evaluations-Framework mit `TrajectoryExpectation`, Swift-Testing-Integration; `fm`-CLI in macOS 27; Python-SDK `apple_fm_sdk`; Foundation-Models-Instrument in Instruments.
- Verfügbarkeit: `SystemLanguageModel.availability` mit `appleIntelligenceNotEnabled`, `deviceNotEligible`, `modelNotReady`. Apple Intelligence in der EU seit iOS 18.4; Siri AI auf 27 in der EU ohne Zeitplan ausgesetzt.
- Umfeld: SpeechAnalyzer/SpeechTranscriber/DictationTranscriber (iOS 26); Vision `RecognizeDocumentsRequest` (iOS 26) und `RecognizeTextRequest` (iOS 18); VisionKit `DataScannerViewController` (iOS 16); PencilKit `PKCanvasView`; EventKit Full Access (iOS 17).

## 11. Arbeitsweise bei Screens und Renderings

- Jede Szene bekommt Haltung, Aufgabe, Umsetzungs-Hinweis mit API-Namen und eine Kennzeichnung je Aussage: Belegt (Quelle nennen), Konzept, Offen, Korrigiert.
- Keine Hände oder Finger, keine Apple-Logos, keine 3D-Modelle; Geräteform stilisiert; PNGs mindestens 2x.
- **Regeln ableiten statt zeichnen.** Wo ein Renderer Leistenachse und -kante aus Display und Orientierung berechnet und die Falz als eigene Raster-Spalte führt, kann kein einzelnes Panel sie falsch haben. Das schlägt jede Sichtprüfung über dreißig Screens.
- **Vor jeder API-Aussage das SDK fragen**, wenn ein Mac mit Xcode da ist. Talks und Blogposts nennen Namen, die es nicht gibt (`toolbarVerticalEdge`), und schweigen über Details, die zählen (`Status.unknown`, das nil-bare `hinge`). Ein negativer Fund in der Swift-Schnittstelle ist kein Beweis — erst die ObjC-Header dazunehmen.
- Verhaltens-Checkliste: Leisten an der richtigen Achse *und* Kante? Falz frei von Buttons? Gleiche Funktionen in jeder Pose? Freigabe-Tasten nicht auf gesperrten Flächen? Außendisplay nur mit Kamera-Accessory? StandBy nur Widgets/Live Activity? Tastatur-Verhalten nicht als belegt ausgegeben?
- Maß-Checkliste: Frames 466×678 und 669×951 pt? Nirgends 626×890? Seitenverhältnisse 1,455 und 1,422? Falzbreite, Eckradien, Dynamic-Island-Maße ohne Zahl? Geräterahmen stilisiert oder unveränderte Apple-Bezels, kein 3D? Keine Behauptung eines offiziellen Duo-Figma- oder Sketch-Kits?
- Apple-Maß-Checkliste: Jede Textzeile auf einem Dynamic-Type-Stil, nichts unter 11 pt? Tippziele 44 pt in der Tipprichtung, auch in Widgets? Systemfarben und Label-Stufen statt eigener Palette, hell wie dunkel? SF Pro über den System-Stack? Kontrast 4,5 : 1 bis 17 pt? Farbe nirgends allein als Träger einer Information?
- Kursierende Community-Renderings mit horizontalen Tabs im Querformat, Karten über der Falz oder App-UI in StandBy sind falsch.
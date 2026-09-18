---
name: iphone-duo-ux
description: "UI/UX-Regeln für Apps auf dem iPhone Duo: Faltzustände, Leistenachse und -kante, Reserved Regions, ArrangementView, StandBy, Widgets, Foundation Models, Punktmaße, Dynamic Type und Design-Ressourcen – nutzen bei Screens, Renderings, Figma/Sketch-Frames, Konzepten oder Prüfungen für das Duo."
---

# iPhone Duo UX – Regeln, Quellen, Prüfmuster

Grundlage ist Apples HIG-Seite „Designing for iPhone Duo“ (https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo, neu am 9. September 2026), dazu die HIG-Seiten Typography, Accessibility, Color und Layout, die Tech Talks 111461–111466, Apple Newsroom vom 9. September 2026, apple.com/iphone-duo(/specs), Apple Design Resources und die Framework-Referenzen zu iOS 27. Vor jeder Aussage zu einem Screen gilt: erst die HIG-Seite lesen, dann die Szene dagegen prüfen. Wo Apple etwas nicht dokumentiert, wird es als Konzept markiert, nie als belegt.

**Lesetrick:** Die HIG-Seiten liefern ohne JavaScript nur „requires JavaScript“. Die Inhalte stehen als JSON unter `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/<seitenname>.json` — so sind Tabellen und wörtliche Sätze zitierfähig zu bekommen.

## 1. Gerät und Anatomie (HIG, Newsroom, Specs)

- Zwei Displays mit je eigener Frontkamera. Außen 5,4" (1398×2034 px, 460 ppi), innen 7,6" (Panel laut Specs 1878×2670 px, 430 ppi; App-Store-Screenshots und Bildschirmausschnitt der Bezels 2007×2853 px).
- Punktmaße dokumentiert Apple nicht, beide Werte sind Ableitungen und so zu kennzeichnen. Außen 466×678 pt (1398×2034 / 3). Innen 669×951 pt (2007×2853 / 3): Das System rendert in 3x und skaliert auf das 1878×2670-Panel herunter (Faktor ≈ 2,81, wie früher bei den Plus-Modellen). Gegenprobe: Beide Displays kommen damit auf ≈ 153 pt pro Zoll bzw. 0,166 mm je Punkt, ein 44-pt-Tippziel ist außen wie innen ≈ 7,3 mm groß, und die Diagonalen treffen die Specs auf 0,03”. Die ältere Community-Zahl 626×890 pt (1878×2670 / 3) ist überholt; jede Rechnung darauf (Spaltenbreiten, 16:9-Letterboxing, Rastermaße) neu machen (Crosley, „Day Two“).
- Seitenverhältnisse: außen 2034/1398 = 1,455, innen 2853/2007 = 2670/1878 = 1,422. Beide Innenwerte haben dasselbe Verhältnis; ein Rahmen im Verhältnis 626:890 ist geometrisch richtig, nur seine Beschriftung und alles in Punkten Gerechnete ist falsch. 16:9-Video innen im Querformat: rund 20 % schwarze Balken; hochkant bleibt rund 60 % Restfläche.
- Breite der Falzregion, Radien der Displayecken und Maße der seitlichen Dynamic Island dokumentiert Apple nicht (Offen); in Renderings als stilisierte Zone, nie mit Zahl.
- Die äußere Kamera sitzt in der Ecke, ist immer sichtbar und vertikal mit den seitlichen Controls ausgerichtet. Die innere Kamera liegt hinter dem Display und erscheint nur bei aktiver Kamera.
- Touch ID sitzt im Seitenknopf, offen wie geschlossen; kein Face ID. Entsperren auch per Apple Watch.
- Apple Pencil (USB-C) kommt „later this year“, nicht zum Start.
- Abschnitte der HIG-Seite: Anatomy, Device poses, Best practices, Dynamic layouts, Reserved regions, Split views, Arrangement views, Vertical controls, Resources. Zur Tastatur, zur inneren Dynamic Island und zur Tisch-Pose als eigenem Layout sagt die HIG nichts.
- Posen laut HIG: „partially folded like a book, placed down on a surface, or standing on its edges“ (Illustration mit sechs Posen). apple.com nennt Landscape, Portrait, Closed, Seated, Standing. Ein „Zelt“ ist bei Apple keine Pose mit API (nur ein Nebensatz in Talk 111461: „set the phone down like a tent“ als Argument für Landscape-Support).
- StandBy: „Set iPhone Duo down and it enters StandBy on either the outer or inner display — even when it's not charging“ (Newsroom). Inhalte in StandBy sind Uhr, Fotos, Widgets und Live Activities – kein App-UI.
- Newsroom: „Lock Screen controls, the Dock on the Home Screen, and app navigation and controls now appear on the side to maximize vertical space for content.“ Die Dynamic Island liegt vertikal an der Seite beider Displays.

## 1a. Design-Ressourcen von Apple und aus der Community (geprüft am 18.09.2026)

- Apple Design Resources, Abschnitt iOS & iPadOS: „iOS 27 and iPadOS 27“ UI Kit für Figma (Community-Datei 1651309003795292092) und Sketch, dazu App-Icon-Templates für Figma, Sketch, Photoshop und Illustrator. **Ein eigenes Duo-Kit für Figma oder Sketch gibt es nicht** — zweimal geprüft, am 17. und 18. September 2026. Wer nach „den Duo-Vorgaben für Figma/Sketch“ fragt, meint das iOS-27-Kit plus die HIG-Maße aus Abschnitt 1b; das ist freundlich richtigzustellen, nicht stillschweigend zu übergehen.
- Product Bezels „iPhone Duo“: Bezel-iPhone-Duo.dmg, nur Photoshop und PNG. Zwei Farben (Night Sky, Star White), fünf Ansichten: innen offen im Quer- und Hochformat, außen geschlossen im Quer- und Hochformat, Außenansicht mit Kamera-Ausschnitt. Innenrahmen 3093×2247 px um einen Bildschirmausschnitt von 2853×2007 px mit 120 px Rand; Außenausschnitt 1398×2034 px. Keine Pose „teilweise gefaltet“, keine Tisch- oder Stand-Pose im Paket (9to5Mac, Crosley).
- Nutzung laut Apple: Bezels nur für Mockups von Apps auf Apple-Plattformen gemäß Marketing Resources and Identity Guidelines; untersagt ist „Rendering in 3D or creating any simulation of an Apple product“. Folge für Renderings: entweder stilisierte, eindeutig schematische Geräteform oder Apples Bezel-Datei unverändert, nie ein nachgebautes fotorealistisches Gerät oder 3D-Modell.
- App Store Connect: Screenshot-Größen iPhone Duo 1398×2034 (außen) und 2007×2853 (innen), jeweils in beiden Orientierungen.
- Community-Kits auf Figma (u. a. „iPhone Duo – iOS 27 UI Kit“ von Axel Bergqvist, „iPhone Duo Mockup“, „iOS 27 with unfold Portrait“, gespiegelt bei TitanUI): inoffiziell, vor dem SDK entstanden, Lizenz meist nur privat, ohne belegte Maße. Nie als Beleg zitieren. Über 37 GitHub-Repositories mit Fold-Animationen und SwiftUI-Beispielen kompilieren nicht gegen echte Duo-APIs (Crosley).
- Eigene Frames anlegen: außen 466×678 pt, innen 669×951 pt (hochkant) bzw. 951×669 pt (quer), alle als Ableitung beschriftet; Komponenten aus dem offiziellen iOS-27-Kit, Präsentationsrahmen aus dem Bezel-Paket.
- Quellen: developer.apple.com/design/resources; 9to5mac.com/2026/09/09/apple-updates-design-resources-with-iphone-duo-and-iphone-18-pro-product-bezels; blakecrosley.com/blog/iphone-duo-day-two.

## 1b. Maße, die Apple wirklich vorgibt

In Screens und Renderings wird in Punkten gesetzt und mit einem ausgewiesenen Faktor skaliert („1 pt = 0,50 px“ unter dem Gerät). Dann sind diese Werte einhaltbar und prüfbar:

| Größe | Wert | Herkunft |
| --- | --- | --- |
| Large Title | 34 / 41 pt | HIG Typography, Dynamic Type „Large“ |
| Title 1 · 2 · 3 | 28/34 · 22/28 · 20/25 pt | dieselbe Tabelle |
| Headline · Body | 17 / 22 pt (Headline Semibold) | dieselbe Tabelle; 17 pt ist die Standardgröße |
| Callout · Subhead | 16/21 · 15/20 pt | dieselbe Tabelle |
| Footnote · Caption 1 · 2 | 13/18 · 12/16 · 11/13 pt | dieselbe Tabelle; **11 pt ist die Untergrenze** |
| Tippziel | 44 × 44 pt | HIG Accessibility: empfohlene Größe; 28 × 28 pt absolutes Minimum |
| Kontrast | 4,5 : 1 bis 17 pt, 3 : 1 ab 18 pt oder fett | HIG Accessibility, WCAG AA |
| systemBlue | #0088FF hell / #0091FF dunkel | HIG Color — Apple rät ausdrücklich davon ab, die Werte fest zu verdrahten; nur fürs Mockup verwenden, in Code die APIs |
| Schrift | SF Pro | HIG Typography; im Web über den System-Stack mit ehrlichem Fallback |
| Seitenrand | 16 pt | Konvention aus dem iOS-27-UI-Kit; die HIG-Layoutseite beziffert sie nicht |
| Leistendicke | 54 pt | Ableitung: 44 pt Tippziel plus Luft. Für die vertikale Leiste nennt Apple keine Zahl |

Farbe darf nie allein eine Information tragen (Diff, Status, Freigabestufe): immer zusätzlich Text, Symbol oder Form.

## 2. Die sechs HIG-Best-Practices (wörtlich als Prüfliste)

1. Build your app to resize – Size Classes, Layout Margins, Safe Area Insets; keine festen Breiten, keine Display-Abhängigkeiten. Compact width außen, regular width innen decken alle Posen ab.
2. Create a consistent experience across displays – gleiche Funktionen und Zustände auf beiden Displays; innen darf eine zusätzliche Hierarchieebene erscheinen (Mail: außen Liste oder Mail, innen beides nebeneinander).
3. Maintain the same functionality across device poses – Controls dürfen überlaufen, Inhalt darf sich verschieben, aber nichts darf nur in einer Pose erreichbar sein. Talk 111466: „You don't want to tie functionality to a specific pose.“
4. Follow the system's vertical layout for toolbars, tab bars, and navigation controls – siehe Abschnitt 5.
5. Make your game playable in every device pose – Seitenverhältnis ändern statt Letterboxing.
6. Don't reinvent your app when it resizes – bestehendes Layout wachsen lassen.

## 3. Reserved Regions (HIG „Dynamic layouts“)

- Drei Regionen: äußere Kamera (immer, wächst zur Dynamic Island für Live Activities), innere Kamera (nur bei aktiver Kamera; das UI weicht dann aus), Falzregion (nur wenn teilweise gefaltet; teilt das Innendisplay in nutzbare Regionen, die Mitte fällt weg).
- Systemkomponenten passen sich automatisch an (HIG: „Components like alerts, context menus, and sheets automatically move to account for the fold“). Eigene Komponenten nutzen die Reserved-Region-APIs: SwiftUI `proxy.reservedRegions(kind: .division)` bzw. `.occlusion`, Option `.includeInactive`; UIKit `view.reservedRegions(kind:)`. Wenn flach: Division-Region inaktiv mit Breite null.
- „Adapt your layout when the device folds“: Container bevorzugen, die sich selbst anpassen (Notes-Split-View); in Rastern gerade Spaltenzahl; wichtige Elemente aus der Mitte halten.
- „Avoid extreme layout changes as people fold the device“: nur bewegen, was nötig ist. Scrollender Inhalt (Artikel, Feeds, Dokumente, Listen) muss der Falz nicht ausweichen; Buttons in der Falz sind schwer zu treffen (Talk 111466).
- Displacement-Regel aus Talk 111463: Buch-Pose → Alerts wandern zur trailing Seite (näher am Außendisplay beim Schließen). Auf dem Tisch abgestellt → oben Inhalt für Lesedistanz, unten interaktive Controls („more stable surface for touch“). Talk 111466: „iPhone Duo is great for hands-free experiences when seated on a table. Media can sit at the top while tappable controls live on a stable base at the bottom.“ Ein spezielles Layout für diese Pose ist optional, muss aber alle Controls und dieselbe Hierarchie behalten.

## 4. Split Views und Arrangement Views (HIG)

- Split View der App (NavigationSplitView/UISplitViewController) expandiert innen und kollabiert außen auf eine Spalte, wie regular/compact auf anderen iPhones.
- ArrangementView hält genau zwei Views (primary, secondary) und ordnet sie nach Größe, Orientierung und Reserved Regions. Split teilt horizontal, wenn breiter als hoch, sonst vertikal; Achsen einschränkbar (`.split.axes(.horizontal)`). Overlay legt primary über secondary; teilweise gefaltet belegen beide je eine Seite. `overlayArrangementZIndex` aus dem Environment; UIKit `UIArrangementViewController`. Verfügbar ab iOS 27.1.
- HIG: „Keep navigation outside of arrangement views“ – NavigationStack, NavigationSplitView, TabView um die ArrangementView herum, nicht hinein. Keine ArrangementView in ScrollViews. Nur einsetzen, wenn das Layout bereits wie HStack/VStack (→ split) oder ZStack (→ overlay) aussieht.

## 5. Vertical Controls – Achse und Kante (HIG)

**Die Achse folgt der Orientierung, nicht der Pose.** Außen immer vertikal. Innen im Querformat vertikal. Innen hochkant horizontal — HIG: „The exception is the inner display in portrait, which has enough vertical space to keep standard horizontal bars.“ Das gilt in jeder Pose: Auf dem Tisch mit waagrechter Falz steht das Innendisplay hochkant, also bleiben die Bars **horizontal** (Status und Toolbar oben, Tab Bar unten, nichts Tippbares in der Falz). Liegt die Falz senkrecht (Buch, quer), liegen sie an der Seite. *Korrigiert: Eine frühere Fassung dieser Datei sagte „Bars bleiben auch dort an der Seite“.*

**Die Kante ist die Außenkante, bei einer einzelnen App also rechts.** Belege: „The outer front-facing camera is in the corner and is always visible, vertically aligned with controls on the side.“ Und für zwei Apps: „when two apps share the inner display with Split View multitasking, each one places controls along its outer edge, so the left app has controls on the left.“ Weil die Achse an der Hardware hängt, bleibt sie auch in RTL-Sprachen auf derselben Seite. Einzige linke Leiste in einem korrekten Rendering ist die linke App eines Paars. *Korrigiert: Frühere Renderings setzten die Leiste links.*

- An der Seite liegen von oben nach unten: Dynamic Island, Statusleiste, Toolbar (inklusive Navigation), Tab Bar.
- Asymmetrie einplanen: Safe Areas nutzen, auch für die gegenüberliegende Kante in Split View. Controls über Posen hinweg an ähnlicher Position halten.
- Reihenfolge: oben Navigation (Back, Close), dann prominente Aktionen (Done), dann übrige Gruppen; das System setzt einen Abstand zwischen Elementen der früheren Top- und Bottom-Bar.
- Überlauf von unten nach oben; `visibilityPriority` (ToolbarItemVisibilityPriority / UIBarButtonItemVisibilityPriority) steuert, was bleibt – häufig genutzte Aktionen (Compose, New Note) und Elemente mit Badges zuerst erhalten.
- **Default-Platzierung nicht überschreiben.** `toolbarVerticalEdge` / `verticalBarEdge` ist zum Abweichen da, nicht zum Herstellen des Normalfalls. Volle Breite nur für nicht scrollende, immersive Layouts (Calculator: 5×4 statt 4×5); Hintergründe dürfen die volle Breite nutzen, scrollender Inhalt bleibt eingerückt.
- Gruppen über ToolbarItemGroup/UIBarButtonItemGroup statt manueller Abstände. Controls beim Inhalt lassen, den sie betreffen (Mail: Listen-Controls über der Liste, Mail-Controls an der trailing Kante).
- Jedes Item mit Titel und Symbol; textbasierte Buttons minimieren, denn Text bleibt in einer horizontalen Bar.
- Bar-Compression: navigationsorientiert → Toolbar-Items ins Überlaufmenü, Tab Bar bleibt (Default); aufgabenorientiert → Tab Bar minimieren, Toolbar bleibt. APIs: `toolbarVerticalCompressionBehavior(.prefersToolbarItems)` / `verticalBarCompressionBehavior`; Systemüberlauf mit `ToolbarOverflowMenu` / `additionalOverflowItems`; Achse mit `.axisBehavior(.verticalPreferred|.horizontalOnly)`; abschalten mit `toolbarVerticalBehavior(.disabled)`. Voraussetzung: Build gegen das aktuelle SDK.
- Keyboard-Accessory-Bars bleiben an der Tastatur, wandern nicht in die vertikale Achse (Talk 111462). Wie sich die Tastatur in der Buch-Pose verhält, dokumentiert Apple nicht – ein geteiltes Keyboard ist Konzept.

## 6. Hinge, Multitasking, zweites Display

- Hinge: SwiftUI `.onHingeChange { previous, context in … }`, UIKit `UIHingeInteraction`; `hinge.status` ist `.closed`, `.partiallyOpen`, `.fullyOpen`, dazu kontinuierlicher `angle`. Kein Pose-Enum. Apple: Hinge-Daten für Interaktionen und Effekte, für Layout die Arrangement- und Region-APIs.
- Split View: zwei Apps nebeneinander, 50/50, App-Paare speicherbar, zwei Fenster derselben App, Drag-and-drop zwischen Apps (Newsroom, apple.com). Auf dem Außendisplay können keine neuen Fenster erzeugt werden; `UIWindowScene.ActivationAction` blendet sich dort aus.
- Zweites Display für Drittanbieter nur über Scene Accessories: `CameraCaptureAccessory` im `.sceneAccessory` zeigt eigene UI auf dem Außendisplay, aber nur wenn die App innen im Vollbild läuft und eine Kamera-Session aktiv ist; Verfügbarkeit über `onAvailabilityChange`, UIKit `registerSceneAccessory(_:)`. Ohne Kamera gibt es keinen Weg auf das Außendisplay.

## 7. Was außerhalb der App geht (StandBy, Widgets, Live Activities)

- StandBy zeigt zwei kleine Widgets nebeneinander skaliert oder eine Live Activity: minimal am Rand, nach Tipp die Lock-Screen-Darstellung bildschirmfüllend (`isActivityFullscreen`). Live Activities haben keinen Netzzugriff, maximal 4 KB Daten, laufen bis 8 Stunden; Updates aus der App im Hintergrund oder per Push.
- Auf gesperrtem Gerät sind Buttons und Toggles in Widgets und Live Activities inaktiv – Aktionen erst nach Entsperren. Freigaben deshalb nie auf Sperrbildschirm oder StandBy legen, sondern auf Home-Screen-Widgets (`Button(intent:)`, iOS 17) oder in die App. Der inaktive Zustand wird gezeigt und begründet, nicht versteckt.
- Tippziele schrumpfen nicht, weil die Fläche klein ist: auch im Widget gelten 44 pt.
- ControlWidget (iOS 18) für Kontrollzentrum, Sperrbildschirm und Aktionstaste; `LiveActivityIntent` startet eine Live Activity aus einem Control ohne App im Vordergrund. Timeline-Refresh per `WidgetCenter.reloadTimelines`, Budget grob 40–70 Reloads pro Tag; Widget-Extension ohne Modell, Inhalte vorberechnen.
- Hintergrundaudio: `AVAudioSession` `.record`/`.playAndRecord` plus `UIBackgroundModes` „audio“ nimmt weiter auf, wenn der Bildschirm sperrt; oranger Mikrofonpunkt. Ob SpeechAnalyzer im Hintergrund weiterläuft, sagt Apple nicht.

## 8. Freigaben und Biometrie

- LocalAuthentication: Dialog ist Systemsache; anpassbar sind nur `localizedReason`, `localizedCancelTitle`, `localizedFallbackTitle`. Keine Positions-API auf iOS. Der Reason-Text muss den Umfang wiederholen, damit die Freigabe lesbar bleibt, denn der Dialog überdeckt Inhalt.
- Muster: Stufe 1 (reversibel) per Tipp im Chat, Stufe 2 (irreversibel: löschen, senden, zahlen) zusätzlich per Touch ID im Seitenknopf. Die Freigabe eines Tool-Aufrufs gehört in `Tool.call(arguments:)`, wo der Aufruf auf die Entscheidung wartet; `onToolCall` im DynamicProfile ist nur ein Beobachtungs-Hook (Abbruch per Throw).

## 9. Foundation Models (iOS 27) – belegte Fakten

- `SystemLanguageModel` auf dem Gerät (Kontext 4K laut Doku, 8192 laut Session 241), kein Reasoning, unbegrenzt. `PrivateCloudComputeLanguageModel`: 32K Kontext, Reasoning `light`/`moderate`/`deep`, Tageslimit mit `quotaUsage` (`isLimitReached`, `status`, `resetDate`, `limitIncreaseSuggestion`), Entitlement `com.apple.developer.private-cloud-compute`; Zugang nur für Entwickler im App Store Small Business Program mit unter 2 Mio. Erstdownloads.
- `LanguageModel`- und `LanguageModelExecutor`-Protokolle für fremde Modelle; Anthropic- und Google-Swift-Pakete angekündigt („soon“), Bedrock nirgends genannt.
- `ToolCallingMode`: `.allowed` (Default), `.required`, `.disallowed`. `DynamicProfile` mit `model`, `reasoningLevel`, `toolCallingMode`, `historyTransform` und Hooks `onPrompt`, `onToolCall`, `onToolOutput`, `onResponse`. `rollingWindow` und `Skills` kommen aus dem Paket foundation-models-utilities (experimentell).
- `Attachment` nur für Bilder (CGImage, CIImage, CVPixelBuffer, URL), kein Audio. LoRA-Adapter-Toolkit endet mit Version 26.0.0 und ist mit 27 inkompatibel.
- `LongRunningIntent` verlängert App Intents über 30 s hinaus, Fortschritt erscheint automatisch als Live Activity, Hintergrund-GPU möglich.
- Evaluations-Framework mit `TrajectoryExpectation` (ordered/unordered/disallowed, Matcher exact/naturalLanguage/keyOnly/range/contains), Swift-Testing-Integration; `fm`-CLI in macOS 27; Python-SDK `apple_fm_sdk`; Foundation-Models-Instrument in Instruments.
- Verfügbarkeit: `SystemLanguageModel.availability` mit `appleIntelligenceNotEnabled`, `deviceNotEligible`, `modelNotReady`. Apple Intelligence ist in der EU seit iOS 18.4 verfügbar; Siri AI auf iOS/iPadOS/watchOS 27 in der EU ohne Zeitplan ausgesetzt; zu Foundation Models/PCC in der EU gibt es keine eigene Aussage.
- Umfeld: SpeechAnalyzer/SpeechTranscriber/DictationTranscriber (iOS 26) live und on-device; Vision `RecognizeDocumentsRequest` (Tabellen, Belege, iOS 26) und `RecognizeTextRequest` (iOS 18); VisionKit `DataScannerViewController` (iOS 16); PencilKit `PKCanvasView` und `PKDrawing.image(from:scale:)`; EventKit Full Access für Termine und Erinnerungen (iOS 17).

## 10. Arbeitsweise bei Screens und Renderings

- Jede Szene bekommt Haltung, Aufgabe, Umsetzungs-Hinweis mit API-Namen und eine Kennzeichnung je Aussage: Belegt (Quelle nennen), Konzept, Offen, Korrigiert.
- Keine Hände oder Finger, keine Apple-Logos, keine 3D-Modelle; Geräteform stilisiert; PNGs mindestens 2x.
- **Regeln ableiten statt zeichnen.** Wo ein Renderer die Leistenachse und -kante aus Display und Orientierung berechnet und die Falz als eigene Raster-Spalte führt, kann kein einzelnes Panel sie falsch haben. Das ist einer Sichtprüfung über viele Screens deutlich überlegen.
- Vor dem Rendern die Verhaltens-Checkliste: Leisten an der richtigen Achse *und* Kante? Falz frei von Buttons? Gleiche Funktionen in jeder Pose? Freigabe-Tasten nicht auf gesperrten Flächen? Außendisplay nur mit Kamera-Accessory? StandBy nur Widgets/Live Activity? Tastatur-Verhalten nicht als belegt ausgegeben?
- Maß-Checkliste: Frames 466×678 und 669×951 pt, beschriftet als Ableitung? Nirgends 626×890 oder daraus gerechnete Werte? Seitenverhältnisse 1,455 außen und 1,422 innen? Falzbreite, Eckradien, Dynamic-Island-Maße ohne Zahl? Geräterahmen stilisiert oder unveränderte Apple-Bezels, kein 3D? Keine Behauptung eines offiziellen Duo-Figma- oder Sketch-Kits?
- Apple-Maß-Checkliste: Jede Textzeile auf einem Stil der Dynamic-Type-Tabelle, nichts unter 11 pt? Tippziele 44 pt in der Tipprichtung, auch in Widgets? Systemfarben und Label-Stufen statt eigener Palette, hell wie dunkel? SF Pro über den System-Stack? Kontrast 4,5 : 1 bis 17 pt? Farbe nirgends allein als Träger einer Information?
- Quellen, deren Referenzseiten noch fehlen (Hinge, ArrangementView, CameraCaptureAccessory), mit dem Wortlaut der Tech Talks belegen und das sagen. Kursierende Community-Renderings mit horizontalen Tabs im Querformat, Karten über der Falz oder App-UI in StandBy sind falsch.
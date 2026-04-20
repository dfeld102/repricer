BQool Repricer Tool

Ein einfaches, browserbasiertes Tool zur Verwaltung und zum Export von Repricing-Regeln für BQool. Entwickelt für Amazon-Seller die mehrere Marktplätze gleichzeitig betreiben.

🚀 Live-App
URL: https://dfeld102.github.io/repricer

Läuft auf jedem Gerät mit Browser — PC, Handy, Tablet. Kein Login, keine Installation notwendig.

📋 Funktionen

Produkte verwalten — SKU, ASIN, Marktplatz, Repricing-Regel, Min/Max-Preis hinzufügen, bearbeiten und löschen
4 Marktplätze — Amazon DE, ES, IT, FR mit jeweils eigenen Regeln und Preisen
BQool-konformer Export — generiert eine .txt-Datei im exakten Format das BQool erwartet
Export-Status — bereits exportierte Produkte werden markiert und beim nächsten Export übersprungen
Export zurücksetzen — global per Button oder einzeln per Klick auf die Status-Badge
Supabase Cloud-Sync — Daten werden in der Cloud gespeichert und sind auf allen Geräten nach einem Refresh verfügbar
Offline-Fallback — App funktioniert auch ohne Internetverbindung mit den zuletzt geladenen Daten
Mobile-ready — Karten-Layout auf kleinen Bildschirmen, Touch-freundliche Buttons
Suche & Filter — nach SKU oder ASIN suchen, nach Marktplatz filtern
Validierung — Min-Preis muss kleiner als Max-Preis sein, Pflichtfelder werden geprüft

📁 Projektstruktur

repricer/
├── index.html        # Gesamte App (HTML + CSS + JS in einer Datei)
└── README.md         # Diese Dokumentation


Die gesamte App ist in einer einzigen index.html gebündelt — kein Build-Prozess, keine Dependencies, keine Node.js-Installation notwendig.

🔧 Technischer Stack

| Komponente | Technologie |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Hosting | GitHub Pages (kostenlos) |
| Datenbank | Supabase (PostgreSQL, kostenlos) |
| Versionierung | GitHub |

🗄️ Datenbank (Supabase)
Projekt: dfeld102's Project
Region: West EU (Ireland)
Tabelle: products

Die Tabelle speichert alle Produkte als JSON-Array in einer einzigen Zeile (jsonb-Spalte). Das vereinfacht das Lesen und Schreiben erheblich.

create table products (
  id uuid primary key default genrandomuuid(),
  data jsonb not null,
  updated_at timestamp with time zone default now()
);


📤 BQool Export-Format

Die exportierte .txt-Datei folgt exakt dem BQool-Format:

FileType = repricing	Version = 1.2.5 (Please do not edit this line...)
Channel	SellerSKU	Cost	Additional Cost	Rule Name	Min Price	Max Price	Shipping	add-delete	Group	Enable Repricing
Amazon DE	MEIN-SKU-123			Meine Regel	19.99	29.99			1


Trennzeichen: Tab (\t)
Encoding: UTF-8 ohne BOM
Cost / Additional Cost / Shipping / add-delete / Group: werden leer gelassen
Enable Repricing: immer 1

🔄 Workflow

Produkt bei A1 / ProfitGo analysieren
Einkauf erfassen (Einkaufspreis, SKU, ASIN)
Min/Max-Preis anhand Breakeven und Ziel-/Mindestmarge selbst setzen
Produkt im Repricer Tool eintragen
CSV exportieren → in BQool hochladen
BQool aktiviert die Repricing-Regeln automatisch

🛠️ Updates & Wartung

Wenn du die App aktualisieren möchtest:

Änderungen in der index.html vornehmen
Auf GitHub hochladen: index.html → Stift ✏️ → Code einfügen → Commit changes
Ca. 1-2 Minuten warten
Hard Refresh im Browser: Strg + Shift + R

📱 App auf dem Handy speichern

https://dfeld102.github.io/repricer im Handy-Browser öffnen
Teilen-Button → „Zum Home-Bildschirm hinzufügen"
Die App erscheint als Icon auf dem Homescreen — verhält sich wie eine native App

📌 Wichtige Links

Live-App: https://dfeld102.github.io/repricer
GitHub Repository: https://github.com/dfeld102/repricer
Supabase Dashboard: https://supabase.com/dashboard
BQool Repricer: https://www.bqool.com

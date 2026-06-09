# test-changelog-quality-gate

Testprojekt für **Option 2 — Quality Gate**.

Der Agent prüft bei jedem PR ob der Entwickler `lib/CHANGELOG.mdx` aktualisiert hat. Falls nicht — wird der PR blockiert und Claude liefert einen Vorschlag als Kommentar.

## Ablauf

```
1. Branch erstellen und Story-Datei ändern
2. PR öffnen
        │
        ├── CHANGELOG.mdx aktualisiert? → PR wird durchgelassen ✅
        │
        └── CHANGELOG.mdx NICHT aktualisiert?
                │
                ▼
            Claude generiert Vorschlag als PR-Kommentar
            PR wird blockiert ❌
            Entwickler kopiert Vorschlag in CHANGELOG.mdx
            Neuer Commit → PR wird durchgelassen ✅
```

## Endlosschleifen-Schutz

Da der Agent nichts in die Dateien schreibt — nur prüft und kommentiert — entsteht keine Endlosschleife.

## Setup

1. `ANTHROPIC_API_KEY` unter **Settings → Secrets → Actions** hinterlegen
2. Optional: Branch Protection Rule aktivieren damit der Quality Gate Check required ist

```
Repository → Settings → Branches → Add rule → main
→ Require status checks → changelog-quality-gate
```

## Testen

**Szenario A — PR ohne Changelog-Update (sollte blockieren):**
```bash
git checkout -b test/button-update
# Änderung in lib/components/ui/Button/index.stories.tsx machen
# CHANGELOG.mdx NICHT anfassen
git add lib/components/ui/Button/index.stories.tsx
git commit -m "feat: update Button stories"
git push origin test/button-update
# PR öffnen → Agent blockiert PR und postet Vorschlag
```

**Szenario B — PR mit Changelog-Update (sollte durchlassen):**
```bash
git checkout -b test/button-update-with-changelog
# Story-Datei ändern UND CHANGELOG.mdx aktualisieren
git add .
git commit -m "feat: update Button stories + changelog"
git push origin test/button-update-with-changelog
# PR öffnen → Agent lässt PR durch ✅
```
# test-changelog-quality-gate

Testprojekt für **Option 2 — Quality Gate**.

Der Agent prüft bei jedem PR ob der Entwickler `lib/CHANGELOG.mdx` aktualisiert hat. Falls nicht — wird der PR blockiert und Claude liefert einen Vorschlag als Kommentar.

## Ablauf

```
1. Branch erstellen und Story-Datei ändern
2. PR öffnen
        │
        ├── CHANGELOG.mdx aktualisiert? → PR wird durchgelassen ✅
        │
        └── CHANGELOG.mdx NICHT aktualisiert?
                │
                ▼
            Claude generiert Vorschlag als PR-Kommentar
            PR wird blockiert ❌
            Entwickler kopiert Vorschlag in CHANGELOG.mdx
            Neuer Commit → PR wird durchgelassen ✅
```

## Endlosschleifen-Schutz

Da der Agent nichts in die Dateien schreibt — nur prüft und kommentiert — entsteht keine Endlosschleife.

## Setup

1. `ANTHROPIC_API_KEY` unter **Settings → Secrets → Actions** hinterlegen
2. Optional: Branch Protection Rule aktivieren damit der Quality Gate Check required ist

```
Repository → Settings → Branches → Add rule → main
→ Require status checks → changelog-quality-gate
```

## Testen

**Szenario A — PR ohne Changelog-Update (sollte blockieren):**
```bash
git checkout -b test/button-update
# Änderung in lib/components/ui/Button/index.stories.tsx machen
# CHANGELOG.mdx NICHT anfassen
git add lib/components/ui/Button/index.stories.tsx
git commit -m "feat: update Button stories"
git push origin test/button-update
# PR öffnen → Agent blockiert PR und postet Vorschlag
```

**Szenario B — PR mit Changelog-Update (sollte durchlassen):**
```bash
git checkout -b test/button-update-with-changelog
# Story-Datei ändern UND CHANGELOG.mdx aktualisieren
git add .
git commit -m "feat: update Button stories + changelog"
git push origin test/button-update-with-changelog
# PR öffnen → Agent lässt PR durch ✅
```

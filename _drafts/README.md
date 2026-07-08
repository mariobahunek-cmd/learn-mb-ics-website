# _drafts/ — Review-Gate für Academy-Blog-Posts

**Blog-Posts der MB-ICS Academy gehen NICHT automatisch live.** Sie durchlaufen
Marios Freigabe.

## Ablauf

1. Neue Post-Entwürfe landen hier in `_drafts/` (als `YYYY-MM-DD-slug-<lang>.md`,
   DE+EN als Paar mit gemeinsamem `translation_key`). Alles hier wird vom
   Jekyll-Build **ignoriert** (kein `--drafts`-Flag; zusätzlich `_drafts/` in
   `_config.yml` unter `exclude`) → **nicht öffentlich sichtbar**.
2. Mario sieht die wartenden Drafts in **Mission Control → Blog-Approval**
   (`mc.sapprep.de/blog-approval`, Quelle `learn-draft`).
3. **Approve** feuert den Workflow `publish-drafts.yml` (nur `workflow_dispatch`,
   **kein** Cron/Auto-Publish): der älteste Draft wird samt `translation_key`-
   Pärling nach `_posts/` verschoben, Datum gesynct, Permalink injiziert,
   committet & gepusht → GitHub Pages baut. **Reject** löscht den Draft.

## Wichtig

- **Kein 2×/Woche-Auto-Publish.** Der Workflow hat bewusst keinen `schedule:`.
- Nichts in `_drafts/` geht ohne aktive Freigabe live.
- Diese Datei ist nur Doku/Platzhalter, damit der Ordner im Repo existiert.

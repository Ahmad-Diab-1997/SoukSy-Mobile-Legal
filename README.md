# legal-site — die öffentlichen Rechtsseiten

Drei statische Seiten, die Google Play **außerhalb** der App verlangt:

| Datei | Wofür in der Play Console |
|---|---|
| `privacy.html` | App-Inhalt → Datenschutzerklärung (Pflicht) |
| `delete-account.html` | App-Inhalt → Löschung des Kontos (Pflicht, sobald die App Konten anlegt) |
| `index.html` | Einstiegsseite, verlinkt beide |
| `style.css` | gemeinsame Hülle |

## Warum ein eigenes Repo

Dieses Projekt-Repo ist **privat und bleibt privat**. GitHub Pages auf einem
privaten Repo braucht einen bezahlten Plan, und die Datenschutzerklärung muss
für jeden ohne Login erreichbar sein. Deshalb: die Quelle lebt hier (versioniert
zusammen mit dem Code, den sie beschreibt), veröffentlicht wird eine Kopie in
einem **separaten öffentlichen Repo**.

Beim Ändern also immer hier bearbeiten und dann kopieren, nie nur drüben.

## Veröffentlichen

1. Auf GitHub ein neues **öffentliches** Repo anlegen, z. B. `souksy-legal`.
   Kein README, kein .gitignore, leer.
2. Die vier Dateien aus diesem Ordner hineinkopieren und pushen:

```bash
git clone https://github.com/<user>/souksy-legal.git
cp store-assets/legal-site/*.html store-assets/legal-site/*.css souksy-legal/
cd souksy-legal && git add . && git commit -m "privacy policy and account deletion" && git push
```

3. Im neuen Repo: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`** → Save.
4. Nach ein bis zwei Minuten sind die URLs live:

```
https://<user>.github.io/souksy-legal/
https://<user>.github.io/souksy-legal/privacy.html
https://<user>.github.io/souksy-legal/delete-account.html
```

5. Beide URLs in einem privaten Browserfenster öffnen — sie müssen **ohne Login**
   laden. Google prüft genau das, und eine Seite hinter einem Login lässt die
   App-Inhalt-Prüfung durchfallen.

## Beim Ändern zu beachten

- Datum und Version stehen in `privacy.html` von Hand in der `.meta`-Zeile. Sie
  werden nicht automatisch gesetzt: eine Seite, die das heutige Datum druckt,
  behauptet jeden Tag aufs Neue, heute geprüft worden zu sein.
- Jeder Satz beschreibt, was die App **heute** tut. Wenn Push-Nachrichten,
  Analytics, Werbung oder eine GPS-Ortung dazukommen, muss diese Seite **vor**
  dem Release mitwachsen — und das Data-Safety-Formular in der Play Console
  gleich mit. Beide müssen dasselbe sagen, sonst ist es ein Policy-Verstoß.
- Die Kontaktadresse steht in allen drei Dateien und muss zu `SUPPORT_EMAIL` in
  `src/features/support/constants/support.ts` und zur Kontaktadresse im
  Play-Eintrag passen.

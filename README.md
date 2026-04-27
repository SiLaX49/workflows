# workflows

Workflows GitHub Actions réutilisables pour mes projets.

## `security-scan.yml` 🛡️

Analyse de sécurité **language-agnostic** : secrets, dépendances, image Docker, SAST, IaC.
Produit un **score 0–100** avec graphique Mermaid dans le résumé du workflow + remontée
SARIF dans l'onglet Security du repo.

### Outils utilisés

| Outil | Couvre |
|---|---|
| **Gitleaks** | Secrets dans le code et dans l'historique git |
| **Trivy FS** | CVE dans les dépendances (`requirements.txt`, `package.json`, `go.mod`, etc.) + misconfig IaC |
| **Trivy Image** | CVE dans l'image Docker (OS + libs) — si Dockerfile présent |
| **Semgrep** | SAST multi-langage : OWASP Top 10, security-audit, secrets |

### Score

Base 100. Pénalités cumulées par finding :
- Critical : −10
- High : −5
- Medium : −2
- Low : −0.5

Échelle : 🟢 ≥85 Excellent · 🟡 ≥60 Correct · 🟠 ≥30 À améliorer · 🔴 <30 Critique

### Utilisation minimale

`.github/workflows/security.yml` dans n'importe quel repo :

```yaml
name: Security
on: [push, pull_request]

jobs:
  scan:
    uses: SiLaX49/workflows/.github/workflows/security-scan.yml@main
```

### Avec options

```yaml
jobs:
  scan:
    uses: SiLaX49/workflows/.github/workflows/security-scan.yml@main
    with:
      scan-docker: true
      fail-on-score-below: 60   # 0 = ne jamais échouer (défaut)
```

---

## `python-ci.yml`

Pipeline CI Python : ruff (lint) + pytest + build Docker. Voir le fichier pour les inputs.

```yaml
jobs:
  ci:
    uses: SiLaX49/workflows/.github/workflows/python-ci.yml@main
```

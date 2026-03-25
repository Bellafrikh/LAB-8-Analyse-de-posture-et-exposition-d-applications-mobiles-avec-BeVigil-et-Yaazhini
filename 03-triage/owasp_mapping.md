# Mapping OWASP - DIVA Android

## FIND-001: Communication HTTP non sécurisée
- **Catégorie OWASP**: MASVS-NETWORK
- **Référence spécifique**: V5.1 (Data in transit)
- **Justification**: L'utilisation de HTTP expose les PIN et identifiants à des interceptions en clair sur le réseau.

## FIND-003: Sauvegarde Android activée (allowBackup)
- **Catégorie OWASP**: MASVS-STORAGE
- **Référence spécifique**: V2.8 (System Backup)
- **Justification**: Permet d'extraire les données privées de l'application via des outils de sauvegarde système.

## FIND-005: Utilisation risquée du stockage externe
- **Catégorie OWASP**: MASVS-STORAGE
- **Référence spécifique**: V2.1 (Sensitive data storage)
- **Justification**: Les données sensibles sont stockées sur la carte SD, les rendant accessibles à toutes les autres applications.

## FIND-006: Injection SQL potentielle
- **Catégorie OWASP**: MASVS-CODE
- **Référence spécifique**: V7.1 (Injection Flaws)
- **Justification**: L'application ne purifie pas les entrées utilisateur avant de les envoyer à la base de données SQLite.

## FIND-009: JavaScript activé dans WebView
- **Catégorie OWASP**: MASVS-PLATFORM
- **Référence spécifique**: V4.3 (WebView security)
- **Justification**: Activer JavaScript augmente les risques d'exécution de scripts malveillants (XSS).

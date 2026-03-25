# Notes d'analyse BeVigil - DIVA (Analyse Réelle)

## Ce qui est certain
- **Injection SQL (CWE-89)** : Présence de requêtes SQL non paramétrées (Sévérité LOW selon BeVigil, mais critique en réalité).
- **Fuite d'info via Logs (CWE-532)** : Des données sensibles sont écrites dans les logs système (Logcat).
- **Hardcoded Credentials** : Des secrets potentiels (clés/mots de passe) sont détectés dans le fichier strings.xml.
- **Permissions Risquées** : L'application demande l'accès en écriture et lecture au stockage externe (WRITE_EXTERNAL_STORAGE, READ_EXTERNAL_STORAGE).

## Ce qui est hypothèse
- Un attaquant ayant accès physiquement ou via une autre app au téléphone pourrait extraire des données privées de la base SQLite ou des logs.

## Points d'intérêt
- Fichier strings.xml : contient 3 correspondances suspectes de secrets.
- Fichier classes.dex : compilé avec dx/dexmerge, ce qui est standard pour les vieux APKs.

## Domaines et sous-domaines
- Aucun domaine spécifique détecté (App de test locale).

## Endpoints et APIs
- Présence d'URLs et de chemins de fichiers internes détectés dans les ressources.

## Permissions Détectées
- **android.permission.WRITE_EXTERNAL_STORAGE** (RISKY)
- **android.permission.READ_EXTERNAL_STORAGE** (RISKY)
- **android.permission.INTERNET** (SAFE)

## Technologies détectées
- **Librairies tierces** : Android Support Library, Support v4, Support v7.
- **Compilateur** : dx (possible dexmerge).

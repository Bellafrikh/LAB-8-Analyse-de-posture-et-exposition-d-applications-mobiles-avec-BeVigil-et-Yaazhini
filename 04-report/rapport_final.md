# Rapport d'analyse de sécurité mobile - DIVA

## A. Informations générales
- **Date**: 2026-03-25
- **Analyste**: Zaynab Bellafrikh
- **Cible**: DIVA (Damned Insecure Vulnerable Application)
- **Version/Hash**: 5CEFC51FCE9BD760B92AB2340477F4DDA84B4AE0C5D04A8C9493E4FE34FAB7C5
- **Outils utilisés**: BeVigil Cloud Portal, Yaazhini v.1.3.2

## B. Résumé exécutif
L'analyse a révélé 8 vulnérabilités majeures, allant d'un niveau de risque élevé à faible. L'application présente des failles critiques de communication réseau et de configuration système (mode débogage, sauvegardes non sécurisées). Le niveau de risque global est jugé ÉLEVÉ, nécessitant une révision immédiate des protocoles de transmission et de stockage des données.

## C. Top 5 constats

### 1. Insecure communication - FIND-001
- **Sévérité**: High (CVSS: 8.1)
- **Preuve**: jakhar\aseem\diva\APICreds2Activity.java ligne 23
- **Impact**: Interception des identifiants/PIN en clair sur le réseau.
- **Remédiation**: Utiliser exclusivement le protocole HTTPS/TLS.
- **Référence OWASP**: MASVS-NETWORK-5.1

### 2. Android debuggable enabled - FIND-002
- **Sévérité**: Medium (CVSS: 4.9)
- **Preuve**: AndroidManifest.xml ligne 7
- **Impact**: Permet l'extraction de données et la manipulation de l'app en cours d'exécution.
- **Remédiation**: Définir android:debuggable="false".
- **Référence OWASP**: MASVS-CODE-7.1

### 3. Android backup vulnerability - FIND-003
- **Sévérité**: Medium (CVSS: 4.9)
- **Preuve**: AndroidManifest.xml ligne 7
- **Impact**: Extraction facilitée des données privées de l'utilisateur via ADB.
- **Remédiation**: Définir android:allowBackup="false".
- **Référence OWASP**: MASVS-STORAGE-2.8

### 4. Improper export of providers - FIND-004
- **Sévérité**: Medium (CVSS: 4.9)
- **Preuve**: AndroidManifest.xml ligne 36 (NotesProvider)
- **Impact**: Accès non autorisé aux notes privées par d'autres applications.
- **Remédiation**: Définir android:exported="false".
- **Référence OWASP**: MASVS-PLATFORM-4.1

### 5. Insecure Data Storage (External) - FIND-005
- **Sévérité**: Warning
- **Preuve**: InsecureDataStorage4Activity.java ligne 24
- **Impact**: Les données sensibles (.uinfo.txt) sont lisibles par toutes les apps sur la carte SD.
- **Remédiation**: Utiliser le stockage interne privé (/data/data).
- **Référence OWASP**: MASVS-STORAGE-2.1

## D. Faux positifs notables
- **Clés de test dans Strings** : Bien que BeVigil ait détecté des "Secrets", il s'agit principalement de PIN de test pour l'exercice DIVA.

## E. Recommandations prioritaires
1. **Migrer vers HTTPS** : Sécuriser toutes les transmissions réseau immédiatement.
2. **Durcir le Manifest** : Désactiver les flags de débogage, de sauvegarde et l'exportation des providers.
3. **Sécuriser le stockage** : Déplacer les données du stockage externe vers le stockage interne sécurisé.

## F. Annexes
- [01-bevigil/bevigil_notes.md]
- [02-yaazhini/Lab8_analyse_diva.html]
- [03-triage/triage.csv]

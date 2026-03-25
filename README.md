# Rapport de Laboratoire : Analyse de Sécurité d'une Application Mobile (APK)

## Informations Générales
- **Analyste :** Zaynab Bellafrikh
- **Établissement :** EMSI
- **Cible :** DIVA (Damned Insecure Vulnerable Application)
- **Objectif :** Identifier les vulnérabilités par analyse OSINT et statique (SAST).

---

## Outils Utilisés
* **BeVigil :** Analyse de la surface d'attaque externe et fuites de données.
* **Yaazhini :** Analyse statique du code source décompilé.
* **PowerShell :** Gestion de l'arborescence et automatisation de la traçabilité.

---

## Étapes du Projet

### Étape 0 — Initialisation de l'environnement
Mise en place de l'arborescence de travail pour garantir une structure d'audit professionnelle.
- Création des dossiers `00-scope` à `04-report`.
- Initialisation du journal de bord `commands.log`.

<img width="863" height="283" alt="image" src="https://github.com/user-attachments/assets/a52790b4-506d-49e9-9df8-351a3c85313d" />

<img width="1255" height="368" alt="image" src="https://github.com/user-attachments/assets/83bf7618-966a-4896-8be1-caa395423b7a" />

<img width="1600" height="106" alt="image" src="https://github.com/user-attachments/assets/7bdc5f9b-9a4b-4796-82eb-33cb05fc8382" />

### Étape 1 — Définition du périmètre (Scope)
Identification précise de la cible.
- Hash SHA-256 de `diva.apk` documenté pour garantir l'intégrité de la cible.
- Rédaction du fichier `scope.md`.

<img width="1600" height="106" alt="image" src="https://github.com/user-attachments/assets/70a879d0-d568-44f9-a9f3-0ffd353d0ae6" />

<img width="1073" height="592" alt="image" src="https://github.com/user-attachments/assets/a820de9a-4d4d-4c5d-a1b5-f7182167bf69" />

<img width="1600" height="119" alt="image" src="https://github.com/user-attachments/assets/6bb4e66c-e5bb-487b-8474-a54523f9a14b" />


### Étape 2 — Traçabilité et informations d'analyse
Préparation du fichier `analyse_info.txt` contenant les métadonnées de l'audit (date, outils, versions).

<img width="1282" height="332" alt="image" src="https://github.com/user-attachments/assets/85508764-c1ba-499a-bc35-e52cdf7c26a0" />


### Étape 3 — Démarrage BeVigil
Utilisation du portail CloudSEK BeVigil pour scanner l'APK.
- Importation du fichier sur la plateforme.
- Surveillance de l'extraction des métadonnées.

<img width="1600" height="831" alt="image" src="https://github.com/user-attachments/assets/8083792f-f09f-4b6e-8763-28fed3341363" />

<img width="887" height="513" alt="image" src="https://github.com/user-attachments/assets/a328ec8d-7c90-4334-a123-4cb4995f8471" />

<img width="1547" height="402" alt="image" src="https://github.com/user-attachments/assets/489e4a59-c63f-4669-87bb-25b0e88f039d" />

![WhatsApp Image 2026-03-24 at 23 19 16](https://github.com/user-attachments/assets/9f524909-9343-4bb0-bd97-175365493e4b)

<img width="1600" height="73" alt="image" src="https://github.com/user-attachments/assets/1284f594-0592-4735-bfd9-4efaf790f18d" />

<img width="1600" height="166" alt="image" src="https://github.com/user-attachments/assets/2619712a-27be-4709-a2d1-5c429452c0c0" />

### Étape 4 — Collecte BeVigil : Endpoints et Secrets
Analyse des résultats fournis par BeVigil.
- Identification des **risky permissions** (Storage).
- Détection d'une **Injection SQL** potentielle.
- Création du fichier `bevigil_notes.md`.

<img width="1600" height="615" alt="image" src="https://github.com/user-attachments/assets/1bac026b-ef5a-4f38-bfd3-6f68cc4eba00" />

<img width="1600" height="68" alt="image" src="https://github.com/user-attachments/assets/ab4f71c3-7e95-4a16-8b7b-620ee9a17f6a" />

### Étape 5 — Démarrage Yaazhini (SAST)
Lancement de l'outil d'analyse statique local.
- Décompilation de l'APK DIVA.
- Génération d'un rapport complet au format HTML.

<img width="1122" height="757" alt="image" src="https://github.com/user-attachments/assets/7750ac6d-fcd7-4a3a-950e-911d70674e47" />

<img width="601" height="520" alt="image" src="https://github.com/user-attachments/assets/613968bb-7525-4a9b-8118-45d89a02f630" />

<img width="1600" height="840" alt="image" src="https://github.com/user-attachments/assets/997f5864-076e-4c7b-b953-ebbaf89ff23c" />

<img width="1600" height="168" alt="image" src="https://github.com/user-attachments/assets/dbfc2ccc-5ef6-4153-993b-e34fc9bb5bef" />


### Étape 6 — Collecte Yaazhini : Indices d'exposition
Exploration approfondie du code source.
- Localisation précise de la **communication HTTP** non sécurisée.
- Identification du mode **Debuggable** et du **allowBackup**.
- Rédaction de `yaazhini_notes.md`.

<img width="1600" height="725" alt="image" src="https://github.com/user-attachments/assets/d3d0ff98-7254-4150-8e9d-cb8d03e81e14" />

<img width="1600" height="98" alt="image" src="https://github.com/user-attachments/assets/87e4c1b2-034f-4a68-8a87-d348326538d3" />


### Étape 7 — Normalisation et dédoublonnage
Consolidation des données dans `triage.csv`.
- Fusion des résultats BeVigil et Yaazhini.
- Attribution d'un ID unique à chaque vulnérabilité (FIND-001 à FIND-010).

<img width="1600" height="375" alt="image" src="https://github.com/user-attachments/assets/6d48a79f-95c4-49cd-8c61-cb42205bad51" />

### Étape 8 — Corrélation avec OWASP MASVS
Liaison des failles trouvées aux standards de l'industrie.
- Mapping avec les catégories **MASVS-NETWORK**, **MASVS-STORAGE**, etc.
- Rédaction du fichier `owasp_mapping.md`.

<img width="1600" height="616" alt="image" src="https://github.com/user-attachments/assets/c3ef3f00-9a08-4ccd-9a13-8006662fbfa2" />

### Étape 9 — Rédaction du Rapport Final
Synthèse de l'audit dans `rapport_final.md`.
- Établissement du Top 5 des constats les plus critiques.
- Définition de recommandations prioritaires (Migration HTTPS, durcissement du Manifest).

<img width="1600" height="817" alt="image" src="https://github.com/user-attachments/assets/d1ea25f4-854b-4b6b-b87c-ea720d62f4e6" />

<img width="1600" height="73" alt="image" src="https://github.com/user-attachments/assets/7403cba0-ba65-46b1-bf6e-2ec960a4ecc0" />

### Étape 10 — Nettoyage et Clôture
Contrôle qualité final.
- Masquage des données sensibles ([MASQUÉ]).
- Signature de la `checklist_fin.md`.

<img width="1600" height="608" alt="image" src="https://github.com/user-attachments/assets/60348594-ce35-445f-bfc1-c2d3a3dcdff8" />

<img width="1672" height="715" alt="image" src="https://github.com/user-attachments/assets/855af21c-30c7-43f9-a8f5-db1e00dc186c" />

<img width="1057" height="815" alt="image" src="https://github.com/user-attachments/assets/8f03d0b0-326c-4aa3-b311-90344875d576" />

---

## Constats Majeurs
1. **Communication HTTP en clair** (Risque d'interception réseau).
2. **Flag Debuggable activé** (Manipulation de l'app possible).
3. **Backup Android autorisé** (Extraction des données via ADB).
4. **Permissions de stockage excessives** (Accès carte SD).
5. **Injection SQL** (Requêtes non paramétrées).

---
*Fin du rapport de laboratoire.*

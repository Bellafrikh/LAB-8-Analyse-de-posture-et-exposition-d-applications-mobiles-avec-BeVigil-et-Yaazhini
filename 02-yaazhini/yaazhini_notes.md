# Notes d'analyse Yaazhini - DIVA (Analyse Statique)

## Éléments identifiés

### Élément 1: Communication non sécurisée (HTTP)
- **Localisation**: Fichier \jakhar\aseem\diva\APICreds2Activity.java\ à la ligne 23.
- **Description**: Yaazhini a détecté une URL utilisant le protocole non sécurisé http:// au lieu de https://.
- **Impact potentiel**: Les données transmises (identifiants, PIN) peuvent être interceptées en clair par un attaquant sur le réseau (attaque Man-In-The-Middle).
- **Remédiation suggérée**: Utiliser exclusivement le protocole HTTPS avec TLS pour toutes les communications réseau.

### Élément 2: Mode Débogage activé (Debuggable)
- **Localisation**: Fichier \AndroidManifest.xml\ à la ligne 7.
- **Description**: La propriété android:debuggable='true' est présente dans la balise <application>.
- **Impact potentiel**: Un attaquant peut attacher un débogueur à l'application en cours d'exécution pour extraire des données ou modifier le comportement de l'app.
- **Remédiation suggérée**: Définir android:debuggable="false" dans le fichier Manifest pour les versions de production.

### Élément 3: Vulnérabilité de sauvegarde Android (Backup Enabled)
- **Localisation**: Fichier \AndroidManifest.xml\ à la ligne 7.
- **Description**: La propriété android:allowBackup='true' est activée.
- **Impact potentiel**: Permet à n'importe qui ayant accès au téléphone via ADB d'extraire les données privées de l'application (/data/data/jakhar.aseem.diva).
- **Remédiation suggérée**: Désactiver la sauvegarde en réglant android:allowBackup="false".

### Élément 4: Exportation incorrecte de Content Provider
- **Localisation**: Fichier \AndroidManifest.xml\ à la ligne 36.
- **Description**: Le composant NotesProvider est marqué avec android:exported="true".
- **Impact potentiel**: Des applications tierces malveillantes installées sur le même appareil peuvent lire ou modifier les notes stockées par DIVA.
- **Remédiation suggérée**: Définir android:exported="false" si le partage de données avec d'autres apps n'est pas nécessaire.

### Élément 5: Utilisation risquée du stockage externe
- **Localisation**: Fichier \jakhar\aseem\diva\InsecureDataStorage4Activity.java\ à la ligne 24 (et 8 autres occurrences).
- **Description**: L'application utilise getExternalStorageDirectory() pour stocker des fichiers comme .uinfo.txt.
- **Impact potentiel**: Les fichiers sur la carte SD sont accessibles en lecture/écriture par toutes les autres applications et par l'utilisateur.
- **Remédiation suggérée**: Utiliser le stockage interne privé de l'application pour les données sensibles.

### Élément 6: JavaScript activé dans la WebView (Bonus)
- **Localisation**: Fichier \jakhar\aseem\diva\InputValidation2URISchemeActivity.java\ à la ligne 14.
- **Description**: La fonction setJavaScriptEnabled(true) est appelée sur une WebView.
- **Impact potentiel**: Risque élevé d'exécution de code arbitraire via des attaques Cross-Site Scripting (XSS).
- **Remédiation suggérée**: Désactiver JavaScript si possible ou auditer rigoureusement le code chargé.

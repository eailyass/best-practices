## The components:

### Asset: 
		- gère la génération des URL et le versionning des web assets (CSS, JS, Images...)
		- Plusieurs stratégies de versionnage: emptyVersionStrategy = pas de version, staticVersionStrategy= version avec prefix (v1, v2...), JsonManifestVersionStrategy = version gérée par un fichier JSON

### BrowserKit:
		- Permet la simulation d'un navigateur, la soumission automatique des formulaires... pour effectuer des tests fonctionnels
		- 

### Cache component:
		- gère les besoins en cache respecte PSR-6 et cache contracts





## Architecture (3.4):


App: appkernel.php  / Config
Bin: console et executables
Src: Code PHP
Vendor: Compsantes tierces géré exclusivement par composer - a ne pas toucher
Web: the public files app.php CSS, JS etc...  + the front cotroller : app.php & app_dev.php   *****  in version 4 the front cotroller is index.php in public/ directory

Everything in symfony is a bundle

to reference a bundle's file in a logical way use @bundleName/path_to_file


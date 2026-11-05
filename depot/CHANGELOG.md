# Historique des versions

Les versions sont numérotées `Vx.xx` : `x` est le numéro majeur, `xx` avance
d'un cran à chaque modification du code.

## [Non publié]

### Nouveautés

- Chaque renommage dit ce qui l'a imposé : la longueur mesurée et la limite
  en vigueur (`nom trop long : 126 car. pour 120 autorisés → 120`), les
  caractères interdits trouvés, le nom réservé… Dans le journal, le rapport
  texte et la nouvelle colonne `explication` du CSV. Le journal affichait
  auparavant la longueur du chemin complet même quand seul le nom était trop
  long.
- Option **Créer un manifeste SHA-256** (Réglages…, groupe Sécurité, cochée
  par défaut) : impose la vérification de chaque copie.
- **Contrôler avec le manifeste SHA-256…** (menu Outils) : relit une sauvegarde, des
  mois après, sans le serveur d'origine : taille d'abord, puis empreinte
  SHA-256 recalculée sur le disque. On peut y choisir la sauvegarde, son
  dossier `_RAPPORT_COPICOL` ou l'un de ses sous-dossiers : la sauvegarde
  est retrouvée en remontant. Le rapport `rapport_controle_<date>`
  distingue les fichiers intacts, altérés, manquants, sans empreinte et
  absents du manifeste (jamais supprimés), et les erreurs de lecture. Libre.
- **Manifeste d'empreintes** `_RAPPORT_COPICOL\empreintes.csv` (UTF-8, pour
  Excel) et `empreintes.sha256` (contrôlable sans copicol avec
  `sha256sum -c`) : empreinte, taille et date de validation de chaque
  fichier, au nom réel dans la sauvegarde. Seuls les fichiers relus sur la
  sauvegarde et identiques à la source y entrent : copie avec vérification,
  ou **Vérifier la sauvegarde…**. Refait après chaque copie, sous un nom temporaire relu
  avant de remplacer l'ancien, d'après les journaux `.empreintes` écrits au
  fil de chaque copie et forcés sur le disque après chaque dossier. Tous
  portent une ligne de format et un sceau, et passent en lecture seule : un
  fichier modifié, tronqué, illisible ou d'un autre format est signalé.
- La vérification pendant la copie compare désormais des empreintes SHA-256
  (BLAKE2 auparavant) : celles-là mêmes que garde le manifeste.
- **Archiver une sauvegarde en zip…** (menu Outils) : fait d'une sauvegarde
  terminée un `.zip` à envoyer ou à ranger, rapports compris. Ses chemins
  étant déjà raccourcis, il s'ouvre partout, explorateur compris. Les formats
  déjà compressés (PDF, images, DWG, Office…) sont rangés tels quels.
  L'archive est relue en entier avant de prendre son nom final ; une
  annulation ou une erreur n'en laisse aucune partielle. Tout ou rien : un
  fichier verrouillé ou un dossier illisible arrête l'archivage, sans rien
  écrire, et chacun est nommé. Libre, sans licence.
- Option **Compresser la cible (NTFS)** (Réglages…, groupe Place sur le
  disque) : Windows compresse chaque fichier écrit sur la sauvegarde, qui
  reste un dossier ordinaire. Sur exFAT, FAT32 ou un NAS, un seul
  avertissement, et la copie se fait sans.
- Bouton **Ce lecteur** (Alt+L), à côté de la cible, quand copicol est lancé
  depuis une clé USB ou un disque externe : la sauvegarde va dans
  `<lecteur>:\SAUVEGARDE`, créé au besoin. Au premier lancement depuis le
  support, la cible est pré-remplie ; la note sous le champ rappelle
  « Lecteur de copicol ». Les chemins de ce lecteur sont mémorisés sans leur
  lettre : la clé branchée en F: au lieu de E: retrouve sa cible.
- **Vérifier la sauvegarde (comparer à la source)…** (menu Outils, Alt+V) :
  contrôle l'intégrité d'une sauvegarde
  existante sans rien recopier. Chaque fichier de la source est comparé
  octet par octet à son double, relu sur le disque, avec les réglages de la
  dernière copie (noms raccourcis et dossier de secours compris). Le rapport
  `rapport_verification_<date>` distingue les fichiers altérés (même date,
  contenu différent), manquants, modifiés depuis la copie, et ceux absents
  de la source. Libre, comme l'estimation.
- Option **Conserver** (Réglages…, groupe Métadonnées) : en plus de la date
  de modification, la date de création et les attributs caché, système et
  archive, puis, au choix, les permissions NTFS. Une métadonnée que la cible
  ne connaît pas (exFAT, FAT32, certains NAS) est abandonnée avec un seul
  avertissement ; un refus ponctuel est compté dans le rapport, sans jamais
  empêcher la copie du fichier.
- **Mode administrateur** : lancé en administrateur, copicol passe outre les
  permissions (lecture de la source, écriture sur la sauvegarde, comme
  `robocopy /B`) et recopie aussi le propriétaire des fichiers.
- **Récupérer les droits…** (menu Outils) : rend à votre compte l'accès
  complet à une sauvegarde que ses permissions recopiées bloquent.
- **Ménager le disque** (Réglages…) : débit maximal et repos d'un
  quart d'heure, par exemple, chaque heure de copie, pour un disque ancien
  ou qui chauffe pendant une longue copie, ou pour ne pas saturer un NAS
  encore utilisé en journée (choix « NAS » à 50 et 25 Mo/s). Modifiables en
  pleine copie, appliqués aussitôt ; les autres réglages de copie sont alors
  grisés jusqu'à la fin. Sans effet sur une simulation.
- **Arrêt sur disque défaillant** (Réglages…, cochée par défaut) :
  après 5 erreurs matérielles (CRC, lecture ou écriture impossible, copie
  relue différente, disque débranché), la copie s'arrête et pourra reprendre.
- **Licence d'utilisation** : la simulation et l'estimation restent libres ; la copie, la reprise
  et la restauration demandent une clé de licence (vendue sur Lemon Squeezy),
  activée une fois par support : activée depuis une clé USB, elle suit la
  clé sur tout ordinateur, sans nouvelle activation. Onglet « Tarifs » dans l'aide (état de la
  licence, offres, conditions) et bouton « Licence… » pour activer la clé ou
  libérer le poste. L'onglet « Licence » devient « Contrat de licence ».
- Option **Raccourcir les noms** (Réglages…) : coupe simple, début et
  fin (garde l'indice ou la date en fin de nom) ou abréviation (retire les
  mots vides avant de couper). La règle est notée dans le rapport ; changer
  de règle sur une cible déjà copiée demande confirmation.
- **Restaurer une sauvegarde…** (menu Outils) : recopie une sauvegarde vers le dossier d'origine ou un
  autre, en rétablissant les noms et l'arborescence d'origine d'après tous
  les rapports de copie (dossier de secours compris). Aucun fichier déjà
  présent à l'arrivée n'est remplacé.
- **Rechercher un fichier…** (menu Outils, Ctrl+F) : retrouve un fichier dans une sauvegarde par les mots de
  son nom ou chemin d'origine, et ouvre son emplacement, même raccourci ou
  déporté.
- Bouton **Estimer…** : mesure la source
  et ce que la cible contient déjà, annonce le volume à copier, la place
  libre et la durée prévue (d'après le débit de la dernière copie), puis
  demande confirmation.
- Option **Exclure** (Réglages…) : motifs de fichiers et de dossiers à
  ne pas copier (`*.tmp; node_modules`), comptés et listés dans le rapport.
- Les éléments de la cible absents de la source (supprimés ou renommés sur le
  serveur depuis une copie précédente) sont signalés dans le rapport, jamais
  effacés.
- `LISEZMOI_COPICOL.txt` à la racine de la cible explique la sauvegarde à qui
  branche le disque sans connaître copicol.
- Onglet « Limites » dans l'aide : ce que la copie, la restauration et la
  recherche ne font pas, ou seulement en partie.

### Copie

- Une copie menée à son terme avec des erreurs n'est plus proposée comme
  « interrompue » à la copie suivante : reprendre aurait sauté des dossiers
  dont les fichiers avaient changé depuis. La question de reprise donne la
  date de l'interruption.
- Un dossier dont le rapport n'a pas pu être écrit (disque ou NAS
  défaillant) n'est plus noté comme fait : une reprise le recopie, au lieu de
  le sauter avec un rapport, donc des noms d'origine, incomplets.
- Si le journal d'empreintes ne peut plus être écrit, un fichier modifié
  n'est plus remplacé dans la sauvegarde : il reste en erreur, à recopier.
  Remplacé, il aurait gardé l'empreinte de l'ancienne version et serait
  passé pour « altéré » à chaque contrôle.
- La restauration rend la dernière version d'un fichier même quand la
  dernière copie a été interrompue ou n'était qu'une reprise des erreurs :
  tous les rapports de copie sont lus, le plus récent l'emportant. Après un
  changement des limites de longueur, l'ancien exemplaire raccourci pouvait
  être restauré à la place du nouveau.
- Dans le CSV, la colonne `explication` écrit `->` au lieu de `→`, qu'Excel
  perdait en réenregistrant le fichier.
- **Vérifier la sauvegarde** : un fichier enregistré dans la source pendant
  la vérification est classé « modifié depuis la copie », et non plus
  « altéré » : la sauvegarde n'était pas abîmée.
- **Archiver une sauvegarde en zip** attend qu'une copie en cours vers cette
  sauvegarde se termine : le zip aurait mélangé deux états.
- Les rapports et journaux d'une sauvegarde restent dans l'ordre où ils ont
  été écrits, même si l'horloge du poste retarde, si deux postes écrivent sur
  le même disque, ou pendant l'heure répétée du passage à l'heure d'hiver.
  Un rapport plus ancien pouvait sinon passer pour le dernier.
- Une source ou une cible dont le nom finit par un point (`Dossier.`, sur un
  NAS) est bien celle qui est copiée, et non `Dossier`.
- Une jonction ou un lien déjà présent dans la cible est remplacé par un vrai
  dossier ou fichier, au lieu de faire écrire la copie ailleurs. La
  restauration, elle, garde les jonctions du serveur où elle écrit (un dossier
  déplacé sur un autre volume par l'administrateur, par exemple) : elle
  restaure à travers elles. Un fichier temporaire
  resté en lecture seule après une coupure ne bloque plus son fichier.
- Entre deux disques NTFS, un fichier réenregistré moins de 2 secondes après
  sa copie est recopié : la tolérance de 2 s ne vaut plus que pour les dates
  à la seconde près (FAT, certains NAS).
- Le rapport texte est réécrit d'un seul geste : une coupure ne le laisse
  plus vide.
- Une extension coupée ne finit plus par une espace ou un point, ce qui
  rendait le nom inaccessible depuis l'explorateur.
- Les fichiers temporaires `~copicol_*.tmp` laissés par une coupure sont
  effacés au passage suivant, même si leur fichier a disparu de la source.
- Une erreur imprévue qui arrête un dossier est notée au rapport : « Recopier
  les N éléments » le reprend.
- L'estimation compare la date en plus de la taille, comme la copie, et ne
  compte plus les liens symboliques, que la copie ignore.
- Fermer copicol pendant une copie attend qu'elle s'arrête proprement
  (rapport final, verrou de la cible levé), 30 secondes au plus.
- Les fichiers OneDrive / SharePoint à la demande, dédupliqués ou
  hiérarchisés sont copiés : ils étaient pris pour des liens et ignorés.
  Seuls les vrais liens symboliques et jonctions le restent.
- Un fichier enregistré dans la source pendant sa copie est signalé en
  erreur et recopié à la copie suivante, au lieu de garder, validé, un
  mélange de deux versions.
- Quand la relecture directe sur le disque est refusée (partage réseau,
  fichier tenu par un antivirus), le journal le signale une fois : la
  vérification passe alors par la mémoire de Windows. Un antivirus qui
  tient le fichier ne force plus ce repli.
- Le rapport CSV est forcé sur le disque avant le point de reprise : une
  coupure ne fait plus sauter à la reprise un lot dont les noms d'origine
  seraient perdus.
- Contrôle avec le manifeste : des fichiers manquants, le plus souvent
  supprimés à la main comme absents de la source, donnent un bandeau
  orange (« supprimé(s) à la main ? ») et non plus « sauvegarde abîmée ».
- « Arrêter si le disque semble défaillant » ne compte plus que les erreurs
  matérielles d'affilée : quelques fichiers abîmés épars n'arrêtent plus
  la copie à chaque reprise.
- Un fichier source nommé `copicol_etat.json` ou `LISEZMOI_COPICOL.txt` à la
  racine est renommé, au lieu d'écraser le point de reprise.
- La reprise des erreurs d'un rapport garde les noms à point final
  (`rapport.`) dans le nouveau rapport.
- Un nom trop long rangé dans un dossier déjà profond est désormais signalé
  « nom trop long + chemin trop long » quand le chemin impose une coupe plus
  courte que la limite de nom (auparavant : « nom trop long » seul).
- Une cible qui contient la source est refusée, y compris quand l'une est
  désignée par sa lettre de lecteur et l'autre par son chemin réseau : un
  dossier copié pouvait retomber sur la source et en écraser des fichiers.
- Un dossier cible impossible à créer figure désormais dans les rapports
  (auparavant compté parmi les erreurs sans y être détaillé).
- « Volume copié » ne compte plus les fichiers dont la copie a échoué.
- Noms réservés reconnus aussi avec un espace avant l'extension (`CON .txt`)
  ou un chiffre en exposant (`COM¹`), noms possibles sur un NAS.
- Au-delà de 999 noms identiques dans un même dossier, le numéro ajouté ne
  fait plus dépasser la limite de longueur.
- Les longueurs se comptent comme Windows : un emoji vaut deux caractères.
  Un chemin plein d'emoji pouvait dépasser la limite d'un tiers.
- Un rapport modifié à la main ne peut plus faire écrire une restauration
  ou une reprise hors de la cible (chemin `D:fichier` d'un autre lecteur) ;
  seule la ligne invalide est ignorée, plus tout le rapport.
- Dans le rapport CSV, un nom commençant par `=`, `+`, `-` ou `@` est
  précédé d'une apostrophe : Excel ne l'exécute plus comme une formule.
- Deux copies lancées dans la même seconde vers une même cible n'écrasent
  plus le rapport de la première (horodatage à la milliseconde).
- L'estimation ne compte plus comme « déjà copié » que les fichiers de la
  source présents dans la cible au même chemin et à la même taille : le
  reste du disque lui faisait annoncer assez de place, ou « tout semble déjà
  copié », à tort.
- « Recopier les N éléments » d'un rapport vérifie la règle de renommage de
  la cible, comme une copie : changée depuis, elle créait des doublons. Une
  règle modifiée pendant l'estimation est aussi signalée avant de lancer.
- Un rapport réenregistré par Excel, ou abîmé d'un octet, se lit encore :
  la recherche ne reste plus bloquée sur « en cours » et la restauration
  n'échoue plus. Seules les lignes illisibles sont ignorées.
- La recherche ne dit plus « non copié (simulation) » d'un fichier copié
  quand une simulation a été lancée après la copie.
- La limite de débit ne laisse plus écrire à pleine vitesse après une
  longue période sans écriture (analyse, reprise) : une seconde d'avance au
  plus.
- Les fichiers placés dans le dossier de débordement ne gardent de leur
  extension que lettres et chiffres : plus de point, d'espace finale ou de
  `?` qui rendaient le nom invalide.
- « Disque plein » désigne le disque du rapport, et non la cible, quand le
  rapport a dû être écrit dans Documents.
- Un rapport modifié dont l'en-tête donne une source ou une cible relative
  (« .. ») ne peut plus faire écrire la restauration hors du dossier
  d'arrivée, ni faire ouvrir à la recherche un emplacement hors de la
  sauvegarde.
- Un rapport texte réenregistré en ANSI n'arrête plus la restauration, la
  recherche, la vérification ni la copie. S'il est illisible, la
  restauration le signale en erreur : les noms qu'il notait sont perdus.
- Après deux copies faites avec des limites différentes, la restauration
  rend la version de la dernière copie, et non l'ancien nom raccourci resté
  dans la sauvegarde.
- La restauration ne remplace pas non plus un fichier apparu à destination
  pendant qu'elle le recopiait : il est conservé et signalé.

### Application

- Licence : le fichier de licence est scellé. Écrit ou modifié à la main, il
  doit d'abord être revérifié en ligne. Recopié sur un autre support, il est
  refusé à la revérification. Sans revérification réussie depuis 30 jours, la
  copie attend une connexion ; la restauration reste possible hors ligne.
  Depuis un partage réseau, chaque poste compte pour un support. Fermer la
  fenêtre de licence pendant l'activation ne lance plus la copie toute seule
  ensuite.
- Contrat de licence, mode d'emploi et onglet Tarifs : règle des 30 jours,
  partage réseau et support reformaté ou remplacé.
- Release : construite à partir de dépendances verrouillées et vérifiées par
  empreinte (`requirements-lock.txt`), actions GitHub épinglées par commit,
  jeton en lecture seule pendant la construction.
- L'exécutable est compilé par Nuitka et non plus assemblé par PyInstaller :
  le code Python est traduit en C, puis compilé (recette :
  `tools/build_exe.py`, qui remplace `copicol.spec`).

- Fenêtre « Mode d'emploi et licences », ouverte par le bouton **?** : à
  propos, mode d'emploi (le README), licence de copicol et licences des
  composants tiers embarqués (Python, Tcl/Tk, OpenSSL…).
- Au premier lancement, la licence est à accepter pour utiliser copicol.
- Le mode d'emploi s'ouvre au démarrage ; une case permet de ne plus
  l'afficher.
- Fenêtre de taille fixe, 800 × 600 (à l'échelle de l'écran) : ses bords ne
  s'étirent plus, seul l'agrandissement en plein écran reste possible. La
  position et le plein écran sont mémorisés.
- Interface réécrite avec tkinter, fourni avec Python : plus aucune
  dépendance (PySide6/Qt retiré) ; l'exécutable est nettement plus léger.
- Les réglages mémorisés passent dans `%LOCALAPPDATA%\copicol\reglages.json` :
  les chemins saisis avec la version 1.0.0 sont à ressaisir une fois.
- Une licence dont la date de vérification est dans le futur (fichier
  modifié, horloge remise en arrière) est revérifiée au démarrage, au lieu
  de rester valable pour toujours.
- La revérification de la licence au démarrage n'écrase plus un « Libérer »
  ou une nouvelle activation faits pendant qu'elle attendait le serveur.
- `tools/public.py` refuse de joindre un `copicol.exe` plus ancien que des
  modifications en cours, et pas seulement que le dernier commit.
- Au 100e commit, le numéro passe de V1.99 à V2.00 plutôt qu'à V1.100, qui
  sortait du format Vx.xx et se triait avant V1.99.

### Interface

- Fenêtre principale réorganisée de haut en bas : dossiers, options, actions,
  état de la copie, journal. Les réglages fins (longueurs, règle de
  renommage, vérification, ménagement du disque, exclusions) passent dans
  une fenêtre **Réglages…** (Alt+G) ; la fenêtre principale en rappelle les
  valeurs modifiées. La case **Simulation** rejoint le bouton Démarrer.
  Progression, rappel de la simulation et bandeau de fin se relaient dans
  une zone de hauteur fixe : le journal garde toujours la même place.
- Barre d'actions selon l'état : Démarrer et Estimer au repos, Pause et
  Annuler pendant la copie. Reprise d'un rapport, restauration et recherche
  rangées dans le menu **Outils** ; « Reprendre… » devient « Reprendre
  d'après un rapport… », qui ne se confond plus avec la reprise après pause.
- Les questions (reprise, règle de renommage, restauration, estimation,
  annulation) ont des boutons qui disent ce qu'ils font, au lieu de
  Oui / Non / Annuler. Annuler une longue copie ou lancer sans place
  suffisante met en avant « Continuer » / « Annuler ».
- Progression affichée sur le bouton de la barre des tâches de Windows (en
  pause : jaune ; erreur ou interruption : rouge jusqu'à lecture du bandeau).
- Après « Estimer… », la barre d'ensemble suit le volume de toute la copie,
  avec le temps restant.
- Progression du dossier en unités lisibles (1.0 Gio / 5.0 Gio au lieu de
  1024 / 5120 Mio).
- Barres de progression fines, aux bouts arrondis, avec le chiffre en gras
  au-dessus ; vertes, orange ou rouges à la fin selon le résultat.
- Filtres du journal en onglets soulignés, avec compteurs en pastille (rouge
  pour les erreurs) ; journal au liseré discret, avec un message centré
  quand il est vide.
- Bandeau orange rappelant le mode simulation.
- Bouton Démarrer en gras, aussi en thème clair.
- Raccourcis Alt + lettre soulignée et Ctrl+F.
- Textes secondaires plus contrastés en thème clair ; infobulles raccourcies,
  le détail restant dans le mode d'emploi.
- Les rapports de la dernière copie (.txt, .csv, dossier) sont regroupés dans
  le menu **Rapports**.
- Fenêtre redimensionnable, qui tient dans l'écran même agrandi à 150 % ;
  sa taille et sa place sont mémorisées.
- Thème clair ou sombre, selon le réglage de Windows, ou imposé par le menu
  **Outils ▸ Thème** (Comme Windows, Clair, Sombre) ; le choix est mémorisé.
- Dossiers vérifiés pendant la frappe : dossier introuvable, cible dans la
  source, place libre et caractères laissés aux chemins copiés. Le bouton
  Démarrer attend une saisie valide.
- Derniers dossiers utilisés proposés dans les champs Source et Cible ;
  texte indicatif dans un champ vide.
- Fin de copie annoncée par un bandeau coloré qui reste dans la fenêtre, au
  lieu d'une boîte de dialogue.
- Journal filtrable (renommages, erreurs et alertes), copie de la sélection
  ou d'une ligne.
- Bouton « Reprendre… » : à partir du rapport d'une copie précédente,
  remplit la source et la cible, puis recopie seulement les éléments en
  erreur (sans reparcourir la source) ou relance la copie complète. Le
  rapport .txt est écrit dès le début de la copie pour que même une copie
  coupée tôt puisse être reprise ainsi.
- Bouton Pause ; confirmation avant d'annuler une copie lancée depuis plus
  d'une minute.
- Journal en police plus lisible (Cascadia Mono ou Consolas, selon le poste).
- Raccourcis Entrée (démarrer) et Échap (annuler) ; réglages fins
  regroupés dans la fenêtre Réglages….
- Option « Inventaire complet » retirée : le rapport CSV contient déjà la
  liste de tous les fichiers.
- Bouton « Lancer le test » retiré de l'application : le jeu d'essai (34 cas)
  reste exécuté par les tests automatiques à chaque construction.
- La copie en cours vers une cible déjà utilisée par un autre poste est
  refusée sans proposer de passer outre : le verrou ne tient plus que tant
  que l'autre copie tourne réellement.
- Annuler (ou Échap) et fermer la fenêtre ne plantent plus quand la copie
  se termine pendant que la confirmation est affichée.
- Après Annuler, Pause reste grisé : un clic dessus bloquait l'interruption
  indéfiniment.
- « Récupérer les droits » compte comme une tâche en cours : pas de copie
  lancée en parallèle, et fermer la fenêtre demande confirmation.
- Une boîte de dialogue ouverte en cours de copie ne fige plus la progression.

## [V1.00] - 2026-11-01

Première version, non publiée.

### Copie

- Copie d'un dossier vers une cible en gardant tous les chemins sous une
  limite réglable (240 caractères par défaut) : noms nettoyés, raccourcis avec
  un code stable, ou déportés dans `_CHEMINS_TROP_LONGS`.
- Copie sous-dossier par sous-dossier, avec reprise après interruption.
- Chaque fichier est écrit sous un nom temporaire et renommé une fois complet :
  jamais de fichier tronqué, même après une coupure de courant.
- Un fichier déjà présent n'est sauté que si sa taille et sa date
  correspondent : un fichier modifié depuis la dernière copie est remplacé
  (statut « mis a jour » dans le CSV). Tolérance aux dates des disques FAT32.
- Option « Vérifier chaque fichier après copie » : relecture sur le disque
  lui-même et comparaison avec la source.
- Arrêt immédiat si le disque cible est plein.
- Fichiers techniques (`Thumbs.db`, verrous Office, `.bak` AutoCAD…) écartés
  par défaut.

### Rapports

- Rapports `.txt` et `.csv` horodatés dans `_RAPPORT_COPICOL`, mis à jour
  après chaque sous-dossier ; ils indiquent la version de copicol.

### Application

- Exécutable autonome, sans installation, avec version et éditeur dans ses
  propriétés Windows.
- Une seule copie à la fois vers une même cible, y compris depuis deux postes.
- Erreurs imprévues consignées dans `%LOCALAPPDATA%\copicol\copicol.log` et
  annoncées par une fenêtre.
- Boîte « À propos » (bouton **?**).

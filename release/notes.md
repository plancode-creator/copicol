**copicol copie un serveur de projets vers un disque externe, même quand ses chemins dépassent la limite de 260 caractères de Windows.** Les noms trop longs sont raccourcis automatiquement, et chaque renommage est noté dans un rapport : rien ne se perd, tout se retrouve et se restaure.

## Télécharger

| Fichier | |
|---|---|
| **copicol.exe** | L'application, prête à lancer : aucune installation, aucun droit d'administrateur. Fonctionne depuis une clé USB. |
| copicol.exe.sha256 | Son empreinte, pour vérifier qu'une copie de l'exe n'a pas été altérée. |

Windows 10 ou 11. Au premier lancement, Windows peut afficher « Windows a protégé votre ordinateur » : cliquer sur **Informations complémentaires**, puis **Exécuter quand même**.

## Pourquoi copicol

Sur un serveur de projets, les dossiers s'empilent (*Phase DCE › Lot 03 › Pièces graphiques…*) jusqu'à dépasser 260 caractères. L'explorateur, Office ou un zip refusent alors ces fichiers, et les outils de copie habituels échouent en silence. copicol :

- **copie tout**, en ramenant chaque chemin sous la limite choisie (240 caractères par défaut) ;
- **note chaque renommage** (ancien et nouveau nom) dans un rapport `.txt` et un inventaire `.csv` déposés sur le disque de sauvegarde ;
- **retrouve** un fichier d'après son nom d'origine, même raccourci ;
- **restaure** la sauvegarde avec ses noms et son arborescence d'origine ;
- **vérifie**, des mois plus tard, que le disque a gardé intact ce qu'on lui a confié ;
- **estime** avant de copier le volume, la place libre et la durée prévue ;
- **ménage le disque et le réseau** : débit plafonné, repos chaque heure, arrêt si le disque semble défaillant ;
- **simule** gratuitement la copie, pour voir ce qui serait renommé sans rien écrire.

## Gratuit ou sous licence

**Gratuit, sans limite de durée** : simulation avec rapports, estimation du volume et de la durée, recherche dans les sauvegardes, vérification d'une sauvegarde, récupération des droits d'accès.

**Sous licence** : copie, reprise après interruption et restauration.

| Offre | Prix | |
|---|---|---|
| Personnelle | 19 € | 1 support activé, usage privé et non commercial |
| Professionnelle | 29 € | 1 support activé, usage professionnel |
| Entreprise | 79 € | jusqu'à 25 supports activés au sein d'une même entreprise |
| Entreprise illimitée | 149 € | nombre illimité de supports activés au sein d'une même entreprise |

Paiement unique, sans abonnement. La licence suit le support d'où copicol est lancé : activée sur une clé USB, elle fonctionne sur tous les ordinateurs où on la branche. Une connexion à Internet est nécessaire à l'activation, puis au moins une fois tous les 30 jours pour copier ; la restauration reste toujours possible hors ligne. Boutique : https://plan-code.lemonsqueezy.com

## Nouveautés de cette version

**Nouveautés**

- Bouton **Ce lecteur** (Alt+L), à côté de la cible, quand copicol est lancé
  depuis une clé USB ou un disque externe : la sauvegarde va dans
  `<lecteur>:\SAUVEGARDE`, créé au besoin. Au premier lancement depuis le
  support, la cible est pré-remplie ; la note sous le champ rappelle
  « Lecteur de copicol ». Les chemins de ce lecteur sont mémorisés sans leur
  lettre : la clé branchée en F: au lieu de E: retrouve sa cible.
- Bouton **Vérifier…** (Alt+V) : contrôle l'intégrité d'une sauvegarde
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
  encore utilisé en journée (choix « NAS » à 50 et 25 Mo/s). Sans effet sur
  une simulation.
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

**Copie**

- Une copie menée à son terme avec des erreurs n'est plus proposée comme
  « interrompue » à la copie suivante : reprendre aurait sauté des dossiers
  dont les fichiers avaient changé depuis. La question de reprise donne la
  date de l'interruption.
- Une jonction ou un lien déjà présent dans la cible est remplacé par un vrai
  dossier, au lieu de faire écrire la copie ailleurs. Un fichier temporaire
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
- Un fichier enregistré dans la source pendant sa copie est recopié à la
  copie suivante, au lieu de garder pour toujours une version périmée.
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

**Application**

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

**Interface**

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

---

Mode d'emploi complet, limites connues et règles de renommage : voir le README du dépôt. Historique des versions : CHANGELOG.md.

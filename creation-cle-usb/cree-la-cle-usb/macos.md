# MacOS

Bien que vous n'ayez pas besoin d'une nouvelle installation de macOS pour utiliser OpenCore, certains utilisateurs préfèrent avoir une nouvelle installation avec les mises à niveau de leur boot-loader.

Pour commencer, nous allons nous procurer une copie de macOS. Vous pouvez ignorer cela et vous diriger vers le formatage de l'USB si vous créez simplement une clé OpenCore amorçable et non un programme d'installation. Pour tous les autres, vous pouvez soit télécharger macOS depuis l'App Store, soit avec le script de Munki.



### Téléchargement de macOS: système d'exploitation moderne

* Cette méthode vous permet de télécharger macOS 10.13 et versions ultérieures, pour 10.12 et versions antérieures, voir Téléchargement de macOS : Legacy OS&#x20;

À partir d'une machine macOS qui répond aux exigences de la version du système d'exploitation que vous souhaitez installer, accédez directement à l'App Store et téléchargez la version du système d'exploitation souhaitée et passez à Configuration du programme d'installation.

Pour les machines qui nécessitent une version spécifique du système d'exploitation ou qui ne peuvent pas être téléchargées depuis l'App Store, vous pouvez utiliser l'utilitaire InstallInstallMacOS de Munki.



<details>

<summary>Remarque pour les utilisateurs utilisant macOS Monterey 12.3 ou supérieur</summary>

À partir de macOS Monterey 12.3, Apple a supprimé la prise en charge de python2.7, donc sans cela, installinstallmacos.py renverra l'erreur suivante :

```
This tool requires the Python xattr module. Perhaps run 'pip install xattr' to install it.
```

Pour résoudre le problème, nous vous recommandons d'installer les outils de ligne de commande pour Xcode en exécutant xcode-select --install dans un terminal, puis exécutez pip3 install xattr

Après cela, vous pouvez exécuter la même commande ci-dessous mais avec python3 au lieu de simplement python

```shell
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python3 installinstallmacos.py
```

</details>

Pour l'exécuter, copiez et collez simplement la commande ci-dessous dans une fenêtre de terminal :&#x20;

```bash
mkdir -p ~/macOS-installer && cd ~/macOS-installer && curl https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py > installinstallmacos.py && sudo python installinstallmacos.py
```

![](../../.gitbook/assets/image.png)

Comme vous pouvez le voir, nous obtenons une belle liste d'installateurs macOS. Si vous avez besoin d'une version particulière de macOS, vous pouvez la sélectionner en tapant le numéro à côté. Pour cet exemple, nous choisirons 10 :&#x20;

![](<../../.gitbook/assets/image (3).png>)



* macOS 12, Monterey Remarque : Comme ce système d'exploitation est assez nouveau, il reste encore quelques problèmes à résoudre avec certains systèmes. Pour plus d'informations, voir ici : macOS 12 : Monterey&#x20;
  * Pour les nouveaux utilisateurs, nous recommandons macOS Catalina (10.15) ou Big Sur (11)
  * ATTENTION : Avec macOS 11.3 et versions ultérieures, XhciPortLimit est rompu, ce qui entraîne des boucles de démarrage (ouvre une nouvelle fenêtre). Nous conseillons aux utilisateurs d'installer un système d'exploitation plus ancien (c'est-à-dire macOS 10.15, Catalina) ou de trouver un programme d'installation Big Sur 11.2.3 ou plus ancien.
    * &#x20;À des fins éducatives, nous avons une copie fournie ici : macOS 11.2.3 InstallAssistant(macOS)(ouvre une nouvelle fenêtre)&#x20;
    * Si vous avez déjà mappé vos ports USB (ouvre une nouvelle fenêtre) et désactivé XhciPortLimit, vous pouvez démarrer macOS 11.3+ sans problème

Cela va prendre un certain temps car nous téléchargeons l'intégralité du programme d'installation de macOS 8 Go+, il est donc fortement recommandé de lire le reste du guide pendant que vous attendez.

Une fois terminé, vous trouverez dans votre dossier `~/macOS-Installer/` un DMG contenant le macOS Installer, nommé `Install_macOS_11.1-20C69.dmg` par exemple. Montez-le et vous trouverez l'application d'installation.

* Remarque : Nous vous recommandons de déplacer l'application Install macOS.app dans le dossier `/Applications`, car nous exécuterons des commandes à partir de là.
* Remarque 2 : L'exécution de Cmd+Shift+G dans le Finder vous permettra d'accéder facilement à `~/macOS-installer`

![](<../../.gitbook/assets/image (2).png>)

![](<../../.gitbook/assets/image (4).png>)

De là, passez à [Configuration du programme d'installation](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-the-installer) pour terminer votre travail. Si vous souhaitez vérifier [l'intégrité de votre téléchargement](https://github.com/notpeter/apple-installer-checksums), vous pouvez consulter ce référentiel de sommes de contrôle (ouvre une nouvelle fenêtre), mais notez qu'il s'agit de sommes de contrôle participatives et qu'elles ne constituent peut-être pas un moyen fiable de vérifier l'authenticité.

### Téléchargement de macOS: Legacy OS <a href="#downloading-macos-legacy-os" id="downloading-macos-legacy-os"></a>



### Configuration du programme d'installation

Nous allons maintenant formater la clé USB pour préparer à la fois le programme d'installation macOS et OpenCore. Nous voudrons utiliser macOS Extended (HFS +) avec une carte de partition GUID. Cela créera deux partitions : la principale MyVolume et une seconde appelée EFI qui est utilisée comme partition de démarrage où votre micrologiciel vérifiera les fichiers de démarrage.

* Remarque : Par défaut, Utilitaire de disque n'affiche que les partitions - appuyez sur Cmd/Win+2 pour afficher tous les périphériques (vous pouvez également appuyer sur le bouton Afficher)
* Remarque 2 : les utilisateurs qui suivent la section "MacOS hérité : méthode en ligne" peuvent passer à la section Configuration de l'environnement EFI d'OpenCore

![](<../../.gitbook/assets/image (1).png>)

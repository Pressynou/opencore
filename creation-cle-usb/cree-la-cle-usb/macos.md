# MacOS

Bien que vous n'ayez pas besoin d'une nouvelle installation de macOS pour utiliser OpenCore, certains utilisateurs préfèrent avoir une nouvelle installation avec les mises à niveau de leur boot-loader.

Pour commencer, nous allons nous procurer une copie de macOS. Vous pouvez ignorer cela et vous diriger vers le formatage de l'USB si vous créez simplement une clé OpenCore amorçable et non un programme d'installation. Pour tous les autres, vous pouvez soit télécharger macOS depuis l'App Store, soit avec le script de Munki.



#### Téléchargement de macOS : système d'exploitation moderne

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

##

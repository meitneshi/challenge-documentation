### Bac à sable (Sandbox)

Il existe un autre mode pour les missions, le mode bac à sable (sandbox).  Les missions classiques doivent
contenir plusieurs tests permettant de verifier que le candidat a bien réussi la mission. Mais parfois, il est difficile 
voire impossible d'implémenter suffisamment de test pour s'assurer que le candidat ait bien compris et réussi le challenge.  
Vous pouvez alors créer une mission sans aucun test, mais vous devrez tout de même créer la classe Run. Le professeur
pourra valider la mission via la page de l'étudiant.  
Il vous suffit d'ajouter la ligne `sandboxed: true` dans le fichier challenge.yml.

Exemple :  
```yaml
name: code_interview_card_game
label: Card Game
description: Card Game
level: ewok
type: CODING
sandboxed: true
```


### Liste noire
Par défaut, il existe une liste noire de mots que le candidat ne peut pas insérer dans son code. 
Un exemple est disponible dans le répertoire contenant toutes les missions de Deadlock. Vous trouverez au même niveau que les missions,
un dossier `resources` contenant les ressources utile pour la création d'une mission dont un exemple de liste noire dans `default/blacklist`.  
Vous pouvez également créer votre propre liste noire pour une mission en créant un fichier `blacklist` au même niveau que le challenge.yml
et en le remplissant comme un fichier csv. Il supporte également les expressions régulière (regex).

Exemple de fichier blacklist :   
```bash
[^<>](<|>)[^><],(System\.exit\()(\d)*(\)),(Runtime\.getRuntime\(\)\.exit\(\d*\))
```

# Mission Score

Lorsque vous créez une mission de code, le candidat dispose de deux manières d'exécuter son code (Plus d'infos [ici](/challenge-documentation)) : 

* Exécuter -> exécute le code seul sans les tests
* Soumettre -> exécute le code avec les tests que vous avez fournis.


Il est possible de retourner un **score** lorsque vous testez le code du candidat.  
Par exemple, si vous considérez que si 50 tests validés sur les 100 disponibles suffisent à considérer la mission comme 
réussie, vous devez l'écrire de cette manière (dépendante du langage) : 

=== "Java"
    ```Java 
    public static void main(String[] args) {
        // test user code
        Mission.INSTANCE.done(50);
    }
    ```
=== "Python"
    ```Python 
    def main():
        # test user code
        Mission.done(50):
    ```

Vous pouvez également spécifier d'autre champs dans le `challenge.yml` :
```yaml
 score:
    min: 0 # score minimum par défaut (optionnel)
    minToValidate: 90 # score minimum pour valider la mission
    max: 100 # score maximum par défaut (optionnel)
```

Le candidat dispose alors d'un nouvel onglet sur son interface juste à coté de la **Console**.
![Example score Python](../img/example-score.png)

### Exemple
[code_score_python](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_score_python)

# Multi-langage (metamorph)

Vous pouvez créer une mission indépendamment du langage dans lequel elle sera résolue.  
Le candidat est donc libre de choisir son langage préféré pour résoudre le problème !  

Liste des langages supportés par Deadlock :

* Java 11.0.5 (openjdk)
* Kotlin 1.3.70-eap-184
* Python 3.8.2
* C/C++ 9.2.0
* Rust 1.39.0
* Go 1.12.16
* Javascript avec NodeJS 12.15.0
* Ruby 2.6.6
* Ocaml 4.08.1


Imaginons que vous souhaitez écrire une mission d'implémentation de la suite de Fibonacci.  

Créer un nouveau dossier contenant un fichier `entry.rs`. Ce fichier définit : 

- quel(s) langage(s) sont disponibles pour l'implémentation de la résolution du candidat,
- tous les tests pour valider le code du candidat.  

```rust linenums="1"
challenge! {{
    "languages": ["java", "python", "c", "cpp", "go", "ruby", "rust", "javascript"]
}}
```

Dans le premier tableau sont énuméré tous les langages que le candidat pourra sélectionner au moment de développer la solution à la mission.  

Ensuite, vous devez écrire différents tests, chacun sera exécuté seulement si le précédent réussi.
Ecrivons ensemble le premier !

```rust linenums="1"
challenge! {{
    "languages": ["java", "python", "c", "cpp", "go", "ruby", "rust", "javascript"],
    "tests": [
        {
            input: 0,
            expected: 1
        }
    ]
}}
```

Ce test va appeler le programme du candidat avec `0` comme *entrée* et s'attend à avoir `1` comme *sortie*.  
Par défaut, pour chaque langage, le candidat dispose d'un template. Vous pouvez personnaliser le template pour chaque langage :

=== "Java"
    ```Java linenums="1"
    public class Main {
        public static void main(String[] args) {
            if (args.length > 0) {
                // Called when you submit your code.
                System.out.println(fibonacci(Long.ValueOf(args[0])));
            } else {
                // Called when you run your code.
                System.out.println("Hello World!");
            }
        }
    
        public static long fibonacci(long n) {
            return n;
        }
    }
    ```
=== "Javascript"
    ```Javascript linenums="1" 
    // CommonJS
    if (process.argv.length > 2) {
        // args given, code submitted
        console.log(fibonacci(process.argv[2]));
    } else {
        // no given, code ran
        console.log("Hello World!");
    }
    
    function fibonacci(n) {
        return n;
    }
    ```
=== "Python"
    ```Python linenums="1" 
    import sys;
    
    def fibonacci(n):
        return n
    
    if (len(sys.argv) > 1):
        # args given, code submitted
        print(fibonacci(sys.argv[1]))
    else:
        # no given, code ran
        print("Hello World!")
    ```
=== "Go"    
    ```Go linenums="1" 
    package main
    import (
        "fmt"
        "os"
    )
    
    func Fibonacci(n int64) int64{
        return n 
    }
    
    func main() {
        if (len(os.Args) > 1) {
            // args given, code submitted
            arg := os.Args[1]
    
            fmt.Println(Fibonacci(arg))
        } else {
            // no given, code ran
            fmt.Println("Hello World!")
        }
    }
    ```
=== "C"    
    ```C linenums="1" 
    #include <stdio.h>
    #include <stdlib.h>
    
    long fibonacci(long n)
    {
        return n;
    }
    
    int main(int argc, char **argv)
    {
        if (argc > 1) {
            // args given, code submitted
            printf(fibonacci(argv[1]));
        } else {
            // no given, code ran
            printf("Hello World!");
        }
    }
    ```
=== "Cpp"    
    ```Cpp linenums="1" 
    #include <iostream>
    #include <bits/stdc++.h> 
    
    bool fibonacci(long n)
    {
        return n;
    }
    
    int main(int argc, char **argv)
    {
        if (argc > 1) {
            // args given, code submitted
            printf(fibonacci(stol(argv[1])))
        } else {
            // no given, code ran
            printf("Hello World!");
        }
    }
    ```
=== "Ocaml"    
    ```Ocaml linenums="1" 
    let fibonacci n =
      let rec fib_2termes n a b =
        match n with
        | 0 -> a
        | 1 -> b
        | _ -> fib_2termes (n - 1) b (a + b)
      in fib_2termes n 0 1 ;;
    
    if Array.length Sys.argv > 1 = true
        then print_int (fibonacci  (int_of_string Sys.argv.(1)));;
    ```
=== "Rust"
    ```Rust linenums="1" 
    use std::env;
    
    fn main() {
        let args: Vec<String> = env::args().collect();
    
        if args.len() == 2 {
            // Called when you submit your code.
            println!("{}", fibonacci(&args[1]))
        } else {
            // Called when you run your code.
            println!("Hello World!")
        }
    }
    
    fn fibonacci(n: i64) -> i64{
        n
    }
    ```
=== "Ruby"    
    ```Ruby linenums="1" 
    class Main
      def initialize
        if(ARGV.length() > 0)
          then puts fibonacci (ARGV[0].to_i) # args given, code submitted
          else puts "Hello World!" # no args given, code runner
        end
      end
      def fibonacci (n)
        0
      end
    end
    
    # initialize object
    Main.new
    ```

L'utilisateur doit compléter la méthode `fibonacci` et le résultat sera affiché dans le stdout (console).  
Continuons avec plus de tests :  
```rust linenums="1" 
challenge! {{
    "languages": ["java", "python", "c", "cpp", "go", "ruby", "rust", "javascript"],
    "tests": [
        {
            input: 0,
            expected: 1
        },
        {
            input: 1,
            expected: 1
        },
        {
            input: 2,
            expected: 2
        },
        {
            input: 3,
            expected: 3
        },
        {
            input: 10,
            expected: 89
        }
    ]
}}
```

#### Tests aléatoires
Cela vous semble trop statique ?
Vous pouvez ajouter des tests plus complexe avec des entrées aléatoires en utilisant la méthode `random` fournie par notre runner :  
```Yaml
randt(n): génère un nombre aléatoire entre 0 et n exclu.
randft(n, m): gnère un nombre aléatoire entre n et m exclu.
```
```Rust linenums="1" 
{
    input: randft(20, 30),
    expected: ?
}
```
Cela pose un problème. Que devons nous écrire dans la valeur attendue ?  
Pas de panique, vous pouvez appeler votre propre solution au lieu d'écrire une réponse attendue statique !
```Rust linenums="1" 
{
    input: randft(20, 30),
    expected: call("java", "Solution.java")
},
{
    input: randt(20),
    expected: call("python", "solution.py")
}
```
La même logique est appliquée, votre `solution.py` est appelée par notre interprèteur Python avec les données de *input*
et vous devez écrire le résultat renvoyé par votre solution dans le *stdout*.  
Par exemple pour la suite de Fibonnaci :  
```Python linenums="1" 
# solution.py
def fibo(n):
    if n <= 1:
       return n
    else:
       return(fibo(n - 1) + fibo(n - 2))

print(fibo(sys.argv[1]))
```

Ensuite la sortie *stdout* donnée avec la méthode *print* est comparée à celle résultant du programme du candidat.  
Vous pouvez choisir un interprèteur parmi la liste de ceux proposé ci-après :   

|           |              |      |      |
| ----------|------------- |:----:|-----:|
| java      | javascript   | ruby | c    |
| rust      | python       | go   | cpp  |


#### Répétition
Qu'en est-il si vous désirez exécuter 50 tests aléatoire à la suite ?  
Ce n'est pas un problème, tout ce que vous avez à faire est d'ajouter le paramètre **repeat** à votre test :
```Rust
{
    input: randt(20),
    expected: call("python", "solution.py"),
    repeat: 50
}
```

#### Valeur d'entrée
Ce n'est pas tout, vous pouvez aussi appeler votre propre programme pour générer les valeurs d'entrée :  
```Rust
{
    input: call("javascript", "generate.js"),
    expected: call("python", "solution.py")
}
```

#### Ouvrir un ficher
Vous pouvez également ouvrir un fichier : 
```Rust
{
    input: open("file.txt"),
    expected: call("python", "solution.py")
}
```
Il sera servi au candidat en tant que *Chaîne de caractère*.

Dès que vous aurez compléter le fichier `entry.rs`, il faut compléter le fichier `challenge.yaml` :
```Yaml
version: 1.0
name: code_metamorph_fibo
label: Fibonacci
description: Implements Fibonacci algorithm
level: ewok
type: CODING
metamorph: true
xp:
  programming: 1
coding:
  templateDirectory: /opt/runner
  successDirectory: success/
  target: main.rs
  editorMode: rust
```

Le dossier `success/` contient votre solution qui sera donnée au candidat lorsqu'il aura résolu le problème de la mission.  
Vous êtes libre de choisir le langage et la logique d'implémentation de votre solution.  

Pour tester votre programme, vous pouvez utiliser notre [CLI](https://pypi.org/project/deadlock-cli/):  
```Bash
> dcli run . java # Exécute template/java/Main.java
> dcli solve . java # Exécute les tests sur template/java/Main.java
> dcli run . python # Exécute template/python/Main.py
```

Chaque fichier placer dans le dossier `template` est donné au candidat lorsqu'il décide de changer le langage selectionné.
Par exemple, si le candidat décide d'utiliser l'interpréteur *Rust*, tous les fichier contenu dans `template/rust` lui seront fourni.

Votre mission doit ressembler à cela : 
```
.
├── challenge.yaml
├── entry.rs
├── runner
├── solution.js
├── success
│   └── Main.rs
└── template
    ├── c
    │   └── Main.c
    ├── cpp
    │   └── Main.cpp
    ├── go
    │   └── Main.go
    ├── java
    │   └── Main.java
    ├── javascript
    │   └── Main.js
    ├── python
    │   └── Main.py
    ├── ruby
    │   └── Main.rb
    └── rust
        └── Main.rs
```

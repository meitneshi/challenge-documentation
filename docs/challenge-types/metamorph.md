# Multi language

When you are creating a challenge, you can create one independent of the programming language.  
It gives the ability for the final user to select it's own programming language!  

Available languages:

* Java 11.0.5 (openjdk)
* Kotlin 1.3.70-eap-184
* Python 3.8.2
* C/C++ 9.2.0
* Rust 1.39.0
* Go 1.12.16
* Javascript with NodeJS 12.15.0
* Ruby 2.6.6
* Ocaml 4.08.1


Let's say you want write a Fibonacci challenge.  
Create a new directory and create a `entry.rs` file, it will define:
- which language is available for the user,
- all your tests to validate user code.  

```rust linenums="1"
challenge! {{
    "languages": ["java", "python", "c", "cpp", "go", "ruby", "rust", "javascript"]
}}
```

In the first array you are listing all languages the user will be able to chose on the page.  

Then you are going to write different tests, which one will be run if the previous one succeeded.
Let's write the first one !

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

It will call the user program with the `0` as *input* and is waiting to have `1` as
ouput.  
By default for each language the user will have a template, you can custom each one for each language:

```Java linenums="1" tab=
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

```Javascript linenums="1" tab=
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

```Python linenums="1" tab=
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

```Go linenums="1" tab=
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

```C linenums="1" tab=
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

```Cpp linenums="1" tab=
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

```Ocaml linenums="1" tab=
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

```Rust linenums="1" tab=
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

```Ruby linenums="1" tab=
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

The user will have to fill the `fibonacci` method and the result will be printed into the stdout.  
Keep going with more tests:  
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

Sounds a bit static ?
You can add more complex tests using `random` method available by our runner:  
```Yaml
randt(n): random from 0 included to n excluded.
randft(n, m): random from n included to m excluded.
```
```Rust
{
    input: randft(20, 30),
    expected: ?
}
```
Which give us a problem, what to write for the expected value ?  
No worries! You can call your own solution instead of writing something static!
```Rust
{
    input: randft(20, 30),
    expected: call("java", "Solution.java")
},
{
    input: randt(20),
    expected: call("python", "solution.py")
}
```
It will be the same logic, your `solution.py` will be called by our Python interpreter with the *input* value
and you have to write the solution result to the *stdout*.  
For instance with Fibonacci:  
```Python
# solution.py
def fibo(n):
    if n <= 1:
       return n
    else:
       return(fibo(n - 1) + fibo(n - 2))

print(fibo(sys.argv[1]))
```

Then the *stdout* given with *print* will be compared with the user program.  
You can choose amoung these interpreters:  

|           |              |      |      |
| ----------|------------- |:----:|-----:|
| java      | javascript   | ruby | c    |
| rust      | python       | go   | cpp  |


#### Repeat
But what if you wish to execute 50 times a random test?
That's not a problem, add the **repeat** parameter to your test:
```Rust
{
    input: randt(20),
    expected: call("python", "solution.py"),
    repeat: 50
}
```

#### Input call
That's not all, you can also call your own program to generate the input:  
```Rust
{
    input: call("javascript", "generate.js"),
    expected: call("python", "solution.py")
}
```

#### Open a file
You can also open a file: 
```Rust
{
    input: open("file.txt"),
    expected: call("python", "solution.py")
}
```
It will be given as a *String* to the user.

Once you have complete the `entry.rs` you have to complete the `challenge.yaml` file:
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

The `success/` directory contains your solution given to the user when it succeeded the challenge.  
You can provide the implementation you wish.  

To test your program you can use [our CLI](https://pypi.org/project/deadlock-cli/):  
```Bash
> dcli run . java # Will run template/java/Main.java
> dcli solve . java # Will execute tests on template/java/Main.java
> dcli run . python # Will run template/python/Main.py
```

Each file placed within a template is provided if the user decide to change the current language.
For instance if the user decide to use *Rust* interpreter, all files under `template/rust` will be provided.

What's your challenge must like:
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

## Use dependencies
Please read the [Dependencies usage](metamorph-using-dependencies.md) documentation to take advantage of new possibilities.

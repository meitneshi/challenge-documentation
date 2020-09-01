# Want to use dependencies with a metamorph challenge ?

This section is made for you.

Keep in mind the metamorph structure:
```
.
├── challenge.yaml
├── entry.rs
├── runner
├── solution.js
├── success
│   └── Main.rs
└── template
    └── ...
```

## Installation

Basic runner image contains required stuff to install external dependencies for each supported language.

However, you __have to__ run this dependencies installation step form your *`Dockerfile`*.  So, it must be like this example:
```dockerfile
FROM <base-runner-image>
COPY <path-to-template-folder>/ template/
RUN install-dependencies.sh
```

## Runtime detection

A detection mechanism is based on the presence of one specific file.<br>
Please notice them in each related language section:

* [C](#c) - Makefile
* [C++](#c++) - Makefile
* [Go](#go) - go.mod
* [Java](#java) - pom.xml
* [Javascript](#javascript) - package.json
* [Kotlin](#kotlin) - pom.xml
* [Python](#python) - requirements.txt
* [Rust](#rust) - Cargo.toml


<!---------- Archive ---------->
## Ready-to-use example
This [example](https://github.com/deadlock-resources/challenge-examples/example/metamorph_using_dependencies) tells you how to use dependencies in a metamorph challenge.


<!---------- C ---------->
## C
Based on make.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── c
    │   ├── libs/       <i># optional folder</i>
    │   ├── Makefile    <b><i># detection file</i></b>
    │   └── Main.c
    └── ...
</pre>

Adding a *`Makefile`* allows you to create a complex multiple files challenge. The dependencies storage location depends on what you specify within your *`Makefile`*. We recommand to use the *`libs`* folder.


<!---------- CPP ---------->
## C++
Based on make.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── cpp
    │   ├── libs/       <i># optional folder</i>
    │   ├── Makefile    <b><i># detection file</i></b>
    │   └── Main.cpp
    └── ...
</pre>

Adding a *`Makefile`* allows you to create a complex multiple files challenge. The dependencies storage location depends on what you specify within your *`Makefile`*. We recommand to use the *`libs`* folder.


<!---------- GO ---------->
## Go
Based on go modules.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── go
    │   ├── go.mod    <b><i># detection file</i></b>
    │   └── Main.go
    └── ...
</pre>


<!---------- JAVA ---------->
## Java
Based on maven.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── java
    │   ├── libs/              <i># generated folder</i>
    │   ├── pom.xml            <b><i># detection file</i></b>
    │   └── Main.java
    └── ...
</pre>

The *`libs`* folder is created during the installion step to store required dependencies. It will be add to the classpath when compiling/running your code.


<!---------- JAVASCRIPT ---------->
## Javascript
Based on npm.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── javascript
    │   ├── package.json         <b><i># detection file</i></b>
    │   ├── package-lock.json    <i># optional file</i>
    │   └── Main.js
    └── ...
</pre>

The *`package-lock.json`* file is optional but [npm best practices](https://docs.npmjs.com/configuring-npm/package-lock-json.html) recommend to provide it.


<!---------- KOTLIN ---------->
## Kotlin
Based on maven.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── kotlin
    │   ├── libs/       <i># generated folder</i>
    │   ├── pom.xml     <b><i># detection file</i></b>
    │   └── Main.kt
    └── ...
</pre>

The *`libs`* folder is created during the installion step to store required dependencies. It will be add to the classpath when compiling/running your code.


<!---------- PYTHON ---------->
## Python
Based on pip.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── python
    │   ├── requirements.txt    <b><i># detection file</i></b>
    │   └── Main.py
    └── ...
</pre>


<!---------- RUST ---------->
## Rust
Based on cargo.

Minimal expected structure:
<pre>
.
├── ...
└── template
    ├── ...
    ├── rust
    │   ├── Cargo.lock    <i># optional file</i>
    │   ├── Cargo.toml    <b><i># detection file</i></b>
    │   └── src
    │       └── main.rs
    └── ...
</pre>

The *`Cargo.lock`* file is optional but [cargo best practices](https://doc.rust-lang.org/cargo/guide/cargo-toml-vs-cargo-lock.html) recommend to provide it.

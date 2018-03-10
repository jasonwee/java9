http://openjdk.java.net/projects/jigsaw/quick-start

intro
```
$ mkdir -p mods/com.greetings


$ javac -d mods/com.greetings \
    src/com.greetings/module-info.java \
    src/com.greetings/com/greetings/Main.java

$ java --module-path mods -m com.greetings/com.greetings.Main
```

dependency
```
$ mkdir -p mods/org.astro mods/com.greetings

$ javac -d mods/org.astro \
     src/org.astro/module-info.java src/org.astro/org/astro/World.java

$ javac --module-path mods -d mods/com.greetings \
     src/com.greetings/module-info.java src/com.greetings/com/greetings/Main.java

$ java --module-path mods -m com.greetings/com.greetings.Main
```

Multi-module compilation
```
$ mkdir mods

$ javac -d mods --module-source-path src $(find src -name "*.java")

$ find mods -type f
```

packaging
```
$ mkdir mlib

$ jar --create --file=mlib/org.astro@1.0.jar \
        --module-version=1.0 -C mods/org.astro .

$ jar --create --file=mlib/com.greetings.jar \
        --main-class=com.greetings.Main -C mods/com.greetings .

$ java -p mlib -m com.greetings

$ jar --describe-module --file=mlib/org.astro@1.0.jar
```

jlinker
```
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.greetings --output greetingsapp
```

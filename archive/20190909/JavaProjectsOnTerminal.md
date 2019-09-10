Starting IDE is a waste of time and vim is of course the bese editor on earth, compiling `java` files on remote server is basically what we should do without an IDE.



### What a `java` project looks like?

- Terminal Eclipse
  - src
    - package 1
      - test.java
  - Jre system library
  - Referenced Libraries
  - lib
    - common.jar
    - common2.jar

Say we are in `src/`

```bash
javac -cp '/home/jojo/Termainal\ Eclipse/lib/common.jar: /home/jojo/Termianal\ Eclipse/lib/common2.jar' package1/Test.java
```

then

```bash
java -cp '/home/jojo/Termainal\ Eclipse/lib/common.jar: /home/jojo/Termianal\ Eclipse/lib/common2.jar' package1.Test
```


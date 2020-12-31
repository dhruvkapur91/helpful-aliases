- Recently I had to play with several Java versions, this thing below keeps me sane :)

```bash
function useJava11() {
  jenv global openjdk64-11.0.7
  export JAVA_HOME=<your java path>
}

function useJava8() {
  jenv global openjdk64-1.8.0.242
  export JAVA_HOME=<your java path>
}

function useJava14() {
  jenv global openjdk64-14.0.1
  export JAVA_HOME=<your java path>
}

function useJava15() {
  jenv global openjdk64-15.0.1
  export JAVA_HOME=<your java path>
}
```
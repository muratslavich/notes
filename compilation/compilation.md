# Compilation java code

![](/notes/images/jvm-architecture.png)

[Работа с java  в командной строке](https://habr.com/en/post/125210/)  

-classpath . указывает на текущий каталог, можно опустить

```
javac Main.java
java -classpath . Main
```

-d folder указывает папку для бинарников

```
javac -d bin src/Main.java
java -classpath ./bin Main
```

необходимо подключить пакет в исходнике package com.slavich.hello;

```
$ javac -d bin src/com/slavich/hello/Main.java
$ java -classpath ./bin com.slavich.hello.Main
```

 -sourcepath ./src путь к исходникам необходимых для компиляции

```
$ javac -sourcepath ./src -d bin src/com/slavich/hello/Main.java

```

<details>
<summary>Some arguments</summary>

```
javac <options> <source files>
  -verbose                   Output messages about what the compiler is doing
  -classpath <path>          Specify where to find user class files and annotation processors
  -cp <path>                 Specify where to find user class files and annotation processors
  -sourcepath <path>         Specify where to find input source files
  -bootclasspath <path>      Override location of bootstrap class files
  -extdirs <dirs>            Override location of installed extensions
  -parameters                Generate metadata for reflection on method parameters
  -d <directory>             Specify where to place generated class files
  -s <directory>             Specify where to place generated source files
  -h <directory>             Specify where to place generated native header files
  -source <release>          Provide source compatibility with specified release
  -target <release>          Generate class files for specific VM version
  -profile <profile>         Check that API used is available in the specified profile
  -Akey[=value]              Options to pass to annotation processors
  -X                         Print a synopsis of nonstandard options
  -J<flag>                   Pass <flag> directly to the runtime system
  @<filename>                Read options and filenames from file
```

```
java [-options] class [args...]
 java [-options] -jar jarfile [args...]
    -d32          use a 32-bit data model if available                          
    -d64          use a 64-bit data model if available                          
    -server       to select the "server" VM. The default VM is server.                                     

    -cp <class search path of directories and zip/jar files>                    
    -classpath <class search path of directories and zip/jar files>             
              A ; separated list of directories, JAR archives,              
              and ZIP archives to search for class files.

    -D<name>=<value>                                                            
              set a system property                                         
    -verbose:[class|gc|jni]                                                     
              enable verbose output                                         
    -version      print product version and exit                                
    -version:<value>                                                            
              Warning: this feature is deprecated and will be removed       
              in a future release.                                          
              require the specified version to run                          
    -showversion  print product version and continue                            
    -jre-restrict-search | -no-jre-restrict-search                              
              Warning: this feature is deprecated and will be removed       
              in a future release.                                          
              include/exclude user private JREs in the version search       
    -? -help      print this help message                                       
    -X            print help on non-standard options

    -ea[:<packagename>...|:<classname>]                                         
    -enableassertions[:<packagename>...|:<classname>]                           
              enable assertions with specified granularity

    -da[:<packagename>...|:<classname>]                                         
    -disableassertions[:<packagename>...|:<classname>]                          
              disable assertions with specified granularity                 
    -esa | -enablesystemassertions                                              
              enable system assertions                                      
    -dsa | -disablesystemassertions                                             
              disable system assertions                                     
    -agentlib:<libname>[=<options>]                                             
              load native agent library <libname>, e.g. -agentlib:hprof     
              see also, -agentlib:jdwp=help and -agentlib:hprof=help        
    -agentpath:<pathname>[=<options>]                                           
              load native agent library by full pathname                    
    -javaagent:<jarpath>[=<options>]                                            
              load Java programming language agent, see java.lang.instrument
    -splash:<imagepath>                                                         
              show splash screen with specified image     
```

</details>    


[all java arguments](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/java.html)

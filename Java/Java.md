# Java
## Tools of the Trade
### JDK
Mac OS X : `export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_09.jdk/Contents/Home`

### The jar Utility
`jar -cvf jarFile path [ path ] [ ... ]` Create jarFile containing path(s)  
`jar -tvf jarFile [ path ] [ ... ]` List the contents of jarFile, optionally showing just path(s).  
`jar -xvf jarFile [ path ] [ ... ]` Extract the contents of jarFile, optionally extracting just path(s).  
The `f` means that the next argument is the name of the JAR file on which to operate.  
The optional `v` flag tells jar to be verbose when displaying information about files.  
eg: `jar -tf fs_sync-0.1.jar com` only list files under com folder in jar file, no verbose.  
#### manifest file
`jar -cvmf myManifest.mf spaceblaster.jar spaceblaster` add manifest info to jar file.  
`Main-Class: com.oreilly.Game` specify the class containing the primary main() method, then you can run the application directly from the JAR: `java -jar spaceblaster.jar`  
#### The pack200 Utility
The Java runtime does not understand the Pack200 format, so you cannot place archives of this type into the classpath. Instead, it is mainly an intermediate format that is very useful for transferring application JARs over the network for applets or other kinds of web-based applications.  
`pack200 fs_sync-0.1.pack.gz fs_sync-0.1.jar` convert jar to pack.gz  
`unpack200 fs_sync-0.1.pack.gz fs_sync-0.1.jar` convert pack.gz to jar  
Note that the Pack200 process completely tears down and reconstructs your classes at the class level, so the resulting foo.jar file will not be byte-for-byte the same as the original.  

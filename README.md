# gradle-delete-broken-symlink-fails

This repository contains a MCVE where Gradle 7.4 fails to delete a broken symlink. Also verified on Gradle 6.7 and 5.6.4.

Steps to reproduce:

```shell script
$ ./gradlew createSymlink

BUILD SUCCESSFUL in 473ms
2 actionable tasks: 2 executed

$ ls -lhd sample-*
drwxrwxr-x 2 slovdahl slovdahl 4,0K nov  4 11:24 sample-directory
lrwxrwxrwx 1 slovdahl slovdahl   16 nov  4 11:24 sample-symlink -> sample-directory

$ ./gradlew deleteDirectory

BUILD SUCCESSFUL in 442ms
1 actionable task: 1 executed

$ ./gradlew deleteSymlink

BUILD SUCCESSFUL in 441ms
1 actionable task: 1 up-to-date

$ ls -lhd sample-*
lrwxrwxrwx 1 slovdahl slovdahl 16 nov  4 11:24 sample-symlink -> sample-directory

$ ./gradlew deleteSymlinkWithFollowSymlinksTrue

BUILD SUCCESSFUL in 441ms
1 actionable task: 1 up-to-date

$ ls -lhd sample-*
lrwxrwxrwx 1 slovdahl slovdahl 16 nov  4 11:24 sample-symlink -> sample-directory
```

# Jar Loader

![jar loader icon](readme/images/coffee-jar.png)

## What is it?

Easy migration to Java 9+ for applications that extend the class path by reflective access to the class loader.

Does your code work under Java 8 but fail under Java 9+ with an error stating that the system class loader is not an instance of `URLClassLoader` or that the method `addURL` could not be found? *Then this is for you.*

## How to use it

Three steps:

1. Add `jar-loader.jar` to your build libraries and application class path.
2. Add `-javaagent:path/to/jar-loader.jar` to the VM options passed to the `java` command used to start your application.
3. Where your code previously used reflection to invoke `addURL` on the system class loader, instead call `ca.cgjennings.jvm.JarLoader.addToClassPath(File jarFile)`.

### Notes

*Jar Loader* uses an official, documented method for extending the class path at runtime that has been supported since Java 6. It falls back to attempting reflective access if that fails. This method differs from `URLClassLoader` in that it only supports local JAR files. If your code relies on `addURL` to download code over a network, you will have to download it yourself and write it to a local file.

If you move the compiled `JarLoader` class to a different JAR file, it must include a `MANIFEST.MF` with the following line:

`Premain-Class: ca.cgjennings.vm.JarLoader`



---

**Image credit:** icon adapted from an icon by [Eucalyp](https://www.flaticon.com/authors/eucalyp).
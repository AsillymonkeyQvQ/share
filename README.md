In fact it depends on many factors:

If both jar files are in the same ClassLoader, for instance the Java classpath (-cp option), normally it should be the first file found in the jar list order.
If deployed in a JavaEE container, like in an EAR file or in WEB-INF/lib or a WAR file, there is no warranty the container will load the same class between two startups. In that context, the only thing sure is that WEB-INF/classes is searched before WEB-INF/lib
In a complex ClassLoader hierarchy, the default behavior is parent-first search but JavaEE implementations have introduced mechanisms like parent-last policy (WebSphere) or filtering thanks to deployment descriptors (WebLogic, JBoss/WildFly)
An option may be to declare jar file dependencies in META-INF/MANIFEST.MF file thanks to the Class-Path attribute. It should enforce a loading order at the ClassLoader level, particularly when started with java -jar myapp.jar but it may depend on implementations in a JavaEE context.

Remark: when using an OpenSource project, it may be fair to submit a change request and publish your changes or improvements so that the community takes benefits from it. Then your project may update to main stream without such a difficulty of wild patches in your ClassPath.

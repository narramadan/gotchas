# Java 8 Streams

## Create List of Objects from another List of Objects

```java
List<ClassA> classAObjects = service.fetchClassAObjects();

List<ClassB> classBObjects = 
    classAObjects.stream().map(objectA -> {
        ClassB objectB = new ClassB();
        objectB.setProp1(objectA.getProp1());
        objectB.setProp2(objectA.getProp2());

        return objectB;
    }).collect(Collectors.toList());

classBObjects.forEach(System.out::println);
```

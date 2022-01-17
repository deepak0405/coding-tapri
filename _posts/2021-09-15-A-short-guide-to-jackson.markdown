---
layout: post
title:  "A short guide on java polymorphic deserialization"
date:   2021-09-15 15:39:31 +0530
comments_id: 6
---

Jackson is the java library to perform serialization and deserialization. So whenever we want to convert a JSON to Java object (deserialization) or whenever we want to convert a Java Object to JSON, we can use the jackson library.

The polymorphic deserialization refers to deserializing the JSON into any of the subclass based on the type information present in the JSON.

Take an example of Zoo class. If we are given a JSON representation of the zoo class, how our java runtime will know whether it should create an object of type Dog or Cat ?


```
  public class Zoo {
    public Animal animal;
  }

  static class Animal { // All animals have names, for our demo purposes... 
     public String name;
     protected Animal() { }
  }

  static class Dog extends Animal {
    public double barkVolume; // in decibels
    public Dog() { }
  }

  static class Cat extends Animal {
    boolean likesCream;
    public int lives;
    public Cat() { }
  }
```

We can use the jackson annotation to let the library know how it can serialize/deserialize a particular object.

The annotation is applied on the parent class as shown below

```
 @JsonTypeInfo(use=JsonTypeInfo.Id.CLASS, include=JsonTypeInfo.As.PROPERTY, property="@class")
 class Animal { } 
```

### What does that mean?

* All instances of annotated type and its subtypes use these settings (unless overridden by another annotation)
* "Type identifier" to use is fully-qualified Java class name (like "org.codehaus.jackson.sample.Animal")
* Type identifier is to be included as a (meta-)property, along with regular data properties; using name "@class" (default name to use depend on type if: for classes it would be "@class")
* Use default type resolver (no @JsonTypeResolver added); as well as default type id resolver (no @JsonTypeIdResolver)


### We could have chosen differently as follows:

* Type id: possible choices are CLASS (fully-qualified Java class name), MINIMAL_CLASS (relative Java class name, if base class and sub-class are in same package, leave out package name), NAME (use logical name, separately defined, to determine actual class) and CUSTOM (type id handled using custom resolver)
* Inclusion: possible choices are PROPERTY (include as regular property along with member properties), WRAPPER_OBJECT (use additional JSON wrapper object; type id used as field name, actual serializer Object as value), WRAPPER_ARRAY (first element is type id; second element serialized Object)
* Property name: for inclusion method of PROPERTY, can use any name; defaults depend on type id.
* To plug in custom type id resolver use @JsonTypeIdResolver
* To plug in custom type resolver use @JsonTypeResolver


Reference: https://github.com/FasterXML/jackson-docs/wiki/JacksonPolymorphicDeserialization

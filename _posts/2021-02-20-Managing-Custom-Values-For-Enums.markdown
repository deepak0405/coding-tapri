---
layout: post
title:  "Managing enums with custom values"
date:   2021-02-20 18:39:31 +0530
comments_id: 7
---

Did you came across a use case where you wanted to add a custom value for a enum ? The most common form in which an enum is used is

```
public enum Animal {
    DOG,
    CAT
}
```

We had a special case where 
1. We wanted to return to value Dog (instead of DOG) and Cat(Instead of CAT) to the users in API.
2. Use the custom value of the enum in our internal logics.

How can we solve this problem using the same enum class?

We can define a custom value for our enum like:

```
public enum Animal {
  @JsonProperty("Dog") DOG("Dog"),
  @JsonProperty("Cat") Cat("Cat")

  private final String displayName;

  Animal(String displayName) {
    this.displayName = displayName;
  }

  @JsonValue
  public String getDisplayName() {
    return displayName;
  }

  @Override
  public String toString() {
    return displayName;
  }

  @JsonCreator(mode = JsonCreator.Mode.DELEGATING)
  public static Animal getAnimalEnum(@JsonProperty("type") String displayName) {
    for (Animal animalType : Animal.values()) {
      if (animalType.displayName.equalsIgnoreCase(displayName)) {
        return animalType;
      }
    }
    throw new IllegalArgumentException("Invalid value: " + displayName);
  }
}
```

Description of the above code example:

* We have define the value custom value as the displayName of the enum
* When we are deserializing a value to Animal enum the function with the annotation `JsonCreator` will be called
* When we are serializing the enum value the function with the `JsonValue` annotation is called


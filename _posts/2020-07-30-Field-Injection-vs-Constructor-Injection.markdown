---
layout: post
title:  "Field Injection vs Constructor Injector"
date:   2020-07-30 19:39:31 +0530
comments_id: 5
---

If we use Guice for managing the dependency injection, then you can either use Field Injection or Dependency Injection. Out of the two which way we should prefer?

<!--more-->

The options are


1.  Field Injection

In field injection, the Guice sets the required dependency into the field of our class using reflection.

```
    public class UserService {
        @Inject AuthService authService;
        ...
    }
```

2. Constructor Injection

In constructor injection, the Guice uses the constructor to add the dependency object to our dependent object. 
```
    public class UserService {
        AuthService authService;
        
        @Inject
        public UserService(AuthService authService){
            authService = authService;
        }
    }
```

Though both of this approach works, which approach should we select ?

I prefer the constructor injection because: 

* I feel that the Field Injection is auto magic as we don't know how the field value is set
* It violates OOPs principles too as we are updating a private field from the outside.
* Also dependency injection using constructor is faster than setting each field using reflection
* For me the field injection doesn't work with @Named annotation (might be a bug in the version I am using)


Reference:  https://softwareengineering.stackexchange.com/questions/300706/dependency-injection-field-injection-vs-constructor-injection
---
layout: post
title:  "Field Injection vs Constructor Injector"
date:   2020-07-30 19:39:31 +0530
comments_id: 5
---

If we use Guice for managing the dependency injection, then we have to option to inject a dependency in a class. The options are

1.  Field Injection

```
    public class UserService {
        @Inject AuthService authService;
        ...
    }
```

2. Constructor Injection
```
    public class UserService {
        AuthService authService;
        
        @Inject
        public UserService(AuthService authService){
            authService = authService;
        }
    }
```

Reference:  https://softwareengineering.stackexchange.com/questions/300706/dependency-injection-field-injection-vs-constructor-injection
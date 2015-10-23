# Cutting Angular cross-cuts

## Links
* slides: https://speakerdeck.com/mgechev/cutting-angulars-crosscuts
* aspect.js https://github.com/mgechev/aspect.js

## SOLID
* Single responsibility principle (SRP)
* Open closed principle (OCP)
* Liskov substitution principle (LSP)
* Interface segregation principle (ISP)
* Dependency injection principle (DIP)

## Caching
Caching crosscut levels of abstractions.
Caching is a cross-cutting concern

These must be separated: caching, logging, ..

## Caching aspect example

```
èxport class CacheAspect {
    beforeUserFinderGetInvocation(meta, id) {
        this.queryCache(lsCache, meta.method, id);
    }

    afterUserFinderGetInvocation(meta,id){
        this.setCache(lsCache, meta.method, id);
    }

    // same for Http
}
```

## Using an aspect
* AspectJS library: aspect.js

... example


---
title: OpenApi Springdoc setup
feed: show
date: 28-04-2024
---
> Doksi: https://springdoc.org

Java17-tel, Springboot 3-mal a következő a minimum dependencia:
```kotlin
implementation("org.springdoc:springdoc-openapi-starter-webmvc-ui:2.1.0")
```

Ha kicsit fel akarjuk turbózni, be kell húzni a common-t is:
```kotlin
  implementation("org.springdoc:springdoc-openapi-starter-common:2.1.0")
```

Ez azért jó, mert elősegíti a Kotlin használatát, pl. támogatott a [[dto-validation]] validációs annotációk segítségével a dokumentáció kibővítése. (lsd. min-max feltételek.)
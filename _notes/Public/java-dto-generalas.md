---
title: Java DTO generálás CLI-ből (XSD / WSLT)
feed: show
date: 23-02-2024
---

Intellij IDEA Ultimate-ből elég egyszerűen lehet .xsd-ből java classokat generálni, csakhogy nem mindig mindenkinél van ultimate, for obvious reasons.

Fel kell hozzá tenni a jaxb-t, JDK 11 óta nem része a JDK-nak.

[https://github.com/eclipse-ee4j/jaxb-ri](https://github.com/eclipse-ee4j/jaxb-ri)

[Jakarta XML Binding](https://eclipse-ee4j.github.io/jaxb-ri/)

**Példa futtatás:**

```bash
xjc -d out -npa -no-header -p hu.tothlp.proba data.xsd
```

WSDL mehet intellij-ből, de fel kell tenni, pl `C:\jaxws-ri` alá:

[Maven Repository: com.sun.xml.ws » jaxws-ri » 4.0.2](https://mvnrepository.com/artifact/com.sun.xml.ws/jaxws-ri/4.0.2)

Ezt beállítani a Settings/Tools/WebServices alatt.
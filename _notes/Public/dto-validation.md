---
title: Kotlin - DTO validálás
feed: show
date: 23-02-2024
---

Ez egy igen régi probléma. Ez most a legutóbbi működő verzió, Jakartával működik már a javax package-ek helyett, szóval eléggé up-to-date.

Ami kell hozzá:

```kotlin
implementation("org.springframework.boot:spring-boot-starter-validation")
```

A DTO-ra kell controllerből a `@Valid`

```kotlin
fun createUser(@RequestBody @Valid request: UserCreateRequest) = 
    userService.createUser(request)
```

DTO szinten a validációs annotációk pedig a getterre kellenek:

```kotlin
data class UserCreateRequest(
    val userCode: String,

    val fullName: String,

    @Optional
    @get:Email(regexp = Constants.EMAIL_REGEX)
    val email1: String?,

    @Optional
    @get:Email(regexp = Constants.EMAIL_REGEX)
    val email2: String?,

    @get:JsonFormat(shape = JsonFormat.Shape.STRING, pattern = Constants.DATE_TIME_FORMAT_PATTERN)
    val validityStart: LocalDateTime,

    @Optional
    @get:JsonFormat(shape = JsonFormat.Shape.STRING, pattern = Constants.DATE_TIME_FORMAT_PATTERN)
    val validityEnd: LocalDateTime?,

    val password: String,

    val passwordAgain: String?
)
```

Email validációhoz: Működik a sima is, de érdemes saját regexet megadni, mert az eredeti megengedi a laci@hello jellegű címeket is…

```kotlin
/**
         * See: https://emailregex.com/. The email validation of spring simply accepts user@domain type strings, without country code.
         */
        const val EMAIL_REGEX =
            "(?:[a-z0-9!#\$%&'*+/=?^_`{|}~-]+(?:\\.[a-z0-9!#\$%&'*+/=?^_`{|}~-]+)*|\"(?:[\\x01-\\x08\\x0b\\x0c\\x0e-\\x1f\\x21\\x23-\\x5b\\x5d-\\x7f]|\\\\[\\x01-\\x09\\x0b\\x0c\\x0e-\\x7f])*\")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\\x01-\\x08\\x0b\\x0c\\x0e-\\x1f\\x21-\\x5a\\x53-\\x7f]|\\\\[\\x01-\\x09\\x0b\\x0c\\x0e-\\x7f])+)\\])"
    }
}
```

Ha összetett object-et kell validálni, akkor nem elég a Controllerben feltenni a `@Valid` annotációt, hanem a child objectekre is kell. Pl:

```kotlin
import javax.validation.Valid
import javax.validation.constraints.NotBlank

data class DocumentRequest(
	@field:NotBlank var ucr: String,
	@field:Valid var okmany: Document
)

data class Document(
	@field:NotBlank var fajlnev: String,
	var tartalom: String
)
```
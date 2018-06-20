# Code guidelines

## Guidelines

We adhere to the [Android Kotlin Guides](https://android.github.io/kotlin-guides/) for our code style. These represent Google's Android coding standards for Kotlin source code. As such we intend to adopt them.

Any deviations from this guide should documented here.

## Tooling

### Auto formatting

Ensure that you regularly use the Android Studio 'Reformat Code' (ALT+CMD+L) tool which will reformat a file to match your code style settings. This should, as a minimum, be used before a submission is made on every file that you have changed in that submission. It is possible to set Android Studio to automatically run this, on file save.

### Static Analysis

We use [detekt](https://github.com/arturbosch/detekt) and [ktlint](https://ktlint.github.io/) to support our coding styles. These have been configured in accordance with the guide.

Note: See [ktlint-rules](https://github.com/brightec/ktlint-rules_Kotlin) for our custom rules.

#### Integration

To integrate these tools you should, copy the "config" folder into the project:
```
-config
  -misc
    -apknaming.gradle
  -quality
    -detekt
      detekt-config.yml
    -ktlint
      -libs
        ktlint-rules-[version].jar
    lint.xml
    quality.gradle
  proguard-rules.pro
  proguardTest-rules.pro
```
Then you can use commands:
* ```./gradlew ktlint``` - to run a variety of checks
* ```./gradlew ktlintFormat``` - to run an automatic formatter (limited implementation, but helpful)
* ```./gradlew detekt``` - to run a variety of checks
* ```./gradlew check``` - to run both ktlint, detekt, lint and tests

## Addendum

- [Named Parameters](#named-parameters)
- [Lambdas](#lambdas)

### Named Parameters

When calling any function (not possible when calling java functions) with more than 2 parameters, you must make use of the named parameters language feature.

__BAD:__

```kotlin
myFunction(1, true, ourString)
```

__GOOD:__

```kotlin
myFunction(parameterSize = 1, isNecessary = true, name = ourString)
```

It is not considered bad practice either way for functions of 2 parameters or less.

The same style should be applied to constructor invocation too.

Exception: Classes which represent tuples (e.g. Triple) or lists (e.g. listOf()), do not need to be invoked using named parameters. This is because they provide no clarity and the invocation should always be done in order regardless.
E.g. ```Triple(objA, objB, objC)``` NOT ```Triple(first = objA, second = objB, third = objC)```

Exception: If all parameters being passed are identical then naming is not required, however is encouraged if it brings extra clarity. E.g. ```repo.someMethod(any(), any(), any())``` is acceptable. ```repo.someMethod(shouldBe1, 1, 1)``` is not.

### Lambdas

When using lambdas, naming of parameters is required when:
- More than one parameter is present or;
- When nesting within the lamdba. 

```it``` can become unclear when its not the simpliest case. Use good judgement to make sure your ```it``` is clear enough, otherwise name it.

__BAD:__

```kotlin
list.forEach {
    list2.forEach {
        //some code
    }
}
```

__GOOD:__

```kotlin
list.forEach { item1 ->
    list2.forEach { item2 ->
        //some code
    }
}
```

Note that the use of a named parameter on the inner most lambda is not required. However the same judgement should be used to ensure code clarity.

The use of ```_``` is encouraged for parameters which are not going to be used. This helps a reader understand that you had no intention of using that parameter, as opposed to not using it by mistake.

## License

```
Copyright 2018 Brightec Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

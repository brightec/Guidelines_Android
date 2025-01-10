# Code guidelines

## Guidelines

We adhere to the [Android Kotlin Guides](https://developer.android.com/kotlin/style-guide) for our code style. These represent Google's Android coding standards for Kotlin source code. As such we intend to adopt them.

Any deviations from this guide should documented here.

## Tooling

### Auto formatting

Ensure that you regularly use the Android Studio 'Reformat Code' (ALT+CMD+L) tool which will reformat a file to match your code style settings. This should, as a minimum, be used before a submission is made on every file that you have changed in that submission. It is possible to set Android Studio to automatically run this, on file save.

### Static Analysis

We use [detekt](https://github.com/arturbosch/detekt) and [ktlint](https://ktlint.github.io/) to support our coding styles. These have been configured in accordance with the guide.

Note: See [ktlint-rules](https://github.com/brightec/ktlint-rules_Kotlin) for our custom rules. _(internal use only)_

## Addendum

- [Lambdas](#lambdas)

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
Copyright 2025 Brightec Ltd.

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

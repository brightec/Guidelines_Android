# Code guidelines

Ensure that you regularly use the Android Studio 'Reformat Code' (ALT+CMD+L) tool which will reformat a file to match your code style settings. This should, as a minimum, be used before a submission is made on every file that you have changed in that submission. This will reduce the code review time and keep the code tidier.

## Table of Contents

- [1 Java language rules](#1-java-language-rules)
  + [1.1 Don't ignore exceptions](#11-dont-ignore-exceptions)
  + [1.2 Don't catch generic exception](#12-dont-catch-generic-exception)
  + [1.3 Don't use finalizers](#13-dont-use-finalizers)
  + [1.4 Fully qualify imports](#14-fully-qualify-imports)
- [2 Java style rules](#2-java-style-rules)
  + [2.1 Fields definition and naming](#21-fields-definition-and-naming)
  + [2.2 Treat acronyms as words](#22-treat-acronyms-as-words)
  + [2.3 Use spaces for indentation](#23-use-spaces-for-indentation)
  + [2.4 Use standard brace style](#24-use-standard-brace-style)
  + [2.5 Annotations](#25-annotations)
    + [2.5.1 Annotations practices](#251-annotations-practices)
    + [2.5.2 Annotations style](#252-annotations-style)
  + [2.6 Limit variable scope](#26-limit-variable-scope)
  + [2.7 Order import statements](#27-order-import-statements)
  + [2.8 Logging guidelines](#28-logging-guidelines)
  + [2.9 Class member ordering](#29-class-member-ordering)
  + [2.10 Parameter ordering in methods](#210-parameter-ordering-in-methods)
  + [2.11 String constants, naming, and values](#211-string-constants-naming-and-values)
  + [2.12 Arguments in Fragments and Activities](#212-arguments-in-fragments-and-activities)
  + [2.13 Line length limit](#213-line-length-limit)
    + [2.13.1 Line-wrapping strategies](#2131-line-wrapping-strategies)
  + [2.14 Short methods, clear names](#214-short-methods-clear-names)
- [3 Tests style rules](#3-tests-style-rules)
  + [3.1 Unit tests](#31-unit-tests)
  + [3.2 Espresso tests](#32-espresso-tests)
- [4 Comments](#4-comments)
  + [4.1 Todo's](#41-todos)
    + [4.1.1 TODO](#411-todo)
    + [4.1.2 FIXME](#412-fixme)
    + [4.1.3 IMPROVE](#413-improve)
    + [4.1.4 STOPSHIP](#414-stopship)
- [License](#license)

## 1 Java language rules

### 1.1 Don't ignore exceptions

You must never do the following:

```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```

_While you may think that your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions like above creates mines in your code for someone else to trip over some day. You must handle every Exception in your code in some principled way. The specific handling varies depending on the case._ - ([Android code style guidelines](https://source.android.com/source/code-style.html))

See alternatives [here](https://source.android.com/source/code-style.html#dont-ignore-exceptions).

### 1.2 Don't catch generic exception

You should not do this:

```java
try {
    someComplicatedIOFunction();        // may throw IOException
    someComplicatedParsingFunction();   // may throw ParsingException
    someComplicatedSecurityFunction();  // may throw SecurityException
    // phew, made it all the way
} catch (Exception e) {                 // I'll just catch all exceptions
    handleError();                      // with one generic handler!
}
```

See the reason why and some alternatives [here](https://source.android.com/source/code-style.html#dont-catch-generic-exception)

### 1.3 Don't use finalizers

_We don't use finalizers. There are no guarantees as to when a finalizer will be called, or even that it will be called at all. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a `close()` method (or the like) and document exactly when that method needs to be called. See `InputStream` for an example. In this case it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs._ - ([Android code style guidelines](https://source.android.com/source/code-style.html#dont-use-finalizers))


### 1.4 Fully qualify imports

This is bad: `import foo.*;`

This is good: `import foo.Bar;`

See more info [here](https://source.android.com/source/code-style.html#fully-qualify-imports)
Use Android Studio tool by right-click on file then select Optimize Imports. This should, as a minimum, be used before a submission is made on every file that you have changed in that submission.

## 2 Java style rules

### 2.1 Fields definition and naming

Fields should be defined at the __top of the file__ and they should follow the naming rules listed below.

* Private, non-static field names start with __m__.
* Private, static field names start with __s__.
* Other fields start with a lower case letter.
* Static final fields (constants) are ALL_CAPS_WITH_UNDERSCORES.

Example:

```java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

### 2.2 Treat acronyms as words

| Good           | Bad            |
| -------------- | -------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |

### 2.3 Use spaces for indentation

Use __4 space__ indents for blocks:

```java
if (x == 1) {
    x++;
}
```

Use __8 space__ indents for line wraps:

```java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
```

### 2.4 Use standard brace style

Braces go on the same line as the code before them.

```java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```

Braces around the statements are required unless it's a return, break or continue e.g.

```java
if (condition) return;
```

These are __bad__:

```java
if (condition)
    body();  // bad!
```
```java
if (condition) body();  // bad!
```

### 2.5 Annotations

#### 2.5.1 Annotations practices

According to the Android code style guide, the standard practices for some of the predefined annotations in Java are:

* `@Override`: The @Override annotation __must be used__ whenever a method overrides the declaration or implementation from a super-class. For example, if you use the @inheritdocs Javadoc tag, and derive from a class (not an interface), you must also annotate that the method @Overrides the parent class's method.

* `@SuppressWarnings`: The @SuppressWarnings annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this "impossible to eliminate" test, the @SuppressWarnings annotation must be used, so as to ensure that all warnings reflect actual problems in the code.

More information about annotation guidelines can be found [here](http://source.android.com/source/code-style.html#use-standard-java-annotations).

#### 2.5.2 Annotations style

__Classes, Methods and Constructors__

When annotations are applied to a class, method, or constructor, they are listed after the documentation block and should appear as __one annotation per line__ .

```java
/* This is the documentation block about the class */
@AnnotationA
@AnnotationB
public class MyAnnotatedClass { }
```

__Fields__

Annotations applying to fields should be listed __on the same line__, unless the line reaches the maximum line length.

```java
@Nullable @Mock DataManager mDataManager;
```

### 2.6 Limit variable scope

_The scope of local variables should be kept to a minimum (Effective Java Item 29). By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error. Each variable should be declared in the innermost block that encloses all uses of the variable._

_Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. If you don't yet have enough information to initialize a variable sensibly, you should postpone the declaration until you do._ - ([Android code style guidelines](https://source.android.com/source/code-style.html#limit-variable-scope))

### 2.7 Order import statements

If you are using an IDE such as Android Studio, you don't have to worry about this because your IDE is already obeying these rules. If not, have a look below.

The ordering of import statements is:

1. Android imports
2. Imports from third parties (com, junit, net, org)
3. java and javax
4. Same project imports

To exactly match the IDE settings, the imports should be:

* Alphabetically ordered within each grouping, with capital letters before lower case letters (e.g. Z before a).
* There should be a blank line between each major grouping (android, com, junit, net, org, java, javax).

More info [here](https://source.android.com/source/code-style.html#limit-variable-scope)

### 2.8 Logging guidelines

Use the logging methods provided by the `Logger` class in the brighteccomponents library to print out error messages or other information that may be useful for developers to identify issues:

* `Logger.v(Class clazz, String msg)` (verbose)
* `Logger.d(Class clazz, String msg)` (debug)
* `Logger.i(Class clazz, String msg)` (information)
* `Logger.w(Class clazz, String msg)` (warning)
* `Logger.e(Class clazz, String msg)` (error)

Note that the `Logger` class will only log messages if in a DEBUG build.

If you need a custom tag then you can use `(String tag, String msg)` methods, however this should not be the norm.

### 2.9 Class member ordering

There is no single correct solution for this but using a __logical__ and __consistent__ order will improve code learnability and readability. It is recommendable to use the following order:

1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces

Example:

```java
public class MainActivity extends Activity {

	private String mTitle;
    private TextView mTextViewTitle;

    public void setTitle(String title) {
    	mTitle = title;
    }

    @Override
    public void onCreate() {
        ...
    }

    private void setUpView() {
        ...
    }

    static class AnInnerClass {

    }

}
```

If your class is extending an __Android component__ such as an Activity or a Fragment, it is a good practice to order the override methods so that they __match the component's lifecycle__. For example, if you have an Activity that implements `onCreate()`, `onDestroy()`, `onPause()` and `onResume()`, then the correct order is:

```java
public class MainActivity extends Activity {

	//Order matches Activity lifecycle
    @Override
    public void onCreate() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}

    @Override
    public void onDestroy() {}

}
```

### 2.10 Parameter ordering in methods

When programming for Android, it is quite common to define methods that take a `Context`. If you are writing a method like this, then the __Context__ must be the __first__ parameter.

The opposite case are __callback__ interfaces that should always be the __last__ parameter.

Examples:

```java
// Context always goes first
public User loadUser(Context context, int userId);

// Callbacks always go last
public void loadUserAsync(Context context, int userId, UserCallback callback);
```

### 2.11 String constants, naming, and values

Many elements of the Android SDK such as `SharedPreferences`, `Bundle`, or `Intent` use a key-value pair approach so it's very likely that even for a small app you end up having to write a lot of String constants.

When using one of these components, you __must__ define the keys as a `static final` fields and they should be prefixed as indicated below.

| Element            | Field Name Prefix |
| -----------------  | ----------------- |
| SharedPreferences  | `PREF_`             |
| Bundle             | `BUNDLE_`           |
| Fragment Arguments | `ARG_`         |
| Intent Extra       | `EXTRA_`            |
| Intent Action      | `ACTION_`           |
| Request Code      | `REQUEST_`           |

Note that the arguments of a Fragment - `Fragment.getArguments()` - are also a Bundle. However, because this is a quite common use of Bundles, we define a different prefix for them.

Example:

```java
// Note the value of the field is the same as the name to avoid duplication issues
static final String PREF_EMAIL = "PREF_EMAIL";
static final String BUNDLE_AGE = "BUNDLE_AGE";
static final String ARG_USER_ID = "ARG_USER_ID";
static final String EXTRA_SURNAME = "EXTRA_SURNAME";
static final String ACTION_OPEN_USER = "ACTION_OPEN_USER";
```

### 2.12 Arguments in Fragments and Activities

When data is passed into an `Activity `or `Fragment` via an `Intent` or a `Bundle`, the keys for the different values __must__ follow the rules described in the section above.

When an `Activity` or `Fragment` expects arguments, it should provide a `public static` method that facilitates the creation of the relevant `Intent` or `Fragment`.

In the case of Activities the method is usually called `getStartIntent()`:

```java
public static Intent getStartIntent(Context context, User user) {
	Intent intent = new Intent(context, ThisActivity.class);
	intent.putParcelableExtra(EXTRA_USER, user);
	return intent;
}
```

For Fragments it is named `newInstance()` and handles the creation of the Fragment with the right arguments:

```java
public static UserFragment newInstance(User user) {
	UserFragment fragment = new UserFragment;
	Bundle args = new Bundle();
	args.putParcelable(ARG_USER, user);
	fragment.setArguments(args)
	return fragment;
}
```

__Note 1__: These methods should go at the top of the class before `onCreate()`.

__Note 2__: If we provide the methods described above, the keys for extras and arguments should be `private` because there is no need for them to be exposed outside the class.

### 2.13 Line length limit

Code lines should not exceed __130 characters__. If the line is longer than this limit there are usually two options to reduce its length:

* Extract a local variable or method (preferable).
* Apply line-wrapping to divide a single line into multiple ones.

There are two __exceptions__ where it is possible to have lines longer than 130:

* Lines that are not possible to split, e.g. long URLs in comments.
* `package` and `import` statements.

#### 2.13.1 Line-wrapping strategies

There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However there are a few rules that can be applied to common cases.

__Break at operators__

When the line is broken at an operator, the break comes __before__ the operator. For example:

```java
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne
        + theFinalOne;
```

__Assignment Operator Exception__

An exception to the `break at operators` rule is the assignment operator `=`, where the line break should happen __after__ the operator.

```java
int longName =
        anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne + theFinalOne;
```

__Method chain case__

When multiple methods are chained in the same line - for example when using Builders - every call to a method should go in its own line, breaking the line before the `.`

```java
Picasso.with(context).load("http://google.com/images/example.jpg").into(imageView);
```

```java
Picasso.with(context)
        .load("http://google.com/images/example.jpg")
        .into(imageView);
```

__Long parameters case__

When a method has many parameters or its parameters are very long, we should break the line after every comma `,`

```java
loadPicture(context, "http://google.com/images/example.jpg", mImageViewProfilePicture, clickListener, "Title of the picture");
```

```java
loadPicture(context,
        "http://google.com/images/example.jpg",
        mImageViewProfilePicture,
        clickListener,
        "Title of the picture");
```

### 2.14 Short methods, clear names

Methods should be short and stick to one function. This makes the code easier to read and test. The method name should reflect clearly what that function is, with more detail included in the Javadoc comment.

[here](https://source.android.com/source/code-style.html#write-short-methods)

## 3 Tests style rules

### 3.1 Unit tests

Test classes should match the name of the class the tests are targeting, followed by `Test`. For example, if we create a test class that contains tests for the `DatabaseHelper`, we should name it `DatabaseHelperTest`.

Test methods are annotated with `@Test` and should generally start with the name of the method that is being tested, followed by a precondition and/or expected behaviour.

* Template: `@Test void methodNamePreconditionExpectedBehaviour()`
* Example: `@Test void signInWithEmptyEmailFails()`

Precondition and/or expected behaviour may not always be required if the test is clear enough without them.

Sometimes a class may contain a large amount of methods, that at the same time require several tests for each method. In this case, it's recommendable to split up the test class into multiple ones. For example, if the `DataManager` contains a lot of methods we may want to divide it into `DataManagerSignInTest`, `DataManagerLoadUsersTest`, etc. Generally you will be able to see what tests belong together because they have common [test fixtures](https://en.wikipedia.org/wiki/Test_fixture).

### 3.2 Espresso tests

Every Espresso test class usually targets an Activity, therefore the name should match the name of the targeted Activity followed by `Test`, e.g. `SignInActivityTest`

When using the Espresso API it is a common practice to place chained methods in new lines.

```java
onView(withId(R.id.view))
        .perform(scrollTo())
        .check(matches(isDisplayed()))
```

## 4 Comments

You should be extensively using comments to help explain to the reader what your code was intending to do. This helps other readers understand your code and spot mistakes. As a minimum any public methods should have comments attached explaining what that method does. [Javadoc info](https://source.android.com/source/code-style.html#use-javadoc-standard-comments)

### 4.1 Todo's

The use of todo's is encouraged and can be very useful if used correctly. All todo's should adhear to the following format:  
`{Type} : {Name} {Date} : {Msg}`  
For example, in Java:  
`// TODO : joebloggs 01/01/2000 : Complete this method which should do this thing`

These formats are included in the Android Studio shared settings.

#### 4.1.1 TODO

TODO should be used when you have a task which needs to be completed.

#### 4.1.2 FIXME

FIXME should be used when the code which has been written needs fixing.

#### 4.1.3 IMPROVE

IMPROVE should be used when you recognise that the code is working but could be made more efficient.

#### 4.1.4 STOPSHIP

STOPSHIP should be used to mark something which absolutely cannot go out in a release build.

## License

```
Copyright 2022 Brightec Ltd.

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

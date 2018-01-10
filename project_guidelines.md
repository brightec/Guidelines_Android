# Project guidelines

## Table of Contents

- [1 Project structure](#1-project-structure)
- [2 File naming](#2-file-naming)
  + [2.1 Class files](#21-class-files)
  + [2.2 Resources files](#22-resources-files)
    + [2.2.1 Drawable files](#221-drawable-files)
    + [2.2.2 Layout files](#222-layout-files)
    + [2.2.3 Menu files](#223-menu-files)
    + [2.2.4 Values files](#224-values-files)
- [License](#license)

## 1 Project structure

New projects should follow the Android Gradle project structure that is defined on the [Android Gradle plugin user guide](http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Project-Structure).

## 2 File naming

### 2.1 Class files
Class names are written in [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

For classes that extend an Android component, the name of the class should end with the name of the component; for example: `SignInActivity`, `SignInFragment`, `ImageUploaderService`, `ChangePasswordDialog`.

### 2.2 Resources files

Resources file names are written in __lowercase_underscore__.

#### 2.2.1 Drawable files

Naming conventions for drawables:


| Asset Type   | Prefix            |		Example               |
|--------------| ------------------|-----------------------------|
| Background   | `bg_`             | `bg_screen1.9.png`          |
| Button       | `btn_`	            | `btn_send_pressed.9.png`    |
| Icon         | `ic_`	            | `ic_star.png`               |

__All icons should follow `ic_{{name}}_{{color}}_{{size}}dp`__. See [Material Icons Guide](https://google.github.io/material-design-icons/).

Note: Occasionally color won't be applicable, in which case don't include it. If the resource isn't square, provide the width.

Naming conventions for selector states:

| State	       | Suffix          | Example                     |
|--------------|-----------------|-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |


#### 2.2.2 Layout files

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the `SignInActivity`, the name of the layout file should be `activity_sign_in.xml`.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Activity Content         | `UserProfileActivity`  | `content_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

Note that Activity refers to the layout for the activity which will include the  appbar, any view that overlays the main content and the content container.

A slightly different case is when we are creating a layout that is going to be inflated by an `Adapter`, e.g to populate a `ListView`. In this case, the name of the layout should start with `item_`.

Note that there are cases where these rules will not be possible to apply. For example, when creating layout files that are intended to be part of other layouts. In this case you should use the prefix `partial_`.

#### 2.2.3 Menu files

Similar to layout files, menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the `UserActivity`, then the name of the file should be `activity_user.xml`

A good practice is to not include the word `menu` as part of the name because these files are already located in the `menu` directory.

#### 2.2.4 Values files

Resource files in the values folder should be __plural__, e.g. `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`

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

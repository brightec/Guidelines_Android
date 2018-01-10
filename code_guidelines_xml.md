
# XML Style Rules

## Table of Contents

- [1 Use self closing tags](#1-use-self-closing-tags)
- [2 Resources naming](#2-resources-naming)
  + [2.1 ID naming](#21-id-naming)
  + [2.2 Strings](#22-strings)
  + [2.3 Styles and Themes](#23-styles-and-themes)
- [3 Attributes ordering](#3-attributes-ordering)
- [License](#license)

## 1 Use self closing tags

When an XML element doesn't have any contents, you __must__ use self closing tags.

This is good:

```xml
<TextView
	android:id="@+id/text_view_profile"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content" />
```

This is __bad__ :

```xml
<!-- Don\'t do this! -->
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```


## 2 Resources naming

Resource IDs and names are written in __lowercase_underscore__.

### 2.1 ID naming

IDs should be prefixed with the name of the element in lowercase underscore, not abbreviated. For example:

| Element            | Prefix            |
| -----------------  | ----------------- |
| `TextView`           | `text_`             |
| `ImageView`          | `image_`            |
| `Button`             | `button_`           |
| `Menu`               | `menu_`             |
| `Relative`               | `relative_`             |
| `Linear`               | `linear_`             |

Some exceptions may apply, for example:

| Element            | Prefix            |
| -----------------  | ----------------- |
| `EditText`          | `edit_`            |
| `FloatingActionButton`          | `fab_`            |
| `RadioButton`             | `radio_`           |

Image view example:

```xml
<ImageView
    android:id="@+id/image_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

Menu example:

```xml
<menu>
	<item
        android:id="@+id/menu_done"
        android:title="Done" />
</menu>
```

### 2.2 Strings

String names should follow the rules below:


| Prefix             | Description                           |
| -----------------  | --------------------------------------|
| `error_`             | An error message                      |
| `title_`             | A title, i.e. a dialog title or activity title          |
| `action_`            | An action such as "Save" or "Create"  |
| `label_`            | A label for input field  |
| `hint_`            | A hint for an edit text  |

If these rules do not cover your case use a sensible category prefix.


### 2.3 Styles and Themes

Style and theme names are written in __UpperCamelCase__.

## 3 Attributes ordering

As a general rule you should try to group similar attributes together. A good way of ordering the most common attributes is:

1. View Id
2. Style
3. Layout width and layout height
4. Other layout attributes, sorted alphabetically
5. Remaining attributes, sorted alphabetically

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

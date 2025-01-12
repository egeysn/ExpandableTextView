# ExpandableTextView [![](https://jitpack.io/v/giangpham96/ExpandableTextView.svg)](https://jitpack.io/#giangpham96/ExpandableTextView)

Light-weighted, convenient implementation of expandable text view that supports expanding & collapsing animations for
Android projects.

## Why ExpandableTextView?

When the text is too long, a designer reasonably asks if it is possible to truncate the text by having a certain line
count limitation. In addition, an expanding call-to-action (ie. "Read more") should be shown at the end of the text.
When user taps the text, it expands to show the full content. ExpandableTextView helps creating such behaviour easily.

## Demonstration

| Normal               | RTL                   | With drawable         |
| :------------------: | :-------------------: | :-------------------: |
| <video src="https://user-images.githubusercontent.com/23420470/155230035-81fe3b4b-47a9-4e1a-9215-9739a9c343c9.mp4" height=500> | <video src="https://user-images.githubusercontent.com/23420470/155230365-1b1d0acf-3a0a-4082-b966-ba08becbbbab.mp4" height=500> | <video src="https://user-images.githubusercontent.com/23420470/155230017-87b7be5f-0e32-4d6f-a496-b9b5bb559b3a.mp4" height=500> |

| maxLines when expand  | Width changes at runtime         |
| :-------------------: | :------------------------------: |
| <video src="https://user-images.githubusercontent.com/23420470/155230032-991aa221-5828-478b-bda1-05cd1d4ac55b.mp4" height=500> | <video src="https://user-images.githubusercontent.com/23420470/155230372-08afae10-f07d-48fc-b4ce-cd7cbb179f9e.mp4" height=500> |

## Install
**Step 1.** Add the JitPack repository to your build file
- AGP older than 7.1.0
```groovy
// build.gradle (root level)
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

- AGP 7.1.0 and newer
```groovy
// settings.gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

**Step 2.** Add the dependency
```groovy
// build.gradle (module level)
dependencies {
    implementation 'com.github.giangpham96:ExpandableTextView:1.0.2'
}
```

## Usage

### Example XML

```xml
    <io.github.giangpham96.expandabletextview.ExpandableTextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/purple_100"
        android:padding="16dp"
        android:maxLines="10"
        app:expandAction="More"
        app:limitedMaxLines="2"
        app:expandActionColor="@color/blue_500"
        app:originalText="@string/long_text" />
```

### Attributes

| Attributes            | Type                 | Description                 | Default value                    |
| :-------------------: | :-------------------------: | :-------------------------: | :------------------------------: |
| app:limitedMaxLines | Int | The maximum line counts when the text is collapsed | 3 |
| app:expandAction | String | The action at the end of truncated text such as "View more" | "" (Nothing will be shown at the end of truncated text)|
| app:expandActionColor | Color | The color of expand action | #ffaa66cc |
| app:originalText | String | The text to be displayed on this text view | "" |

### Public functions

- `limitedMaxLines` public getter & setter for the maximum line counts when the text is collapsed.
- `expandAction` public getter & setter for the action at the end of truncated text such as "View more".
- `expandActionColor` public getter & setter for the color of expand action.
- `originalText` public getter & setter for the text to be displayed on this text view.
- `collapsed` public getter to determine if the text is being collapsed
- `expanded` public getter to determine if the text is being expanded
- `toggle` function that makes the text changes its state from collapsed to expanded & vice versa. It also adds
animation transition during the state change.

### Notes

- **DO NOT** directly use `android:text` or `setText` in this view. Use `app:originalText` or `originalText` instead.
Attempting to use `android:text` or `setText` will lead to unexpected behaviour.
- At any time, `limitedMaxLines` **MUST** always be less than or equal to `maxLines`. Otherwise, an exception will be
thrown.
- This view only supports `TextUtils.TruncateAt.END`.

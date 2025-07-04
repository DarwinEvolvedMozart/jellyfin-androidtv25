# Jellyfin Android TV - Theme and Navigation Improvements

This document outlines all the changes made to add the Amber theme and improve navigation with icons.

## 🎨 Amber Theme Implementation

### New Theme Files Created

#### `app/src/main/res/values/theme_amber.xml`
- **Purpose**: Defines the Amber theme with warm orange/amber colour palette
- **Key Colours**:
  - Primary: `#E5A00D` (warm amber)
  - Secondary: `#FAA61A` (lighter amber)
  - Dark: `#2D2D2D` (dark grey)
  - Darker: `#1F1F1F` (darker grey)
- **Features**: Overrides all theme attributes to use amber colour scheme

### Updated Files

#### `app/src/main/java/org/jellyfin/androidtv/preference/constant/AppTheme.kt`
```kotlin
// Added new theme enum
AMBER(R.string.pref_theme_amber)
```

#### `app/src/main/java/org/jellyfin/androidtv/util/ActivityThemeExtensions.kt`
```kotlin
// Added theme mapping
AppTheme.AMBER -> R.style.Theme_Jellyfin_Amber
```

#### String Resources Added
- **English**: `pref_theme_amber` = "Amber"
- **Spanish**: `pref_theme_amber` = "Ámbar"
- **French**: `pref_theme_amber` = "Ambre"
- **German**: `pref_theme_amber` = "Bernstein"

## 🔧 Theme Fixes (Hardcoded Colour Removal)

### Fixed Files

#### `app/src/main/res/layout/view_lb_title.xml`
- **Change**: Replaced hardcoded `android:textColor="#E5E5E5"` with `android:textColor="?android:attr/textColorPrimary"`

#### `app/src/main/res/drawable/button_default_text.xml`
- **Change**: Replaced hardcoded highlight text colour with `?android:attr/colorAccent`

#### `app/src/main/res/drawable/button_icon_tint.xml`
- **Change**: Replaced hardcoded highlight text colour with `?android:attr/colorAccent`

#### `app/src/main/res/drawable/button_icon_tint_animated.xml`
- **Change**: Replaced hardcoded highlight text colour with `?android:attr/colorAccent`

#### `app/src/main/res/color/nav_text_color.xml`
- **Change**: Replaced hardcoded focused colour with `?android:attr/colorAccent`

#### `app/src/main/res/layout/glassmorphic_toolbar.xml`
- **Change**: Replaced hardcoded search icon tint with `?android:attr/colorAccent`

#### `app/src/main/res/drawable/toolbar_icon_background.xml`
- **Change**: Replaced hardcoded focused/pressed colours with `?attr/buttonDefaultHighlightBackground`

#### `app/src/main/res/drawable/nav_pill_selector.xml`
- **Change**: Replaced hardcoded focused colour with `?attr/buttonDefaultHighlightBackground`

#### `app/src/main/res/drawable/nav_pill_animated_background.xml`
- **Change**: Replaced hardcoded focused colour with `?attr/buttonDefaultHighlightBackground`

#### `app/src/main/res/drawable/toolbar_icon_background.xml`
- **Change**: Added size constraints (32dp) to prevent oversized circles
- **Change**: Replaced hardcoded focused/pressed colours with `?attr/buttonDefaultHighlightBackground`

#### `app/src/main/res/drawable/user_avatar_container.xml`
- **Change**: Replaced hardcoded focused/pressed colours with `?attr/buttonDefaultHighlightBackground`

## 🧭 Navigation Improvements

### New Files Created

#### `app/src/main/res/layout/view_nav_pill_with_icon.xml`
- **Purpose**: Layout for navigation pills with icons and text
- **Features**:
  - Horizontal layout with icon and text
  - Theme-aware icon tinting
  - Proper spacing and sizing
  - Focus and click handling

### Updated Files

#### `app/src/main/java/org/jellyfin/androidtv/ui/home/HomeFragmentNetflixStyle.kt`

##### New Functions Added:
```kotlin
private fun getIconForCollectionType(collectionType: CollectionType?): Int? {
    return when (collectionType) {
        CollectionType.MOVIES -> R.drawable.ic_movie
        CollectionType.TVSHOWS -> R.drawable.ic_tv
        CollectionType.MUSIC -> R.drawable.ic_music_album
        CollectionType.PHOTOS -> R.drawable.ic_photo
        CollectionType.PLAYLISTS -> R.drawable.ic_mix
        CollectionType.LIVETV -> R.drawable.ic_tv_guide
        CollectionType.BOXSETS -> R.drawable.ic_movie
        else -> null
    }
}
```

##### Modified Functions:
- **`createNavTab()`**: Now uses `view_nav_pill_with_icon.xml` layout with icons
- **`createJellyfinTab()`**: Now uses `view_nav_pill_with_icon.xml` layout with Jellyfin icon
- **`createStaticTab()`**: Now uses `view_nav_pill_with_icon.xml` layout with appropriate icons
- **`getDisplayNameForCollectionType()`**: Modified to prioritize actual library names over generic types

##### Icon Mapping:
- **Movies** → `ic_movie`
- **TV Shows** → `ic_tv`
- **Music** → `ic_music_album`
- **Photos** → `ic_photo`
- **Playlists** → `ic_mix`
- **Live TV** → `ic_tv_guide`
- **Collections** → `ic_movie`
- **Jellyfin** → `ic_jellyfin`

## 🎯 What These Changes Achieve

### Amber Theme Benefits:
1. **Warm, inviting colour scheme** inspired by classic media platforms
2. **Consistent theming** across all UI elements
3. **Proper focus states** with amber highlights
4. **No copyright issues** - uses generic "Amber" name

### Navigation Benefits:
1. **Visual library identification** with relevant icons
2. **Actual library names** instead of generic type names
3. **Better user experience** with clear visual hierarchy
4. **Theme-aware icons** that change colour with theme

### Technical Benefits:
1. **Removed hardcoded colours** - now fully themeable
2. **Consistent theming system** - all elements use theme attributes
3. **Maintainable code** - easy to add new themes
4. **Proper Android patterns** - follows Material Design principles

## 🚀 How to Apply These Changes

### For New Forks:
1. Copy all the modified files to your project
2. Ensure all imports are correct
3. Build and test the changes
4. Customize colours or add new themes as needed

### For Existing Projects:
1. Back up your current theme files
2. Apply the changes incrementally
3. Test each change to ensure compatibility
4. Adjust colours to match your brand

## 🎨 Adding New Themes

To add a new theme:
1. Create `theme_[name].xml` in `app/src/main/res/values/`
2. Add theme string to all language files
3. Add enum to `AppTheme.kt`
4. Add mapping to `ActivityThemeExtensions.kt`
5. Define your colour palette

Example:
```xml
<!-- theme_ocean.xml -->
<color name="theme_ocean_primary">#0066CC</color>
<color name="theme_ocean_secondary">#0099FF</color>
<!-- ... more colours ... -->
```

## 📝 Notes

- All changes maintain backward compatibility
- Theme changes require app restart to take effect
- Icons are 16dp for optimal visibility
- Navigation pills use existing focus and animation systems
- All hardcoded colours have been replaced with theme attributes

## 🤝 Contributing

When contributing themes or navigation improvements:
1. Follow the existing naming conventions
2. Test on both light and dark backgrounds
3. Ensure accessibility compliance
4. Add appropriate string resources for all languages
5. Update this changelog with your changes

---

**Created**: July 2025  
**Author**: AI Assistant  
**Project**: Jellyfin Android TV Fork  
**Version**: 1.0 
## ThemePicker: All I Know About It

So, ThemePicker is a pretty interesting app made by AOSP project for Android 10, which overrides the WallpaperPicker2 app to mix it up with some additions. The idea is providing some cool customization for your device and things like that. It suppurts: Accents, Fonts, Icons, Adaptive Icon Shape and a custom Wallpaper. 
It's a simple tool and that's a good thing and a bad thing. Good thing because it provides a good looking UI and the possibility of providing some tweaking without any weirdstratum or CM's dead TE. The bad thing is that's done in a pretty simplistic way that they don't even check possible flaws (or fatal exceptions) on their method.

But to trashtalk about it, let's see how it works:

 - The override.xml file
 - The overlays for every theme
 - A theme stub

### The override.xml file
This is a file located on res/values that holds some important values that you have to replace to get it working and tweaked on your own. The most basic ones are the following:


    <string  name="themes_stub_package"  translatable="false"/>

This one specifies your theme stub (more on that later), else the theme part of the picker won't be available.

    <array name="icon_shape_preview_packages">
    
    <item>com.google.android.gm</item>
    
    <item>com.google.android.googlequicksearchbox</item>
    
    <item>com.google.android.apps.photos</item>
    
    <item>com.google.android.apps.docs</item>
    
    <item>com.google.android.youtube</item>
    
    <item>com.android.vending</item>
    
    </array>
This array specifies which packages will be used to generate a preview for the custom icon shapes. It's set to some gapps by default but you can switch them to normal AOSP apps or some any other package that has an adaptive icon.

Some other values are the following 

    <string name="grid_control_metadata_name" translatable="false">com.android.launcher3.grid.control</string>
    
    <string name="launcher_overlayable_package" translatable="false">com.android.launcher3</string>
These are for launcher overlays and the grid one of to set a custom grid, needs some extra work on Launcher3 to enable that feature too.

    <string  name="clocks_provider_authority"  translatable="false">com.android.keyguard.clock</string>
  It's the authority of a provider in System UI that will provide preview info for available clockfaces.

### The overlays for every theme
This is basically all the overlays required for the theme. 
It requires:

 - *An accent overlay*
 - *A font overlay*
 - *4 overlays for icon shape on Launcher3, System, SystemUI and Settings*

You can find an example of all those overlays on **packages/overlays** on frameworks/base repo on AOSP git.

### The Theme Stub
This is the most essential thing for themepicker because the theme stub is a package that holds all the theme info, like packages and strings.
You have to specify some values on those strings, else the app will crash (haha).

Let's make an example about a theme i'll codename *roblox* on the strings and the theme name will be *OOF*. I have to set the strings on the following way:

    <string name="theme_name_roblox">OOF</string>
    <string name="theme_overlay_color_roblox">com.android.theme.color.red</string>
    <string name="theme_overlay_font_roblox">com.android.theme.font.rbx</string>
    <string name="theme_overlay_icon_android_roblox">com.android.theme.icon_pack.square.android</string>
    <string name="theme_overlay_icon_launcher_roblox">com.android.theme.icon_pack.square.launcher</string>
    <string name="theme_overlay_icon_settings_roblox">com.android.theme.icon_pack.square.settings</string>
    <string name="theme_overlay_icon_sysui_roblox">com.android.theme.icon_pack.square.systemui</string>
    <string name="theme_overlay_icon_themepicker_roblox">com.android.theme.icon_pack.square.themepicker</string>
    <string name="theme_overlay_shape_roblox">com.android.theme.icon.square</string>
    <string name="theme_title_roblox">@string/theme_name_roblox</string>
    <string name="theme_wallpaper_roblox">@drawable/minecraftsteve</string>
    <string name="theme_wallpaper_thumbnail_roblox">@drawable/smallsteve</string>
    <string name="theme_wallpaper_title_roblox">Minecraft Steve</string>
    <string name="theme_wallpaper_attribution_roblox">Mojang/DeviantArt - 2017 </string>
So, as you can see, all the strings has a prefix before the theme ID (roblox in this case), and all those overlays are requires to tell the [DefaultThemeProvider](https://android.googlesource.com/platform/packages/apps/ThemePicker/+/refs/tags/android-10.0.0_r5/src/com/android/customization/model/theme/DefaultThemeProvider.java)  what are all those overlays that are needed for our theme to enable/disable when you play with them.
Also, for previewing sake, you have to add another drawable of your wallpaper but smaller, and speacify the name on the theme_wallpaper_thumbnail_themeid string, so it can be shown on the preview on ThemePicker. In the case of theme_wallpaper_themeid you can use a drawable or a live wallpaper special activity, and some options. Don't know a lot about the latter one, so that's it.

Remember to do the overlays for everything, do the stub theme app and the required overlays, and let's have fun theming!

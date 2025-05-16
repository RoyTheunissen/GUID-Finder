[![Roy Theunissen](Documentation~/Github%20Header.jpg)](http://roytheunissen.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE.md)
![GitHub Follow](https://img.shields.io/github/followers/RoyTheunissen?label=RoyTheunissen&style=social)
<a href="https://roytheunissen.com" target="blank"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/globe_dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/globe_light.png">
    <img alt="globe" src="globe_dark.png" width="20" height="20" />
</picture></a>
<a href="https://bsky.app/profile/roytheunissen.com" target="blank"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/bluesky_dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/bluesky_light.png">
    <img alt="bluesky" src="bluesky_dark.png" width="20" height="20" />
</picture></a>
<a href="https://www.youtube.com/c/r_m_theunissen" target="blank"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/youtube_dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/youtube_light.png">
    <img alt="youtube" src="youtube_dark.png" width="20" height="20" />
</picture></a> 
<a href="https://www.tiktok.com/@roy_theunissen" target="blank"><picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/tiktok_dark.png">
    <source media="(prefers-color-scheme: light)" srcset="https://github.com/RoyTheunissen/RoyTheunissen/raw/master/tiktok_light.png">
    <img alt="tiktok" src="tiktok_dark.png" width="20" height="20" />
</picture></a>

_Sometimes you really need find all the places where an asset is being referenced, and Unity's own search solutions are too unreliable for this._

## About the Project

Let's say you removed a script from your game, and you want to ensure that it's also removed from scenes/prefabs. You might be inclined to use `Right Click -> Find References in Project`, which opens a Search window which will be thinking and processing for a very, very long time and then will then output _some_ results.

In practice I've found that it won't find usages in scenes unless those scenes happen to be open, and its track record is spotty with prefabs, too.

In other words: if you're doing an important refactor and _must_ know all the places an asset's referenced, Unity Search will not suffice.

But every asset has a GUID, so you could simply search the contents of assets for that GUID. In fact, you could do it in [Notepad++](https://notepad-plus-plus.org/) pretty easily:
- Go to the asset in question in Unity
- `Right Click -> Show in Explorer`
- Go to the asset in question's `.meta` file
- Copy the GUID
- Press `CTRL+Shift+F` or go to to `Search > Find in Files`
- Search for the specified GUID in files with pattern `*.unity *.prefab` in your project's `Assets` folder.
- This will think only for a few seconds and then output a list of **every** reference to that asset.
- You can then search for that asset by name in Unity

This is a very robust approach, but of course you have to leave the editor for this, and there's a lot of manual labour involved. GUID Finder is essentially just a nice GUI for the above mentioned workflow:

![image](https://github.com/user-attachments/assets/2c88b227-b5b3-41d4-9ce4-41343782d30d)

When doing important refactors, this tool is simple, fast, and thorough enough to get the job done.

It is guaranteed to find *every* possible reference.

## Getting Started

- Open the GUID Finder window via `Window > Search > GUID Finder`
  ![image](https://github.com/user-attachments/assets/2b3ed868-6076-4bc2-a296-47bf4a10d6b9)

- Drag in an asset in the `Asset to find` field.
- The GUID for the asset in question will appear.
- Specify the types of files to search in.
- Specify the folder to search in.
- Press Search.
- Observe how all the assets that reference the specified asset are listed, and you can click on them to open them.
![image](https://github.com/user-attachments/assets/d9c78a48-d2a5-49dc-be3b-9c0082d2bf79)
_Pictured: A script that is referenced inside a specific scene will be found even if that scene is not open, something that Unity's own Search solution does not seem to do._

## Caveats
- If you have a reference to an asset in a script, then remove that field from the script, the assets that had the reference will continue to have the reference until you modify and save the asset. You can see this happening in your version control software. It makes sense if you think about it: if you remove a field from a script you don't see Unity start a lengthy process of purging all the references of that field from its prefabs and scenes, polluting your working copy with a lot of changes. **This also means that if you have any such leftover references lying around, GUID Finder will find those as well**. GUID Finder will find **everything**, and it's up to you to filter out such false positives.
- If you have a reference somewhere deep in a complicated prefab or scene, GUID Finder is not able to tell you _where_ inside that complicated prefab or scene. It's then up to you to go looking for the exact reference.

## Feature Wishlist
- Some (optional?) way to check if a reference is from a script, and then to check if that script does indeed still contain the specified field. If not, we could filter out search results for references that are not in use.
- Some (optional?) way to locate the exact location of a reference inside of a prefab or script. This might be tricky, we may have to parse the asset a bit. There's also the question of how to present this in the GUI.

## Compatibility

This system was developed for Unity 2022, it's recommended that you use it in Unity 2022 or upwards. It's been tested in Unity 6 as well and seems to work the same there.

If you use an older version of Unity and are running into trouble, feel free to reach out and I'll see what I can do.

The GUI was developed with UI Toolkit and the functionality is pretty basic, so this tool will likely work across a wide range of Unity versions.

## Installation

### Package Manager

Go to `Edit > Project Settings > Package Manager`. Under 'Scoped Registries' make sure there is an OpenUPM entry.

If you don't have one: click the `+` button and enter the following values:

- Name: `OpenUPM` <br />
- URL: `https://package.openupm.com` <br />

Then under 'Scope(s)' press the `+` button and add `com.roytheunissen`.

It should look something like this: <br />
![image](https://user-images.githubusercontent.com/3997055/185363839-37b3bb3d-f70c-4dbd-b30d-cc8a93b592bb.png)

<br />
All of my packages will now be available to you in the Package Manager in the 'My Registries' section and can be installed from there.
<br />


### Git Submodule

You can check out this repository as a submodule into your project's Assets folder. This is recommended if you intend to contribute to the repository yourself.

### OpenUPM
The package is available on the [openupm registry](https://openupm.com). It's recommended to install it via [openupm-cli](https://github.com/openupm/openupm-cli).

```
openupm add com.roytheunissen.guid-finder
```

### Manifest
You can also install via git URL by adding this entry in your **manifest.json** (make sure to end with a comma if you're adding this at the top)

```
"com.roytheunissen.guid-finder": "https://github.com/RoyTheunissen/GUID-Finder.git"
```

### Unity Package Manager
From Window->Package Manager, click on the + sign and Add from git: 
```
https://github.com/RoyTheunissen/GUID-Finder.git
```


## Contact
[Roy Theunissen](https://roytheunissen.com)

[roy.theunissen@live.nl](mailto:roy.theunissen@live.nl)

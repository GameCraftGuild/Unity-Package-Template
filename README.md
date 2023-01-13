# Unity UPM Package Template

#### Adaption/Fork note
This template is an adaptation of [Stan's Assets](https://github.com/StansAssets)' Unity Package Template. It has been heavily rearranged to suit our needs at GameCraft Guild. Stan and the other contributors did an amazing job outlining and describing how to get started making a custom Unity Package! So the original readme information he wrote has been mostly kept. with edits and additions to describe this new adaption of his package template.

## Introduction
The purpose of this template is to give you a head start when creating a new package for Unity. You'll find the repository structure description below as well as why it was built this way.
I assume you already have some basic understanding of what the UPM package is and why you would like to build one. If not, please check out Unity's [Creating custom packages](https://docs.unity3d.com/Manual/CustomPackages.html) page.

## How to use
1. Create a new repository and use this repository as a template
2. Run init script `bash init <new-package-name> <new-package-namespace>`
    * Example1: `bash init com.mycompany.awesome-package MyCompany.AwesomePackage`
    * Example2: `bash init com.stansassets.foundation Stansassets.Foundation`
3. Open the root directory as a Unity project and ensure the embedded package is compiling and detected
4. Open `package.json` and update package metadata. You can do this by selecting the `package.json` in the Unity Editor or within a text editor. I would recommend using a text editor since there are additional properties not consumed by Unity in the `package.json`
5. Close the Unity project. Then go into the `.gitignore` file and remove the temporarily ignored Unity files.
   ```gitignore
   ...
   # ===== DELETE when ready to work on Unity project and embedded package ===== #
   UserSettings/
   ProjectSettings/
   **/*.meta
   # ===== DELETE when ready to work on Unity project and embedded package ===== #
   ``` 
6. Delete the init script and make your initial git commit. Happy package making!

## Package manifest
Unity uses the package manifest file `package.json` to manage information about a specific version of a specific package. The package manifest is always at the root of the package and contains crucial information about the package, such as its registered name and version number. ([Full Package manifest Unity Guide](https://docs.unity3d.com/Manual/upm-manifestPkg.html))

### Required attributes
* **name** - The officially registered package name.
* **version** - The package version number (MAJOR.MINOR.PATCH)
* **displayName** - A user-friendly name to appear in the Unity Editor
* **description** - A brief description of the package
* **unity** - Indicates the lowest Unity version the package is compatible with

### Optional attributes
* **unityRelease** - Part of a Unity version indicating the specific release of Unity that the package is compatible with
* **dependencies** - A map of package dependencies
* **keywords** - An array of keywords used by the Package Manager search APIs
* **license** - Specify a license for your package so that people know how they are permitted to use it, and any restrictions you’re placing on it. Or set the string to "See LICENSE.md file" if your package includes a `License.md` file
* **author** - Author of the package
* and more - see [Full Package manifest Unity Guide](https://docs.unity3d.com/Manual/upm-manifestPkg.html)

### npmjs attributes
This is only relevant if you are planning to distribute your package with npmjs. Otherwise, remove listed keywords from the `package.json` template.
I will list attributes that will affect how your package is displayed on the npmjs package page. As an example, you can check out the [Foundation package page](https://www.npmjs.com/package/com.stansassets.foundation). But I would also recommend reading the full [npm-package.json guide](https://docs.npmjs.com/files/package.json.html).

* **homepage** - The URL to the project homepage.
* **bugs** - The URL to your project issue tracker and/or the email address to which issues should be reported.
* **repository** - Specify the place where your code lives.

### Package manifest example
This is how `package.json` looks like in our template repository:
```json
{
   "name": "com.gamecraftguild.package-template",
   "version": "0.0.1-preview",
   "displayName": "GameCraftGuild - Package Template",
   "description": "a description of package",
   "unity": "2022.2",
   "documentationUrl": "",
   "changelogUrl": "",
   "license": "See LICENSE.md file",
   "licensesUrl": "",
   "keywords": [
      "gamecraft",
      "gamecraftguild"
   ],
   "author": {
      "name": "GameCraft Guild",
      "email": "gamecraftguild@gmail.com",
      "url": "https://github.com/GameCraftGuild"
   },
   "homepage": "https://github.com/GameCraftGuild",
   "bugs": {
      "url": "https://github.com/GameCraftGuild/Unity-Package-Template/issues",
      "email": "gamecraftguild@gmail.com"
   },
   "repository": {
      "type": "git",
      "url": "ssh://git@github.com:GameCraftGuild/Unity-Package-Template.git"
   }
}
```

## Repository structure
* `init` - CLI init script
* `.github`  - GitHub Settings & Actions 
* `.gitignore` - Git ignore file designed to this specific repository structure
* `.gitattributes` - Git attributes file designed to this specific repository structure
* `README.md` - text file that introduces and explains a project
* `Assets/` - a default assets folder with an empty example scene which helps Unity detect this repository as a Unity Project
* `Packages/com.gamecraftguild.package-template` - your embedded Unity package location

This structure was chosen for the following reasons:
1. Simplicity. Your root directory is a Unity Project making it easy to stand up and get started working on your package
2. You have the Unity Project that your team may use to work on a package. There are a few benefits of having the project already set:
   * Team members (especially the ones who haven't worked with the project before) won't have to setup their own project
   * The project is already linked to the package since it is setup as an [embedded package](https://docs.unity3d.com/Manual/upm-embed.html)
3. Structure emphasizes **one** unity package per repository to help focus changes to be always around the singular package and allow the use of git version tags for [openUPM](https://openupm.com/docs/adding-upm-package.html#upm-package-criteria)'s package detection

#### Note:
* It is recommended to use [openUPM](https://openupm.com/docs/adding-upm-package.html#upm-package-criteria) as the means to distribute your package
* If you are planning to distribute your package via [Git URL](https://docs.unity3d.com/Manual/upm-git.html), this structure would not work for you. In such a case, your package would need to be in the repository's root directory

## Package Info 
You are not obligated to provide any description files with your package, but to be a good package developer, it's nice to at least ship the following files for your project.
You will also want all the links to work when your package is viewed in Unity's [Package Manager window](https://docs.unity3d.com/Manual/upm-ui.html) 
![](https://user-images.githubusercontent.com/12031497/81487789-bab70780-9269-11ea-87b9-5a453c332d21.png)

### LICENSE.md
You should specify a license for your package so that people know how they are permitted to use it, and any restrictions you’re placing on it.
The template repository `LICENSE.md` file already comes the MIT license. 

### CHANGELOG.md
A changelog is a file that contains a curated, chronologically ordered list of notable changes for each version of a project. To make it easier for users and contributors to see precisely what notable changes have been made between each release (or version) of the project.
The template repository `CHANGELOG.md` has some sample records based on the [keep a changelog](https://keepachangelog.com/) standard.

### Documentation~/YourPackageName.md
The file contains the offline copy of the package documentation. I recommend placing the package description and links to the web documentation into that file.

### README.md
I do not think I have to explain why this is important :) Besides this file will be used to make home page content for your package if you distribute it on [npm](https://www.npmjs.com/) or [openUPM](https://openupm.com/). The template repository `README.md` already contains some content that describes how to install your package via [openUPM](https://openupm.com/), [npm](https://www.npmjs.com/), or ~~[Git URL](https://docs.unity3d.com/Manual/upm-git.html)~~ 

There are also some cool badges you would probably like to use. The [Foundation package](https://github.com/StansAssets/com.stansassets.foundation) is a good example of how it can look like:
![](https://user-images.githubusercontent.com/12031497/81487844-4892f280-926a-11ea-9418-df89e427652b.png)

## Package layout
The repository package layout follows the [official Unity packages convention](https://docs.unity3d.com/Manual/cus-layout.html).

```
<package root>
  ├── package.json
  ├── README.md
  ├── CHANGELOG.md
  ├── LICENSE.md
  ├── Third Party Notices.md
  ├── Editor
  │   ├── [company-name].[package-name].Editor.asmdef
  │   └── EditorExample.cs
  ├── Runtime
  │   ├── [company-name].[package-name].asmdef
  │   └── RuntimeExample.cs
  ├── Tests
  │   ├── Editor
  │   │   ├── [company-name].[package-name].Editor.Tests.asmdef
  │   │   └── EditorExampleTest.cs
  │   └── Runtime
  │        ├── [company-name].[package-name].Tests.asmdef
  │        └── RuntimeExampleTest.cs
  ├── Samples~
  │        ├── SampleFolder1
  │        ├── SampleFolder2
  │        └── ...
  └── Documentation~
       └── [package-name].md
```
The only comment I would like to add is to remove unused folders and `*.asmdef` files. For example, you do not have any tests atm or your package does not have an Editor API. Those folders and files should be removed.
The same goes for if you are not keeping your changelog up to date; Just remove the `CHANGELOG.md`. 

Keeping unused & unmaintained pieces in your published package will be misleading for its users, so please avoid doing so.

## CI / CD
It's important to have, it will save your development time. Again this is something I don't have to explain, let's just go straight to what we already have set in this package template repository.

### Currently removed all actions. new actions TBD


### Next Steps
To make me completely happy about this template there should be few more set up steps. But I think we will get to it with the next article.

* Automatic `CHANGELOG.md` generation. We are already feeling up the release notes, I don't see the reason why we have to do it again the `CHANGELOG.md` when we can simply have an automated commit before publishing to npm action.
* Editor and Playmode tests. It's not a real CI until we have no tests running. 
* Docfx + GitHub Pages documentation static website generation.

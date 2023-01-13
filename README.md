# Unity UPM Package Template

#### Adaption/fork note
This template is an adaptation of [Stan's Assets](https://github.com/StansAssets)' Unity Package Template. It has been heavily rearranged to suit our needs at GameCraft Guild. Stan and the other contributors did an amazing job outlining and describing how to get started making a custom Unity Package! So the original readme information he wrote has been mostly kept. with edits and additions to describe this new adaption of his package template.

## Introduction
The purpose of this template is to give you a head start when creating a new package for Unity. You'll find the repository structure description below as well as why it was built this way.
I assume you already have some basic understanding of what the UPM package is and why you would like to build one. If not, please check out Unity's [Creating custom packages](https://docs.unity3d.com/Manual/CustomPackages.html) page.

## How to use
* Create a new repository and use this sample repository as a template
* Run init script `sh <new-package-name> <new-package-namespace>` 
    * Example1: `sh init com.my-company.unity.awesome-package MyCompany.AwesomePlugin`
    * Example2: `sh init com.stansassets.foundation Stansassets.Foundation`
* Open `package.json` and update package metadata. You can do this by selecting the `package.json` in the Unity Editor or within a text editor. I would recommend using a text editor since there are additional properties not consumed by Unity in the `package.json`

## Package manifest
Unity uses the package manifest file `package.json` to manage information about a specific version of a specific package. The package manifest is always at the root of the package and contains crucial information about the package, such as its registered name and version number. [Full Package manifest Unity Guide](https://docs.unity3d.com/Manual/upm-manifestPkg.html).

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
* **author** - Author of the package

### npmjs attributes
This is only relevant if you are planning to distribute your package with npmjs. Otherwise, remove listed keywords from the `package.json` template.
I will list attributes that will affect how your package is displayed on the npmjs package page. As an example, you can check out the [Foundation package page](https://www.npmjs.com/package/com.stansassets.foundation). But I would also recommend reading the full [npm-package.json guide](https://docs.npmjs.com/files/package.json.html).

* **homepage** - The URL to the project homepage.
* **bugs** - The URL to your project issue tracker and/or the email address to which issues should be reported.
* **license** - Specify a license for your package so that people know how they are permitted to use it, and any restrictions you’re placing on it. 
* **repository** - Specify the place where your code lives.

### Package manifest example
This is how `package.json` looks like in our template repository:
```json
{
  "name": "com.stansassets.package-sample",
  "displayName": "Stans Assets - Package Sample",
  "version": "0.0.1-preview",
  "unity": "2019.3",
  "description": "Package Sample.",
  "dependencies": {
    "com.stansassets.foundation": "1.0.2"
  },
  "keywords": [
    "keyword1",
    "keyword2",
    "keyword3"
  ],
  "license": "MIT",
  "author": {
    "name": "Stan's Assets",
    "email": "stan@stansassets.com",
    "url": "https://stansassets.com/"
  },
  
  "homepage": "https://api.stansassets.com/",
  "bugs": {
    "url": "https://github.com/StansAssets/com.stansassets.foundation/issues",
    "email" : "support@stansassets.com"
  },
  "repository": {
    "type": "git",
    "url": "ssh://git@github.com:StansAssets/com.stansassets.foundation.git"
  },
}
```

## Repository structure
* `init` - CLI init script.
* `.github`  - GitHub Settings & Actions 
* `.gitignore` - Git ignore file designed to this specific repository structure.
* `README.md` - text file that introduces and explains a project. 
* `PackageSampleProject` - Team shared project for package development.
* `com.stansassets.package-sample` - UMP package.

This structure was chosen for the following reasons:
1. Scalability. Since the package isn't located in the repository root, you can host more than one package in the repository.
2. You have the Unity Project that your team may use to work on a package. There are a few benefits of having the project already set:
   * Team members (especially the ones who haven't worked with the project before) won't have to go thought the project set up.
   * Project already linked to the package using a [local](https://docs.unity3d.com/Manual/upm-localpath.html) relative path.
   * You can have Additional scripts, resources, another package. Whatever could help you develop the package but should not be part of the package release.
   * You can have additional settings defined in your project `manifest.json` For example project from this template has stansassets npmjs score registry defined.

```json
"scopedRegistries": [
     {
       "name": "npmjs",
       "url": "https://registry.npmjs.org/",
       "scopes": [
         "com.stansassets"
       ]
     }
   ],
  "dependencies": {
    "com.stansassets.package-sample": "file:../../com.stansassets.package-sample",
```

#### Note:
* If you are planning to distribute your package via [Git URL](https://docs.unity3d.com/Manual/upm-git.html), this structure would not work for you. In this case, you will need to place your package in the repository's root.
* Template `.gitignore` will also ignore project settings. The motivation here, is that you need to ensure that your package will run on different Unity editor versions/configurations and your team members might be jumping between those versions. Adding ProjectSettings into `.gitignore`  will help to avoid conflicts between developers.

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
I do not think I have to explain why this is important :) Besides this file will be used to make home page content for your package if you distribute it on [npm](https://www.npmjs.com/) or [openUPM](https://openupm.com/). The template repository `README.md` already contains some content that describes how to install your package via [npm](https://www.npmjs.com/), [openUPM](https://openupm.com/) or [Git URL](https://docs.unity3d.com/Manual/upm-git.html) 

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

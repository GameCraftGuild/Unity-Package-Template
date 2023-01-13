# Package Sample
<!-- Describe your package -->

[![openupm](https://img.shields.io/npm/v/com.gamecraftguild.package-template?label=openupm&registry_uri=https://package.openupm.com)](https://openupm.com/packages/com.gamecraftguild.package-template/)
[![NPM Package](https://img.shields.io/npm/v/com.gamecraftguild.package-template)](https://www.npmjs.com/package/com.gamecraftguild.package-template)
[![Licence](https://img.shields.io/npm/l/com.gamecraftguild.package-template)](https://github.com/GameCraftGuild/com.gamecraftguild.package-template/blob/master/LICENSE)
[![Issues](https://img.shields.io/github/issues/GameCraftGuild/com.gamecraftguild.package-template)](https://github.com/GameCraftGuild/com.gamecraftguild.package-template/issues)

<!-- Add some useful links here -->

[API Reference](https://myapi) | [Forum](https://myforum) | [Wiki](https://github.com/GameCraftGuild/com.gamecraftguild.package-template/wiki)

### Install from OpenUPM [recommended]
* Install openupm-cli `npm install -g openupm-cli` or `yarn global add openupm-cli`
* Enter your unity project folder `cd <YOUR_UNITY_PROJECT_FOLDER>`
* Install package `openupm add com.gamecraftguild.package-template`

### Install from NPM
* Navigate to the `Packages` directory of your project.
* Adjust the [project manifest file](https://docs.unity3d.com/Manual/upm-manifestPrj.html) `manifest.json` in a text editor.
* Ensure `https://registry.npmjs.org/` is part of `scopedRegistries`.
  * Ensure `com.gamecraftguild` is part of `scopes`.
  * Add `com.gamecraftguild.package-template` to the `dependencies`, stating the latest version.

A minimal example ends up looking like this. Please note that the version `X.Y.Z` stated here is to be replaced with [the latest released version](https://www.npmjs.com/package/com.gamecraftguild.package-template) which is currently [![NPM Package](https://img.shields.io/npm/v/com.gamecraftguild.package-template)](https://www.npmjs.com/package/com.gamecraftguild.package-template).
  ```json
  {
    "scopedRegistries": [
      {
        "name": "npmjs",
        "url": "https://registry.npmjs.org/",
        "scopes": [
          "com.gamecraftguild"
        ]
      }
    ],
    "dependencies": {
      "com.gamecraftguild.package-template": "X.Y.Z",
      ...
    }
  }
  ```
* Switch back to the Unity software and wait for it to finish importing the added package.

### Install from a Git URL [not supported]
This package cannot be installed via Git URL because it's root directory is not the repository's root directory.

For more information about what protocols Unity supports, see Unity's [Git URLs](https://docs.unity3d.com/Manual/upm-git.html) page.

[//]: # (* Open [Unity Package Manager]&#40;https://docs.unity3d.com/Manual/upm-ui.html&#41; window.)

[//]: # (* Click the add **+** button in the status bar.)

[//]: # (* The options for adding packages appear.)

[//]: # (* Select Add package from git URL from the add menu. A text box and an Add button appear.)

[//]: # (* Enter the `https://github.com/StansAssets/com.gamecraftguild.package-template.git` Git URL in the text box and click Add.)

[//]: # (* You may also install a specific package version by using the URL with the specified version.)

[//]: # (  * `https://github.com/StansAssets/com.gamecraftguild.package-template#X.Y.X`)

[//]: # (  * Please note that the version `X.Y.Z` stated here is to be replaced with the version you would like to get.)

[//]: # (  * You can find all the available releases [here]&#40;https://github.com/StansAssets/com.gamecraftguild.package-template/releases&#41;.)

[//]: # (  * The latest available release version is [![Last Release]&#40;https://img.shields.io/github/v/release/stansassets/com.gamecraftguild.package-template&#41;]&#40;https://github.com/StansAssets/com.gamecraftguild.package-template/releases/latest&#41;)

[//]: # ()
[//]: # (For more information about what protocols Unity supports, see Unity's [Git URLs]&#40;https://docs.unity3d.com/Manual/upm-git.html&#41; page.)


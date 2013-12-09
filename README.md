# ImageX InstallKit Patches

The following is a collection of patches that are used on a regular basis during active development. This repository exists as a central holding area for all patch files that are applied to [ImageX InstalKit](http://github.com/imagex/imagex_installkit). These patches are used to directly alter something in InstallKit for site-specific modifications that cannot easily be made in another way. These patches are a short-term fix until more robust development tools and APIs can be created.

## Patches for ImageX InstallKit

#### JQuery Update version

This patch modifies InstallKit contrib make file to download the latest development version of jQuery Update instead of version 2.3. The latest development version includes the ability to set a different jQuery version to be used on the administration theme.

Applies to the 7.x-1.x-dev version of InstallKit.

***Patch File: [imagex_installkit-jquery-update-latest.patch](https://raw.github.com/kevinchampion/imagex_installkit_patches/7.x/imagex_installkit/imagex_installkit-jquery-update-latest.patch)***

#### Remove Permissions

This patch removes the dependencies to the various permissions component modules in installkit so that they're not installed and we don't have to deal with the permissions overriding headache:

- imagex_bean_permissions
- imagex_superuser
- imagex_user_permissions
- imagex_vocabulary_tags_permissions
- imagex_wysiwyg_profiles_permissions

Applies to the 7.x-1.x-dev version of InstallKit.

***Patch File: [imagex_installkit-remove_permissions_modules.patch](https://raw.github.com/kevinchampion/imagex_installkit_patches/7.x/imagex_installkit/imagex_installkit-remove_permissions_modules.patch)***


## How to use these patches

Patches should be applied to the correct make file project definition in the relevant drupal-org.make file, which will allow the project to be patched during the build process using drush make.

Each of the patch links above directly link to the RAW version of the patch file that is to be applied. The `drush make` files that specify patches for projects using the `projects[project-name][patch][]` syntax need to have a URL specified for the patch file. Therefore, copy the RAW URL of the patch file that lives within this repository and specify it within `drush make` project build file. This will allow for increased management of the code that is to be patched in addition to ease of managing revisions to the patches.

All projects that make use of these patches should also not directly link to the forked repositories RAW version of the patch file but instead directly to this repositories RAW version.

For example, if your project is to have the inheritable profiles patch applied to it, the `drupal-org-core.make` file may look something like this:

```
api = 2
core = 7.x

; Download Drupal core.
projects[drupal][type] = "core"
projects[drupal][version] = "7.23"

; Apply the inheritable profiles patch to core.
projects[drupal][patch][] = https://raw.github.com/imagex/imagex_patches/7.x/core/inheritable-profiles/1356276-D7-inheritable-profiles-multi.patch
```

## Contributing

If you believe that we are missing a patch that should exist and or you have a revised patch that should be updated, please fork the repository, update and create a new pull request. Be sure to include the patch file, a description of what the patch does and why it is necessary.

This repository is maintained by the development leads and their teams at [ImageX](http://imagexmedia.com).

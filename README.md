# Divvun Dev Keyboard

This repository exists for the purposes of triggering CI and CD. It is a kbdgen meta-repository, and serves as the basis for the content of the mobile keyboard apps.

If you want your keyboard to be built, update `divvun-dev.kbdgen/targets/android.yaml` or `divvun-dev.kbdgen/targets/ios.yaml`. [This](https://github.com/divvun/divvun-dev-keyboard/commit/c62eeaf12b3619ef7898f958f1371f52eca0ac0c) is the kind of edit you're looking for. 

Edits to the layouts should happen in the keyboard repos in [GiellaLT](https://github.com/giellalt), one repo for each language.


## Creating a new iOS app

Oh it's great fun. You can't just create it - you have to create an identifier first. 

1. Create identifier
2. Add to fastlane
3. Add to build


### 1. Create identifier

1. Go to https://developer.apple.com/account/resources/identifiers/list  (log in with divvun.ios@gmail.com )
2. Click the "+" button next to the word Identifiers
3. Select "App IDs" on the "Register a new identifier" screen. Continue
4. Select type "App". Continue
5. Enter "Divvun Dev Keyboard liv" and "no.uit.giella.keyboards.dev.liv" as Descrition and BundleID (Explicit) respectively.
6. In capabilities, copy the settings from some other keyboard you like. For instance https://developer.apple.com/account/resources/identifiers/bundleId/edit/TUY9Q4GR35
7. Continue
8. Register


### 2. Add to fastlane.

See [fastlane.md](https://github.com/divvun/maintenance2023/blob/main/inventory/fastlane.md) for the fastlane dance setup. Or just try running this and .. you know. Figure it out. 

What we want to do is add a certificate for your new identifer (no.uit.giella.keyboards.dev.liv).

```
$ fastlane match appstore
[✔] 🚀
[21:29:08]: Get started using a Gemfile for fastlane https://docs.fastlane.tools/getting-started/ios/setup/#use-a-gemfile

+-------------------------------------------------------------+
|                  Summary for match 2.221.1                  |
+----------------------------------------+--------------------+
| type                                   | appstore           |
| readonly                               | false              |
| generate_apple_certs                   | true               |
| skip_provisioning_profiles             | false              |
| storage_mode                           | git                |
| git_branch                             | master             |
| shallow_clone                          | false              |
| clone_branch_directly                  | false              |
| skip_google_cloud_account_confirmation | false              |
| s3_skip_encryption                     | false              |
| gitlab_host                            | https://gitlab.com |
| keychain_name                          | login.keychain     |
| force                                  | false              |
| force_for_new_devices                  | false              |
| include_mac_in_profiles                | false              |
| include_all_certificates               | false              |
| force_for_new_certificates             | false              |
| skip_confirmation                      | false              |
| safe_remove_certs                      | false              |
| skip_docs                              | false              |
| platform                               | ios                |
| derive_catalyst_app_identifier         | false              |
| fail_on_name_taken                     | false              |
| skip_certificate_matching              | false              |
| skip_set_partition_list                | false              |
| verbose                                | false              |
+----------------------------------------+--------------------+

[21:29:09]: To not be asked about this value, you can specify it using 'git_url'
[21:29:09]: URL to the git repo containing all the certificates: git@github.com:divvun/fastlane-secrets.git
[21:29:13]: Cloning remote git repo...
[21:29:13]: If cloning the repo takes too long, you can use the `clone_branch_directly` option in match.
[21:29:16]: Checking out branch master...
[21:29:17]: 🔓  Successfully decrypted certificates repo
[21:29:17]: Verifying that the certificate and profile are still valid on the Dev Portal...
-------------------------------------------------------------------------------------
Please provide your Apple Developer Program account credentials
The login information you enter will be stored in your macOS Keychain
You can also pass the password using the `FASTLANE_PASSWORD` environment variable
See more information about it on GitHub: https://github.com/fastlane/fastlane/tree/master/credentials_manager
-------------------------------------------------------------------------------------
Username: divvun.ios@gmail.com
-------------------------------------------------------------------------------------
Please provide your Apple Developer Program account credentials
The login information you enter will be stored in your macOS Keychain
You can also pass the password using the `FASTLANE_PASSWORD` environment variable
See more information about it on GitHub: https://github.com/fastlane/fastlane/tree/master/credentials_manager
-------------------------------------------------------------------------------------
Username: divvun.ios@gmail.com
[21:29:24]: To not be asked about this value, you can specify it using 'app_identifier'
[21:29:24]: The bundle identifier(s) of your app (comma-separated string or array of strings): no.uit.giella.keyboards.dev.liv
...
```

Specify only a single identifier if you are just adding a new language to the existing app. If you have to refresh all certs, then you also need to specify all bundle identifiers.

```
...
[21:29:29]: Installing certificate...

+-------------------------------------------------------------------------------+
|                             Installed Certificate                             |
+-------------------+-----------------------------------------------------------+
| User ID           | 2K5J2584NX                                                |
| Common Name       | Apple Distribution: The University of Tromso (2K5J2584NX) |
| Organisation Unit | 2K5J2584NX                                                |
| Organisation      | The University of Tromso                                  |
| Country           | US                                                        |
| Start Datetime    | 2024-07-22 18:22:50 UTC                                   |
| End Datetime      | 2025-07-22 18:22:49 UTC                                   |
+-------------------+-----------------------------------------------------------+


+--------------------------------------------------------------------------------------+
|                               Summary for sigh 2.221.1                               |
+-------------------------------------+------------------------------------------------+
| app_identifier                      | no.uit.giella.keyboards.dev.liv                |
| force                               | false                                          |
| cert_id                             | 4M5M5795GT                                     |
| provisioning_name                   | match AppStore no.uit.giella.keyboards.dev.liv |
| ignore_profiles_with_different_name | true                                           |
| fail_on_name_taken                  | false                                          |
| include_all_certificates            | false                                          |
| include_mac_in_profiles             | false                                          |
| platform                            | ios                                            |
| adhoc                               | false                                          |
| developer_id                        | false                                          |
| development                         | false                                          |
| skip_install                        | false                                          |
| skip_fetch_profiles                 | false                                          |
| skip_certificate_verification       | false                                          |
| readonly                            | false                                          |
+-------------------------------------+------------------------------------------------+

[21:29:32]: To not be asked about this value, you can specify it using 'username'
[21:29:32]: Your Apple ID Username: divvun.ios@gmail.com
[21:29:36]: Starting login with user 'divvun.ios@gmail.com'
[21:29:37]: Successfully logged in
[21:29:37]: Fetching profiles...
[21:29:37]: Verifying certificates...
[21:29:37]: No existing profiles found, that match the certificates you have installed locally! Creating a new provisioning profile for you
[21:29:38]: Creating new provisioning profile for 'no.uit.giella.keyboards.dev.liv' with name 'match AppStore no.uit.giella.keyboards.dev.liv' for 'ios' platform
[21:29:39]: Downloading provisioning profile...
[21:29:39]: Successfully downloaded provisioning profile...
[21:29:39]: Installing provisioning profile...
/var/folders/hn/tz1vlvm16zs22yr5ytyn7jc80000gn/T/d20240722-73011-3eas65/profiles/appstore/AppStore_no.uit.giella.keyboards.dev.liv.mobileprovision
[21:29:39]: Installing provisioning profile...
[21:29:39]: 🔒  Successfully encrypted certificates repo
[21:29:39]: Pushing changes to remote git repo...
[21:29:47]: Finished uploading files to Git Repo [git@github.com:divvun/fastlane-secrets.git]

+-------------------------------------------------------------------------------------------------------+
|                                    Installed Provisioning Profile                                     |
+---------------------+----------------------------------------+----------------------------------------+
| Parameter           | Environment Variable                   | Value                                  |
+---------------------+----------------------------------------+----------------------------------------+
| App Identifier      |                                        | no.uit.giella.keyboards.dev.liv        |
| Type                |                                        | appstore                               |
| Platform            |                                        | ios                                    |
| Profile UUID        | sigh_no.uit.giella.keyboards.dev.liv_  | 7c5bfd28-fef2-4e24-8248-901f418ab256   |
|                     | appstore                               |                                        |
| Profile Name        | sigh_no.uit.giella.keyboards.dev.liv_  | match AppStore                         |
|                     | appstore_profile-name                  | no.uit.giella.keyboards.dev.liv        |
| Profile Path        | sigh_no.uit.giella.keyboards.dev.liv_  | /Users/srdkvr/Library/MobileDevice/Pr  |
|                     | appstore_profile-path                  | ovisioning                             |
|                     |                                        | Profiles/7c5bfd28-fef2-4e24-8248-901f  |
|                     |                                        | 418ab256.mobileprovision               |
| Development Team ID | sigh_no.uit.giella.keyboards.dev.liv_  | 2K5J2584NX                             |
|                     | appstore_team-id                       |                                        |
| Certificate Name    | sigh_no.uit.giella.keyboards.dev.liv_  | Apple Distribution: The University of  |
|                     | appstore_certificate-name              | Tromso (2K5J2584NX)                    |
+---------------------+----------------------------------------+----------------------------------------+

[21:29:47]: All required keys, certificates and provisioning profiles are installed 🙌
```


### 3. Add to build

Add you config to the `dependencies` in [project.yaml](divvun-dev.kbdgen/project.yaml).

```yml
  liv:
    url: "giellalt/keyboard-liv"
    layouts: ["liv"]
```

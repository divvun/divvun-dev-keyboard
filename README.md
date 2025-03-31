# Divvun Dev Keyboard

This repository exists for the purposes of triggering CI and CD. It is a kbdgen meta-repository, and serves as the basis for the content of the mobile keyboard apps.

If you want your keyboard to be built, update `divvun-dev.kbdgen/targets/android.yaml` or `divvun-dev.kbdgen/targets/ios.yaml`. [This](https://github.com/divvun/divvun-dev-keyboard/commit/c62eeaf12b3619ef7898f958f1371f52eca0ac0c) is the kind of edit you're looking for. 

Edits to the layouts should happen in the keyboard repos in [GiellaLT](https://github.com/giellalt), one repo for each language.


## Adding a new keyboard to Divvun Dev Keyboard 

1. Create identifier
2. Add to `project.yaml`
3. Trigger CI


### 1. Create identifier

1. Go to https://developer.apple.com/account/resources/identifiers/list  (log in with divvun.ios@gmail.com )
2. Click the "+" button next to the word Identifiers
3. Select "App IDs" on the "Register a new identifier" screen. Continue
4. Select type "App". Continue
5. Enter "Divvun Dev Keyboard liv" and "no.uit.giella.keyboards.dev.liv" as Descrition and BundleID (Explicit) respectively.
6. In capabilities, copy the settings from some other keyboard you like. For instance https://developer.apple.com/account/resources/identifiers/bundleId/edit/TUY9Q4GR35 (you'll add the actual App Group at the end)
7. Continue
8. Register
9. Once registered, click your newly created Identifier and click "Edit" next to App Groups and add `Divvun Keyboards Group - group.no.uit.giella.keyboards.dev`

The new identifier and associated certificates will be automatically picked up via [`fastlane match` by CI](https://github.com/divvun/kbdgen/blob/b079c5f445eb1f337de95aeac633924eca1eef25/src/build/ios/xcodebuild.rs#L208C1-L216C44) when it runs. No manual intervention should be needed with fastlane.


### 2. Add keyboard to `project.yaml`
Add the keyboard to the `dependencies` in [project.yaml](divvun-dev.kbdgen/project.yaml).

```yml
  liv:
    url: "giellalt/keyboard-liv"
    layouts: ["liv"]
```


### 3. Trigger CI
Bump the version/build number as mentioned before to trigger a new build. The new keyboard should appear as an option in the TestFlight/Google Play test build it generates.

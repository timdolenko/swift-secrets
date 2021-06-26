# swift-secrets

To avoid our iOS client-side secrets being leaked by reverse engineering, we will use GYB to obfuscate them.

Install [GYB](https://nshipster.com/swift-gyb/)

```
brew install nshipster/formulae/gyb
```

Add the following script to your target Build Phases, before Compile Sources:
```
find . -name '*.gyb' |
    while read file; do
        /usr/local/bin/gyb --line-directive '' -o "${file%.gyb}" "$file";
    done
```

1. Add Secrets.swift.gyb to your project folder
2. Save your secrets with name secrets.json in the root project folder
3. Build the project from XCode
4. Secrets.swift should appear, add it to the project inside XCode
5. Add Secrets.swift and secrets.json to your .gitignore file
6. Enjoy! 🎉

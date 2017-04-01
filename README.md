# iOS - multiple target with fastlane
Note for setting fastlane build app with multiple target in xcode

# Create environment
1.  Open terminal and go to fastlane folder, create env file for target.
```
touch .env.app1
```
2.  Open env file with text editor and add environment.
```
# Loaded from `fastlane <lane> --env app1`
SCHEME=App1 # target name
BUNDLE_ID=com.yourcompany.app1
METADATA=fastlane/metadata-app1
SCREENSHOTS=fastlane/screenshots-app1
```

# Download metadata and screenshots for target
Run command in terminal, replace metadata_path, screenshots_path and app_identifier to your owned.
1.  Download metadata
```
deliver download_metadata --metadata_path fastlane/metadata-app1 --app_identifier com.yourcompany.app1
```
2.  download screenshots
```
deliver download_screenshots --screenshots_path fastlane/screenshots-app1 --app_identifier com.yourcompany.app1
```

# Setting Fastfile
Open 'Fastfile' in text editor and change like this:
```
lane :release do options available
  gym(scheme: ENV['SCHEME'],
    workspace: "yourApp.xcworkspace",
    export_method: "app-store",
    include_bitcode: true)
  deliver(force: true,
  metadata_path: ENV['METADATA'],
  screenshots_path: ENV['SCREENSHOTS'],
  app_identifier: ENV['BUNDLE_ID'])
end
```

# Run fastlane command with enviroment
Using like this:
```
fastlane release --env app1
```

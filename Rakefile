# Default target, if no is provided
task default: [:setup]
# Steps for project environment setup
task :setup => [
    :pre_setup,
    :create_iphone_archive,
    :create_similator_archive,
    :create_xcframework,
]

# Color Helper
class String
    def colorize(color_code)
        "\e[#{color_code}m#{self}\e[0m"
    end
  
    def green
        colorize(32)
    end
end

task :pre_setup do
    puts 'Clear all archive ...'.green
    sh 'rm -rf xcframework && mkdir xcframework'
end

task :create_iphone_archive do
    puts "DivKit's SDK for iOS is archiving ...".green
    sh 'xcodebuild build \
    -scheme DivKit \
    -derivedDataPath ./builds/iphone \
    -arch arm64 \
    -sdk iphoneos'
end

# -archivePath xcframework/DivKit-iOS.xcarchive \
#     -destination "generic/platform=iOS"
#     SKIP_INSTALL=NO \
#     BUILD_LIBRARY_FOR_DISTRIBUTION=YES

task :create_similator_archive do
    puts "DivKit's SDK for iOS Similator is archiving ...".green
    sh 'xcodebuild build \
    -scheme DivKit \
    -derivedDataPath ./builds/simulator \
    -arch x86_64 \
    -sdk iphonesimulator'
end

task :create_xcframework do
    puts "Creating xcframework ...".green
    sh 'xcodebuild -create-xcframework \
    -library ./builds/iphone/Build/Products/Debug-iphoneos/libDivKit.a \
    -library ./builds/simulator/Build/Products/Debug-iphonesimulator/libDivKit.a \
    -output xcframework/DivKit.xcframework'
    puts "DivKit's xcframework output was created successfully.".green
    sh 'open .'
end

# -framework xcframework/DivKit-Sim.xcarchive/Products/Library/Frameworks/DivKit.framework \
#     -framework xcframework/DivKit-iOS.xcarchive/Products/Library/Frameworks/DivKit.framework \
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load("@build_bazel_rules_apple//apple:resources.bzl", "apple_resource_bundle")


apple_resource_bundle(
    name = "PerformanceTestAppAssets",
    bundle_id = "com.narlei.resources",
    resources = glob(["App/**/*.xcassets"]) + glob(["App/**/*.storyboard"]),
    visibility = ["//visibility:public"],
)


swift_library(
    name = "BaseSource",
    module_name = "BaseSource",
    srcs = glob(["App/**/*.swift"]),
    visibility = ["//visibility:public"],
    deps = [
        "//Libraries/LibraryA:LibraryA",
        "//Libraries/LibraryB:LibraryB",
        "//Libraries/LibraryC:LibraryC",
        "//Libraries/LibraryD:LibraryD",
    ]
)

ios_application(
    name = "ios-app",
    bundle_id = "com.narlei.sample",
    families = [
        "iphone",
        "ipad",
    ],
    infoplists = [":Info.plist"],
    deps = [
        ":BaseSource",
        ":PerformanceTestAppAssets",
        "//Libraries/LibraryA:LibraryA",
        "//Libraries/LibraryB:LibraryB",
        "//Libraries/LibraryC:LibraryC",
        "//Libraries/LibraryD:LibraryD",
    ],
    minimum_os_version = "15.0",
    visibility = ["//visibility:public"],
    resources = [":PerformanceTestAppAssets"]
)

load(
    "@com_github_buildbuddy_io_rules_xcodeproj//xcodeproj:defs.bzl",
    "top_level_target",
    "xcodeproj",
)

xcodeproj(
    name = "xcodeproj",
    build_mode = "bazel",
    project_name = "ios-app",
    tags = ["manual"],
    focused_targets = ["//Libraries/LibraryA:LibraryA"],
    top_level_targets = [
       top_level_target(":ios-app", target_environments = ["simulator"]),
    ],
)
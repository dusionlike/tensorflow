package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache

exports_files(["LICENSE"])

config_setting(
    name = "qnx",
    constraint_values = ["@platforms//os:qnx"],
    values = {
        "cpu": "x64_qnx",
    },
    visibility = [":__subpackages__"],
)

alias(
    name = "windows",
    constraint_values = ["@platforms//os:windows"],
    actual = select({
        ":windows_x64": ":windows_x64",
        ":windows_x86": ":windows_x86",
        "//conditions:default": ":windows_x64",  # Arbitrarily chosen from above.
    }),
    visibility = [":__subpackages__"],
)

config_setting(
    name = "windows_x64",
    values = {"cpu": "x64_windows"},
)

config_setting(
    name = "windows_x86",
    values = {"cpu": "x64_x86_windows"},
)

config_setting(
    name = "macos",
    constraint_values = [
        "@platforms//os:macos",
    ],
    visibility = [":__subpackages__"],
)

cc_library(
    name = "benchmark",
    srcs = glob(
        [
            "src/*.cc",
            "src/*.h",
        ],
        exclude = ["src/benchmark_main.cc"],
    ),
    hdrs = ["include/benchmark/benchmark.h"],
    linkopts = select({
        ":windows": ["-DEFAULTLIB:shlwapi.lib"],
        ":macos": ["-lpthread"],
        "//conditions:default": [
            "-pthread",
            "-lrt",
        ],
    }),
    strip_include_prefix = "include",
    visibility = ["//visibility:public"],
)

cc_library(
    name = "benchmark_main",
    srcs = ["src/benchmark_main.cc"],
    hdrs = ["include/benchmark/benchmark.h"],
    strip_include_prefix = "include",
    visibility = ["//visibility:public"],
    deps = [":benchmark"],
)

cc_library(
    name = "benchmark_internal_headers",
    hdrs = glob(["src/*.h"]),
)

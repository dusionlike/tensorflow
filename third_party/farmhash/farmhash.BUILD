licenses(["notice"])  # MIT

exports_files(["COPYING"])

alias(
    name = "windows",
    actual = select({
        ":windows_x64": ":windows_x64",
        ":windows_x86": ":windows_x86",
        "//conditions:default": ":windows_x64",
    }),
    visibility = ["//visibility:public"],
)

config_setting(
    name = "windows_x64",
    values = {"cpu": "x64_windows"},
)

config_setting(
    name = "windows_x86",
    values = {"cpu": "x64_x86_windows"},
)

cc_library(
    name = "farmhash",
    srcs = ["src/farmhash.cc"],
    hdrs = ["src/farmhash.h"],
    # Disable __builtin_expect support on Windows
    copts = select({
        ":windows": ["/DFARMHASH_OPTIONAL_BUILTIN_EXPECT"],
        "//conditions:default": [],
    }),
    includes = ["src/."],
    visibility = ["//visibility:public"],
)

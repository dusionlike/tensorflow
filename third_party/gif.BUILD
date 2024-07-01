# Description:
#   A library for decoding and encoding GIF images

licenses(["notice"])  # MIT

exports_files(["COPYING"])

cc_library(
    name = "gif",
    srcs = [
        "dgif_lib.c",
        "egif_lib.c",
        "gif_err.c",
        "gif_font.c",
        "gif_hash.c",
        "gif_hash.h",
        "gif_lib_private.h",
        "gifalloc.c",
        "openbsd-reallocarray.c",
        "quantize.c",
    ],
    hdrs = ["gif_lib.h"],
    defines = select({
        ":android": [
            "S_IREAD=S_IRUSR",
            "S_IWRITE=S_IWUSR",
            "S_IEXEC=S_IXUSR",
        ],
        "//conditions:default": [],
    }),
    includes = ["."],
    visibility = ["//visibility:public"],
    deps = select({
        ":windows": [":windows_polyfill"],
        "//conditions:default": [],
    }),
)

cc_library(
    name = "windows_polyfill",
    hdrs = ["windows/unistd.h"],
    includes = ["windows"],
)

genrule(
    name = "windows_unistd_h",
    outs = ["windows/unistd.h"],
    cmd = "touch $@",
)

alias(
    name = "windows",
    actual = select({
        ":windows_x64": ":windows_x64",
        ":windows_x86": ":windows_x86",
        "//conditions:default": ":windows_x64",  # Arbitrarily chosen from above.
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

config_setting(
    name = "android",
    values = {"crosstool_top": "//external:android/crosstool"},
)

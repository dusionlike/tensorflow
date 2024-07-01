# Description:
#   LMDB is the Lightning Memory-mapped Database.

licenses(["notice"])  # OpenLDAP Public License

exports_files(["LICENSE"])

cc_library(
    name = "lmdb",
    srcs = [
        "mdb.c",
        "midl.c",
    ],
    hdrs = [
        "lmdb.h",
        "midl.h",
    ],
    copts = [
        "-w",
    ],
    linkopts = select({
        ":windows": ["-DEFAULTLIB:advapi32.lib"],  # InitializeSecurityDescriptor, SetSecurityDescriptorDacl
        "//conditions:default": ["-lpthread"],
    }),
    visibility = ["//visibility:public"],
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

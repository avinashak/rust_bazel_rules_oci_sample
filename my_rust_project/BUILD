load("@rules_rust//rust:defs.bzl", "rust_binary")
load("@rules_oci//oci:defs.bzl", "oci_image")
load("@rules_pkg//pkg:pkg.bzl", "pkg_tar")
load("@crates//:defs.bzl", "aliases", "all_crate_deps")

rust_binary(
    name = "my_rust_binary",
    edition = "2024",
    srcs = ["src/main.rs"],
    deps = all_crate_deps(
        normal = True,
    ),
)

pkg_tar(
    name = "my_rust_tar",
    srcs = [":my_rust_binary"],
    package_dir = "/usr/local/bin",
)

oci_image(
    visibility = ["//visibility:public"],
    name = "my_rust_image",
    base = "@distroless_cc", # change to your base image, ideally multi platform
    tars = [
        ":my_rust_tar",
    ],
    env = {
        "SAMPLE_ENV_VAR": "VAL",
    },
    entrypoint = ["/usr/local/bin/my_rust_binary"],
)

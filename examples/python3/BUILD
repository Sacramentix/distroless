# Public notice: this file is for internal documentation, testing, and
# reference only. Note that repo maintainers can freely change any part of the
# repository code at any time.
load("@contrib_rules_oci//oci:defs.bzl", "oci_image", "oci_tarball")
load("@rules_pkg//:pkg.bzl", "pkg_tar")
load("//base:distro.bzl", "DISTROS")

pkg_tar(
    name = "hello_py",
    srcs = ["hello.py"],
)

# This example runs a python program that walks the filesystem under "/etc" and prints every filename.
oci_image(
    name = "hello_debian11",
    base = "//experimental/python3:python3_root_amd64_debian11",
    cmd = [
        "hello.py",
        "/etc",
    ],
    tars = [
        ":hello_py",
    ],
)

oci_image(
    name = "hello_debian12",
    base = "//python3:python3_root_amd64_debian12",
    cmd = [
        "hello.py",
        "/etc",
    ],
    tars = [
        ":hello_py",
    ],
)

# Run
# podman load -i bazel-bin/examples/python3/tarball/tarball.tar
# podman run localhost/distroless/examples/py:latest
[
    oci_tarball(
        name = "tarball_" + distro,
        image = ":hello_" + distro,
        repotags = ["distroless/examples/py:latest"],
    )
    for distro in DISTROS
]

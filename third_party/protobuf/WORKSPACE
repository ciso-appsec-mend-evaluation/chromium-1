workspace(name = "com_google_protobuf")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

local_repository(
    name = "com_google_protobuf_examples",
    path = "examples",
)

http_archive(
    name = "com_google_googletest",
    sha256 = "9dc9157a9a1551ec7a7e43daea9a694a0bb5fb8bec81235d8a1e6ef64c716dcb",
    strip_prefix = "googletest-release-1.10.0",
    urls = [
        "https://mirror.bazel.build/github.com/google/googletest/archive/release-1.10.0.tar.gz",
        "https://github.com/google/googletest/archive/release-1.10.0.tar.gz",
    ],
)

http_archive(
    name = "com_github_google_benchmark",
    sha256 = "e8af99057fbd85dc44e4ca9cb6afce571a228577ee01cd53b8633c548fa695eb",
    strip_prefix = "benchmark-f2f78087c2235e9e3156d0651be26660005a03a1",
    urls = [
        "https://github.com/google/benchmark/archive/f2f78087c2235e9e3156d0651be26660005a03a1.zip",
    ],
)

# Load common dependencies.
load("//:protobuf_deps.bzl", "PROTOBUF_MAVEN_ARTIFACTS", "protobuf_deps")
protobuf_deps()

bind(
    name = "python_headers",
    actual = "//util/python:python_headers",
)

load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = PROTOBUF_MAVEN_ARTIFACTS,
    # For updating instructions, see:
    # https://github.com/bazelbuild/rules_jvm_external#updating-maven_installjson
    maven_install_json = "//:maven_install.json",
    repositories = [
        "https://repo1.maven.org/maven2",
        "https://repo.maven.apache.org/maven2",
    ],
)

load("@maven//:defs.bzl", "pinned_maven_install")

pinned_maven_install()

# For `cc_proto_blacklist_test` and `build_test`.
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

# For `kt_jvm_library`
load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories")
kotlin_repositories()

load("@io_bazel_rules_kotlin//kotlin:core.bzl", "kt_register_toolchains")
kt_register_toolchains()

load("@upb//bazel:workspace_deps.bzl", "upb_deps")
upb_deps()

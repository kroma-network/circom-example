workspace(name = "kroma_network_circom_example")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "kroma_network_rules_circom",
    sha256 = "53f91f916b56e8f3070f1a594b625866afafe53057222a02796bee6f06dfc349",
    strip_prefix = "rules_circom-977a8c486949d86bd4099a4e85deca56a9e47233",
    urls = ["https://github.com/kroma-network/rules_circom/archive/977a8c486949d86bd4099a4e85deca56a9e47233.tar.gz"],
)

load("@kroma_network_rules_circom//:rules_circom_deps.bzl", "rules_circom_deps")

rules_circom_deps()

# Start of rules_rust
load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(
    edition = "2021",
    versions = [
        "1.66.1",
    ],
)

load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")

crate_universe_dependencies()

load("@rules_rust//crate_universe:defs.bzl", "crates_repository")

crates_repository(
    name = "crate_index",
    cargo_lockfile = "@kroma_network_rules_circom//:Cargo.lock",
    lockfile = "@kroma_network_rules_circom//:Cargo.Bazel.lock",
    manifests = ["@kroma_network_rules_circom//:Cargo.toml"],
)

load("@crate_index//:defs.bzl", "crate_repositories")

crate_repositories()
# End of rules_rust

local_repository(
    name = "kroma_network_tachyon",
    path = "third_party/tachyon",
)

load("@kroma_network_tachyon//bazel:tachyon_deps.bzl", "tachyon_deps")

tachyon_deps()

load("@kroma_network_tachyon//bazel:buildifier_deps.bzl", "buildifier_deps")

buildifier_deps()

local_repository(
    name = "kroma_network_circom",
    path = "third_party/tachyon/vendors/circom",
)

# Start of rules_js
load("@kroma_network_tachyon//bazel:js_deps.bzl", "js_deps")

js_deps()

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@aspect_bazel_lib//lib:repositories.bzl", "aspect_bazel_lib_dependencies")

aspect_bazel_lib_dependencies()

# Fetch and register node, if you haven't already
load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = DEFAULT_NODE_VERSION,
)

load("@aspect_rules_js//npm:repositories.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npm",
    data = ["@iden3_ffiasm//:package.json"],
    npm_package_lock = "@iden3_ffiasm//:package-lock.json",
    pnpm_lock = "@iden3_ffiasm//:pnpm-lock.yaml",
    update_pnpm_lock = True,
    verify_node_modules_ignored = "@iden3_ffiasm//:.bazelignore",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

# End of rules_js

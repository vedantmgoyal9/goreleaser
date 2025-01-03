# Builds (Zig)

<!-- md:version v2.5 -->

<!-- md:alpha -->

You can now build Zig binaries using `zig build` and GoReleaser!

Simply set the `builder` to `zig`, for instance:

```yaml title=".goreleaser.yaml"
builds:
  # You can have multiple builds defined as a yaml list
  - #
    # ID of the build.
    #
    # Default: Project directory name.
    id: "my-build"

    # Use zig.
    builder: zig

    # Binary name.
    # Can be a path (e.g. `bin/app`) to wrap the binary in a directory.
    #
    # Default: Project directory name.
    binary: program

    # List of targets to be built, in Zig's format.
    # Default: [ "x86_64-linux", "x86_64-macos", "x86_64-windows", "aarch64-linux", "aarch64-macos" ]
    targets:
      - aarch64-macos
      - x86_64-linux-gnu

    # Path to project's (sub)directory containing the code.
    # This is the working directory for the Zig build command(s).
    #
    # Default: '.'.
    dir: my-app

    # Set a specific zig binary to use when building.
    # It is safe to ignore this option in most cases.
    #
    # Default: "zig".
    # Templates: allowed.
    tool: "zig-nightly"

    # Sets the command to run to build.
    # Can be useful if you want to build tests, for example,
    # in which case you can set this to "test".
    # It is safe to ignore this option in most cases.
    #
    # Default: build.
    command: not-build

    # Custom flags.
    #
    # Templates: allowed.
    # Default: "-Doptimize=ReleaseSafe".
    flags:
      - --release

    # Custom environment variables to be set during the builds.
    # Invalid environment variables will be ignored.
    #
    # Default: os.Environ() ++ env config section.
    # Templates: allowed.
    env:
      - FOO=bar
```

Some options are not supported yet[^fail], but it should be usable at least for
simple projects already!

You can see more details about builds [here](./builds.md).

## Caveats

GoReleaser will translate Zig's Os/Arch pair into a GOOS/GOARCH pair, so
templates should work the same as before.
The original target name is available in templates as `.Target`, and so is the
ABI as `.Abi`.

[^fail]:
    GoReleaser will error if you try to use them. Give it a try with
    `goreleaser r --snapshot --clean`.

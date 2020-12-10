# Android bindings

## Build

In order to build Android bindings, first follow
[main README's instructions](/README.md) and then, from the project root,
follow the [Local](#local) or [In docker](#in-docker) instructions.

Both instructions will generate the artifacts (`library-debug.aar` and
`library-release.aar`) in `ffi/android/library/build/outputs/aar/`.

### Local

* Install dependencies: bash, cargo nightly, cmake, g++, git, libpcre3-dev, make, openjdk-11-jdk, rustc nightly, rustup, swig 4.0
* Install the Android SDK and export the env variable `ANDROID_SDK_ROOT` to its base path
* Install the Android NDK (version `20.1.5948944`) and export the env variable `NDK_HOME` to its base path
* Install the four cargo targets:
```
rustup target add aarch64-linux-android x86_64-linux-android armv7-linux-androideabi i686-linux-android
```
* Go to `ffi/android` and then:
    * Update the `PATH` in `build_rust.sh` script if you're not building from x86_64
    * Run `./gradlew build` (if something fails, manually run the `build_rust.sh` script for a better error report)

### In docker

```bash
docker build -f ffi/android/Dockerfile -t rgb-sdk-android .
mkdir -p ffi/android/library/build/outputs/aar
docker run --rm -v $(pwd):/opt/mount --entrypoint bash \
    rgb-sdk-nodejs \
    -c 'cp /rgb-sdk/ffi/android/library/build/outputs/aar/*.aar /opt/mount/ffi/android/library/build/outputs/aar/'
```

## Usage

To try the generated library, you can use:
- [android demo](/demo/android)
- [react-native demo](/demo/react-native)

# protobuf-partial

Derived from protobuf 3.3.0.

## Instructions for building for Android stlport

```
cd protobuf-partial
export NDK_ROOT=/home/user/SDKS/ANDROID/NDK/android-ndk-r13b
export SYSROOT=$NDK_ROOT/platforms/android-9/arch-arm
export PREBUILT=$NDK_ROOT/toolchains/arm-linux-androideabi-4.9
export LDFLAGS="--sysroot=$SYSROOT"
export LD="$NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/arm-linux-androideabi/bin/ld $LDFLAGS"
export LIBS="-llog $NDK_ROOT/sources/cxx-stl/stlport/libs/armeabi-v7a/libstlport_static.a"
export CPPFLAGS="-D__ANDROID__=1 -DANDROID_STLPORT=1"
export INCLUDES="-I$NDK_ROOT/sources/cxx-stl/stlport/stlport/ -I$NDK_ROOT/platforms/android-9/arch-arm/usr/include/"
export CXXFLAGS="-march=armv7-a -mfloat-abi=softfp -DGOOGLE_PROTOBUF_NO_RTTI --sysroot=$SYSROOT"
export CCFLAGS="$CXXFLAGS"
export CXX="$PREBUILT/prebuilt/linux-x86_64/bin/arm-linux-androideabi-g++ $CXXFLAGS"
export CC="$CXX"
./autogen.sh
./configure --host=arm-linux-androideabi --with-sysroot=$SYSROOT --enable-cross-compile --with-protoc=protoc --disable-static --enable-shared CXX="$CXX" CC="$CC" LD="$LD"
make
mkdir -p ~/git/project/build/protobuf_android_stlport/
cp -v src/.libs/* ~/git/project/build/protobuf_android_stlport/
```

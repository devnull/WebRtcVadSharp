VERSION = 1.4.0

CFLAGS = -I. -fPIC -DWEBRTC_POSIX -DNDEBUG
LDFLAGS = -shared

LINUX_TARGET = libwebrtcvad.so
MACOS_TARGET = libwebrtcvad.dylib
SOURCES = $(shell find . -type f -iname '*.c')
HEADERS = $(shell find . -type f -iname '*.h')
OBJECTS = $(SOURCES:.c=.o)

# Linux targets
lib-linux-x64: CC=gcc
lib-linux-x64: $(OBJECTS)
	mkdir -p runtimes/linux-x64/native
	$(CC) $(LDFLAGS) -o runtimes/linux-x64/native/$(LINUX_TARGET) $(OBJECTS)

lib-linux-arm64: CC=aarch64-linux-gnu-gcc
lib-linux-arm64: $(OBJECTS)
	mkdir -p runtimes/linux-arm64/native
	$(CC) $(LDFLAGS) -o runtimes/linux-arm64/native/$(LINUX_TARGET) $(OBJECTS)

# macOS targets
lib-osx-arm64: CC=clang -arch arm64
lib-osx-arm64: $(OBJECTS)
	mkdir -p runtimes/osx-arm64/native
	$(CC) -dynamiclib -o runtimes/osx-arm64/native/$(MACOS_TARGET) $(OBJECTS)

lib-osx-x64: CC=clang -arch x86_64
lib-osx-x64: $(OBJECTS)
	mkdir -p runtimes/osx-x64/native
	$(CC) -dynamiclib -o runtimes/osx-x64/native/$(MACOS_TARGET) $(OBJECTS)

clean:
	rm -rf $(OBJECTS) bin obj runtimes

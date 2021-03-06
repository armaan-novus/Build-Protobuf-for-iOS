# Google Protobuf - Mac OS X and iOS Support

The script in this gist will help you buid the Google Protobuf library for use
with Mac OS X and iOS.  Other methods (such as homebrew or direct compilation)
have issues that prevent their use. The libraries built by this script are
universal and support all iOS device architectures including the simluator.

# Get the Script

The easiest way to use this script is to simply clone the repo onto your
machine using the following command:

```
$ git clone https://github.com/armaan-novus/Build-Protobuf-for-iOS.git
```

# Performing the Build

The script will automatically download the tarball from Google Code, so
all you need to do is run the script. This will build the 3.17.3 version of
Protobuf. The script understands a few command-line options too.

```
$ ./build-protobuf.sh
```

Add `--interactive` to the above script if you would like the script to stop
after each major operation. This makes it easier to inspect the output from
the various steps for potential errors.

Add `--master` if you would prefer to build from the master branch in the 
Google Protobuf git repo.

# Results

Build results are found in a folder called `protobuf` This folder contains `bin`, `include` and `lib` folders.  

# Integration with Xcode

Create a build rule in your Xcode project with the following settings.

    Process *Source files with names matching:* `*.proto`
    Using *Custom script:*

    cd ${INPUT_FILE_DIR}
    ${SRCROOT}/Google/protobuf/bin/protoc --proto_path=${INPUT_FILE_DIR} ${INPUT_FILE_PATH} --cpp_out=${DERIVED_FILE_DIR}

    Output Files
    $(DERIVED_FILE_DIR)/$(INPUT_FILE_BASE).pb.cc
    $(DERIVED_FILE_DIR)/$(INPUT_FILE_BASE).pb.h

Depending on where you choose to install the protobuf build, you will 
need to adjust the path to `protoc`.


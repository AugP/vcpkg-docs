---
title: vcpkg_install_copyright
description: Learn how to use vcpkg_install_copyright.
ms.date: 01/10/2024
---
# vcpkg_install_copyright

Merges multiple copyright files into a single file and install it.
Installs a single copyright file.

>[!NOTE]
> The licensing information provided for each package in the vcpkg registry represents Microsoft's best understanding of the licensing requirements. However, this information may not be definitive. Users are advised to verify the exact licensing requirements for each package they intend to use, as it is ultimately their responsibility to ensure compliance with the applicable licenses.

## Usage

```cmake
vcpkg_install_copyright(FILE_LIST <file1> <file2>... [COMMENT])
```

## Parameters

### FILE_LIST

Specifies a list of license files with absolute paths. You must provide at least one file.

### COMMENT

This optional parameter adds a comment before at the top of the file. 

## Notes

This function creates a file called `copyright` inside `${CURRENT_PACKAGES_DIR}/share/${PORT}`

If more than one file is provided, this function concatenates the contents of multiple copyright files to a single file.

The resulting `copyright` file looks similar to this:

```
LICENSE-LGPL2.txt:

Lorem ipsum dolor...

LICENSE-MIT.txt:

Lorem ipsum dolor sit amet...
```

Or with `COMMENT`:

```
A meaningful comment

LICENSE-LGPL2.txt:

Lorem ipsum dolor...

LICENSE-MIT.txt:

Lorem ipsum dolor sit amet...
```

## Examples

```cmake
vcpkg_install_copyright(FILE_LIST "${SOURCE_PATH}/LICENSE/license.md" "${SOURCE_PATH}/LICENSE/license_gpl.md" COMMENT "This is a comment")
```

You can also collect the required files using a `GLOB` pattern:

```cmake
file(GLOB LICENSE_FILES "${SOURCE_PATH}/LICENSES/*")
vcpkg_install_copyright(FILE_LIST ${LICENSE_FILES})
```

## Source

[vcpkg_install_copyright.md](https://github.com/Microsoft/vcpkg/blob/master/scripts/cmake/vcpkg_install_copyright.cmake)

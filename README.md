**Table of contents :**
- [Introduction](#1-introduction)
- [Current version](#2-current-version)
- [How to use](#3-how-to-use)
- [License](#4-license)

# Introduction

This repository allow to use [QCustomPlot][qcp-main] as a shared library compliant with [CMake][cmake] build system.  
Besides, this repository also provides _community patches_ available.

# Current version

Official changelog of the library can be found at [official changelog][changelog-official] file.  
This repository also provide a [changelog][changelog-repo] in order to track change differences with the official version (represented by **tweak** version property).

| Library version | Qt compatibility |
| :-: | :-: |
| [2.1.1.1.ul][tag-2.1.1.1.ul] | move files:  `lib/*` -> `./*` |
| [2.1.1.1][tag-2.1.1.1] | `Qt 4.6.x` -> `Qt 6.4.x` |
| [2.1.0.2][tag-2.1.0.2] | `Qt 5.8.x` -> `Qt 6.2.x` |
| [2.1.0.1][tag-2.1.0.1] | `Qt 4.6.x` -> `Qt 6.0.0` |

# How to use

This library can be use as an _embedded library_ in a subdirectory of your project (like a _git submodule_ for example) :
1. In the **root** CMakeLists, add instructions :
```cmake
add_subdirectory(qcustomplot) # Or if library is put in a folder "dependencies" : add_subdirectory(dependencies/qcustomplot)
```

2. In the **application/library** CMakeLists, add instructions :
```cmake
# Link needed libraries
# QCustomPlot library
target_link_libraries(${PROJECT_NAME} PRIVATE qcustomplot)

# Compile needed definitions
target_compile_definitions(${PROJECT_NAME} PRIVATE QCUSTOMPLOT_USE_LIBRARY)
```
> Examples of how to use the library can be found in the associated repository [QCustomPlot-examples][repo-qcp-examples]

# License

[QCustomPlot][qcp-main] is released under [GPL-3.0 License][license], so as this repository.

<!-- Links to QCustomPlot website -->
[qcp-main]: https://www.qcustomplot.com/index.php/introduction
[qcp-doc]: https://www.qcustomplot.com/documentation/index.html

<!-- Links to useful resources -->
[cmake]: https://cmake.org/

<!-- Links to external repositories -->
[repo-qcp-examples]: https://github.com/legerch/QCustomPlot-examples

<!-- Links to this repository -->
[changelog-repo]: https://github.com/legerch/QCustomPlot-library/blob/dev/CHANGELOG.md
[changelog-official]: https://github.com/legerch/QCustomPlot-library/blob/dev/changelog-official.txt
[license]: https://github.com/legerch/QCustomPlot-library/blob/master/LICENSE.md

[tag-2.1.1.1.ul]: https://github.com/UmbrellaLeaf5/qcustomplot/releases/tag/2.1.1.1.ul
[tag-2.1.1.1]: https://github.com/legerch/QCustomPlot-library/releases/tag/2.1.1.1
[tag-2.1.0.2]: https://github.com/legerch/QCustomPlot-library/releases/tag/2.1.0.2
[tag-2.1.0.1]: https://github.com/legerch/QCustomPlot-library/releases/tag/2.1.0.1

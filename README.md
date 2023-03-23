## RPI Pico Temp Alarm

This project provides a simple measurements of temperature on various places in object and raises alarm when any point exceeds set threshold.


Using VianPatel/mlx90640-RPI-Pico driver for communication between a raspberry pi pico and an mlx90640 thermal sensor.

The api can be found in the `include` and `src` folders.

The `sample` folder contains example code showing how to use the api, along with a header only library `ThermalCamera.h` that provides a simple to use wrapper.


**Hardware setup:**

Using the api or sample requries the following hardware setup.

Connect the mlx90640 camera pins as follows:

```
(mlx90640 pin) -> (pico pin)
sda -> gp4
scl -> gp5
gnd -> gnd
3-6v -> 3v3
```



**Using the api in your project:**

`git submodule add https://github.com/VianPatel/ThermalCamera-RPI-Pico.git` (or `git clone` if you prefer to not use submodules)

Put the following in your `CMakeLists.txt`:

```
# MLX90640 api
add_subdirectory("pathToSubmoduleRepoRoot" mlx90640api)
target_link_libraries(${CMAKE_PROJECT_NAME} mlx90640-RPI-Pico)
```

replace `pathToSubmoduleRepoRoot` with the path to the submodule root


**Compiling sample:**

install gcc-arm-none-eabi from:


https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
or with: `sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib`


```
git clone https://github.com/VianPatel/ThermalCamera-RPI-Pico.git
```

```
cd ThermalCamera-RPI-Pico
```

```
git submodule update --init pico-sdk/
```

```
cd pico-sdk
```

```
git submodule update --init lib/tinyusb/
```

```
cd ../
```

```
mkdir build
```

```
cd build
```





```
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH="fullPathToCompiler" -DCMAKE_CXX_COMPILER:FILEPATH="fullPathToCompiler" ../sample
```

With `fullPathToCompiler` filled in, this command might look something like:

```
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH="/usr/bin/arm-none-eabi-gcc" -DCMAKE_CXX_COMPILER:FILEPATH="/usr/bin/arm-none-eabi-g++" ../sample
```





```
cmake --build .
```





**Sample usage:**

Copy `ThermalCamera.uf2` from the `build` folder to the pico's root folder


Establish a connection to the pico's com port (this can be done via putty on windows)

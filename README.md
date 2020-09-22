# Docker-Robot-Framework-Appium
For building images containing Appium(server) and Robot-Framework with AppiumLibrary

## How to build
 ```$ docker build -t rf-appium-server path/to/folder/Dockerfile-folder```
 Or with test source form git (contents downloaded to /test folder)
 ```$ docker build -t rf-appium-server --build-arg TEST_SRC_PATH=https://github.com/qubilea-sadinmaki/Oma-Fortum-Robot-Framework-Appium.git path/to/folder/Dockerfile-folder```
**or**
```$ docker build -t rf-appium-server --build-arg TEST_SRC_PATH=https://github.com/qubilea-sadinmaki/Oma-Fortum-Robot-Framework-Appium.git https://github.com/qubilea-sadinmaki/Docker-Robot-Framework-Appium.git#:robot-appium-android```

The following --build-args are available:
* TEST_SRC_PATH (this copies source from git)

## Mount the USB devices connected to Docker host machine
```$ docker-machine --version
$ docker-machine version 0.10.0, build 76ed2a6```

```$ docker-machine create --driver virtualbox appium-test-machine```

```$ docker-machine stop appium-test-machine
$ vboxmanage modifyvm appium-test-machine --usb on --usbehci on
$ docker-machine start appium-test-machine```

```$ adb kill-server```

```$ docker-machine ssh appium-test-machine```

```$ docker run --privileged -d -p 4723:4723  -v /dev/bus/usb:/dev/bus/usb --name container-appium appium/appium```

```$ docker exec -it container-appium adb devices```

```$ docker exec -it container-appium robot /test/testfile.robot```


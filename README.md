# journey-of-self-driving-car-systems

Perhaps it is another [CARLA](https://carla.org/) setup and configuration repo, it also includes a simple path planning and configuration that should be done on a Linux system.

## Requirements

The requirements to build the proyect:

1- PC with Ubuntu18.04/20.04. Minimum ram 8GB

2- At least 250GB of hard disk space

3- 

## Steps to Build and lauch

Config my environment

* Carla: 0.9.10
* Ubuntu Focal 20.04

for other Ubuntu versions the commands may be different. I recommend reading the official documentation and [installation on Linux](https://carla.readthedocs.io/en/latest/build_linux/).

It is advisable to use python virtual intonors. in my case I use [conda](https://docs.conda.io/projects/conda/en/stable/).

1- Create and activate the conda environment

```
    $conda create -n [ENVNAME] python=3.8

    $conda activate [ENVNAME]
```

2- Install dependencies.

```
    $sudo apt-get update &&

    $sudo apt-get install wget software-properties-common

    $sudo add-apt-repository ppa:ubuntu-toolchain-r/test

    $wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add

    $sudo apt-add-repository "deb http://apt.llvm.org/focal/ llvm-toolchain-focal main"

    $sudo apt-get update

    $sudo apt-get install build-essential clang-10 lld-10 g++-7 cmake ninja-build libvulkan1 python python-dev python3-dev python3-pip libpng-dev libtiff5-dev libjpeg-dev tzdata sed curl unzip autoconf libtool rsync libxml2-dev git

    $sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/lib/llvm-10/bin/clang++ 180

    $sudo update-alternatives --install /usr/bin/clang clang /usr/lib/llvm-10/bin/clang 180
```

3- Install dependencies Python

```
    $pip3 install -upgrade pip

    $pip3 install --user -Iv setuptools==47.3.1

    $pip3 install --user distro

    $pip3 install --user wheel auditwheel
```

4- Install Unreal

```
    $git clone https://github.com/CarlaUnreal/UnrealEngine.git

    $cd UnrealEngine-4.26

    $./Setup.sh && ./GenerateProjectFiles.sh && make

```

Verify the installation of Unreal you should be able to open the editor window.

```
    $cd ~/UnrealEngine-carla/Engine/Binaries/Linux && ./UE4Editor
```

5- Install [CARLA](https://carla.org/)

```
    $sudo apt-get install aria2

    $git clone https://github.com/carla-simulator/carla

    $cd ~/carla && git checkout -b tags/0.9.10

    $./Update.sh
```

6- Build [CARLA](https://carla.org/)

You need to Modify bashrc Files
```
    $cd && vim ~/.bashrc
```

Add text to bottom line: `export UE4_ROOT=~/YOUT/PATH/UNREALENGINE-CARLA`

Into the line 6th line `carla/Util/BuildTools/BuildCarlaUE4.sh` include `UE4_ROOT=~/YOUT/PATH/UNREALENGINE-CARLA`

```
    $cd ~/carla && make PythonAPI

    $make launch
```

### First steps and configuration.

It is required to have the 2000, 2001, 2002 ports (TCP - UDP) enabled and available. You can check with:

```
    $sudo ufw status
```

If you have problems, you could disable Firewal, REMEMBER THIS IS DANGEROUS IF YOU DO IT IN PUBLIC LOCATIONS.

```
    $sudo ufw disable
```

In carla's folder, you can run the server mode with different scenarios. you could use.

```
    $./CarlaUE4.sh /Game/Maps/RaceTrack -windowed -ResX=800 -ResY=600 -quality-level=low -nosound -benchmark -fps=20 -carla-server

    or 

    $./CarlaUE4.sh /Game/Maps/Town01 -windowed -ResX=800 -ResY=600 -quality-level=low -nosound -benchmark -fps=20 -carla-server

    or 

    $./CarlaUE4.sh /Game/Maps/Town02 -windowed -ResX=800 -ResY=600 -quality-level=low -nosound -benchmark -fps=20 -carla-server
```

In another terminal window you can run the client.

```
    $python ...this_repo/PythonClient/manual_control.py
```

or runt the pathFollow

```
    $python ...this_repo/PythonClient/pathFollow.py
```



......under contruction.........



### TODO

*------------

*------------

*------------

## Autor

* Juan D. Valenciano - (jvalenciano@unal.edu.co)

## License

unlicense

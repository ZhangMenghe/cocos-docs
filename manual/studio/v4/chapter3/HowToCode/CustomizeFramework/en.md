# Instructions of self-compiled Cocos Framework & Simulator


## Introduction

This document describes how to customize Cocos Framework & Simulator and then apply the customized Cocos Framework & Simulator into game project.

Customizing Cocos Framework is a process, which users can modify and customize the source code of engine to use after installing Cocos Framework.

## Version Requirement
Customizing Cocos Framework is a new feature in v3.7 
and is not supported by versions below 3.7.

Paths mentioned in the following contents are on basis of v3.7. To get the specific one, please check the actual installation directory of your own Cocos Framework.

## How to customize Cocos Framework

Customizing Cocos Framework is to modify the installation source code in practice. 
Users are free to choose their own IDE tool or code editor to make modification
once the Cocos Framework is installed. 

* For Mac users, open the project file  `/Applications/Cocos/frameworks/cocos2d-x-v3.7/build/CocosFramework.xcodeproj` in XCode then do change and debug. 
* For Windows users, open the project file `[Installation directory]/frameworks/cocos2d-x-v3.7/build/CocosFramework.sln` in Visual Studio then do change and debug.

## How to build the customized Cocos Framework

### Rebuild the precompiled libraries

There is a script tool attached to Cocos Framework that can compile source code to precompiled libraries: `frameworks/cocos2d-x-v3.7/tools/framework-compile/gen_cocos_libs.py`.



Instructions of the Script tool:


	usage: gen_cocos_libs.py [-h] [-c] [-all] [--win] [--mac] [--ios] [--android]
                         [--dis-strip] [--vs VS_VERSION] [--app-abi APP_ABI]

	build new precompiled libraries for Cocos Framework

	Optional parameters:

     -h, --help            help message

     -c                    delete prebuilt folder before compile

     -all                  compile all plateforms（for Mac system: Mac,iOS and Android;for Windows system: Win32 and Android）

     --win                 compile Win32 plateform

     --mac                 compile Mac plateform

     --ios                 compile iOS plateform

     --android             compile Android plateform

     --dis-strip, --disable-strip  close function strip, no strip in new .a file in following compilation.(affect precompiled libraries on Mac,iOS and Android )

     --vs VS_VERSION       Specify the version of Visual Studio or else search the avaliable automatically

     --app-abi APP_ABI     Specify value of parameter APP_ABI for ndk-build. Use ':' to separate values. e.g.--app-abi armeabi:x86. by default armeabi.

Samples:

1. `python gen_cocos_libs.py -c -all` clear all precompiled libraries and compile all plateforms
2. `python gen_cocos_libs.py --win --vs 2015` use VS2015 to compile Win32 plateform

The precompiled libraries exist in `frameworks/cocos2d-x-v3.7/prebuilt` folder.The game project can link to new precompiled libraries directly.

Notes:

* Customizing Cocos Framework includes modifying source code and maintaining 
corresponding project files. If erros are introduced to customized code or project configuration, the compiler may fail to execute.

## Rebuild simulator

There is a script tool attached to Cocos Framework that compile source code to precompiled libraries: `frameworks/cocos2d-x-v3.7/tools/framework-compile/gen_cocos_simulator.py`.

Instructions of the Script tool：


	usage: gen_cocos_simulator.py [-h] [-c] [-m {debug,release}] [-o OUT_DIR] -p
                              {ios,mac,android,win32,all} [--vs VS_VERSION]

	Rebuild simulator

	Optional parameters:

	-h, --help            help message

    -c, --clean           delete specific output directory before rebuild

    -m {debug,release}, --mode {debug,release}	modal of simulator,options:debug,release

    -o OUT_DIR, --output OUT_DIR	path of new simulator.default path: "frameworks/cocos2d-x-v3.7/simulator"

    -p {ios,mac,android,win32,all}, --platform {ios,mac,android,win32,all} plateforms to compile.When set "all", Mac system will compile Mac,iOS and Android; Windows systme will compile Win32 and Android

    --vs VS_VERSION       pecify the version of Visual Studio or else search the avaliable


Samples：

1. `python gen_cocos_simulator.py -c -p all` clear previous simulator and compile all
2. `python gen_cocos_libs.py -p win32 --vs 2015` use VS2015 to compile simulator on Win32 plateform

## Integrate custom simulator:

Cover the files under **[Installation directory]/Cocos/cocos-simulator-bin** 
by new compiled simulator files to make use of custom simulator.

Notes:

* Simulator is mainly used to preview in resource editor. Replace former simulator in resource editor by the new one to make it work.

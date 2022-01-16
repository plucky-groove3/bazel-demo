# bazel-demo

## INSTALL BAZEL

https://docs.bazel.build/versions/4.2.2/install-ubuntu.html

Using Bazel's apt repository

Step 1: Add Bazel distribution URI as a package source

```
sudo apt install curl gnupg
curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor > bazel.gpg
sudo mv bazel.gpg /etc/apt/trusted.gpg.d/
echo "deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
```

Step 2: Install and update Bazel

```
sudo apt update && sudo apt install bazel
sudo apt update && sudo apt full-upgrade
#sudo apt install bazel-1.0.0
```

Using the binary installer

Step 1: Install required packages
Bazel needs a C++ compiler and unzip / zip in order to work:
sudo apt install g++ unzip zip

Step 2: Run the installer
Next, download the Bazel binary installer named bazel-<version>-installer-linux-x86_64.sh from the Bazel releases page on GitHub.

chmod +x bazel-<version>-installer-linux-x86_64.sh
./bazel-<version>-installer-linux-x86_64.sh --user

Step 3: Set up your environment
If you ran the Bazel installer with the --user flag as above, the Bazel executable is installed in your $HOME/bin directory. It’s a good idea to add this directory to your default paths, as follows:

export PATH="$PATH:$HOME/bin"
You can also add this command to your ~/.bashrc or ~/.zshrc file to make it permanent.


## WORKSPACE


## BUILD

bazel build //main:hello-world
bazel clean

## RULES

cc_binary  name.stripped;name.dwp
cc_import  import precompiled C/C++ libraries.
cc_library
cc_proto_library  generates C++ code from .proto files.
fdo_prefetch_hints
fdo_profile
propeller_optimize
cc_test
cc_toolchain
cc_toolchain_suite

# GRAPH
命令行
bazel query --notool_deps --noimplicit_deps "deps(//main:hello-world)" \
  --output graph

图形化
sudo apt update && sudo apt install graphviz xdot
xdot <(bazel query --notool_deps --noimplicit_deps "deps(//main:hello-world)" \
  --output graph)

# DEFINITION
https://docs.bazel.build/versions/main/be/common-definitions.html


```
bazel build :multiplatform_lib --cpu x86
```

BUILD文件:

```
cc_library(
    name = "multiplatform_lib",
    srcs = select({
        ":x86_mode": ["x86_impl.cc"],
        ":arm_mode": ["arm_impl.cc"]
    })
)
config_setting(
    name = "x86_mode",
    values = { "cpu": "x86" }
)
config_setting(
    name = "arm_mode",
    values = { "cpu": "arm" }
)
```

Kconfig怎么解决？不太好支持
https://docs.bazel.build/versions/main/skylark/config.html
替代：select 产品？


cmake中使用bazel？
https://opensourcelibs.com/lib/bazel.cmake

bazel中使用cmake?
原生支持
https://bazelbuild.github.io/rules_foreign_cc/

conan中使用bazel?
原生支持
https://docs.conan.io/en/latest/integrations/build_system/bazel.html


catkin/colcon中使用bazel? 
原生不支持，适配困难。 

交叉编译 ceva、gcc等如何制定工具链
https://opensourcelibs.com/lib/bazel-embedded


其他应用
fuzz https://opensourcelibs.com/lib/rules_fuzzing
asan

bazelcon 2019 https://oasisdigital.com/class/bazel
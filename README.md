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
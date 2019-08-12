# Setting up MacOS Development Environment

## Installing Xcode Command Line Tools

Run the following command (in Terminal):

```
xcode-select --install
```

_Note: The Xcode command line toolkit is installed in `/Library/Developer/CommandLineTools/` directory._

## Installing Homebrew

Run the following command:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

For detailed usage of Homebrew, see this [tutorial](./homebrew.md)

## Installing and Configure Git

1. Run the following command to install Git

```
brew install git
```

To verify, run `git --version`.

2. Run the following commands to configure Git

```
git config --global user.name "Your Name"
git config --glabal user.email "username@example.com"
```

## Setting up Java Development Environment

1. First, install `sdkman` using the following commands:

```
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

2. To JDK with `sdkman`, first find a OpenJDK distro:

```
sdk ls java
```

Then install the JDK using `sdk install <jdk-distro-id>`.

To verify, run `java -version` and `javac -version`.

3. Optionally, install `Maven` or `Gradle`:

```
sdk install maven
sdk install gradle
```

4. Install IntelliJ IDEA CE with Homebrew,

```
brew cask install intellij-idea-ce
```

## Setting up Python Development Environment

_Make sure `wget` is installed. If not, run `brew install wget`._

1. Download and run [Anaconda Installer](https://repo.anaconda.com/archive/Anaconda3-2019.07-MacOSX-x86_64.sh):

```
cd ~/Downloads
wget https://repo.anaconda.com/archive/Anaconda3-2019.07-MacOSX-x86_64.sh
bash Anaconda3-2019.07-MacOSX-x86_64.sh
```

Follow the instruction to finish the installation. To verify successful installation, run `python --version`.

2. Install Visual Studio Code and Microsoft Python Extension

See VS Code installation [instructions](https://code.visualstudio.com/docs/setup/mac) and installing
[Python VS Code Extension](https://code.visualstudio.com/docs/python/python-tutorial).

## Setting up Node.js (JavaScript) Development Environment

1. Install Node.js with Homebrew:

```
brew install node
```

To verify, `node -v` and `npm -v`.

## Installing Relational Database System (MySQL)

1. Install MySQL server:

```
brew install mysql
```

2. Install `brew services`:

```
brew tap homebrew/services
```

3. Load and start MySQL service

```
brew services start mysql
```

4. Install MySQL Workbench (GUI client)

```
brew cask install mysqlworkbench
```

## Installing NoSQL Database (MongoDB)

1. Install MongoDB with Homebrew:

```
brew install mongodb
```

2. Install `brew services`:

```
brew tap homebrew/services
```

3. Load and start MongoDB service

```
brew services start mongodb
```

4. Install MongoDB GUI client

```
brew cask install robo-3t
```

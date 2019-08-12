# Homebrew Tutorial

## Installation

First make sure the Xcode is installed:

```
xcodebuild -version
```

If Xcode is not installed, run the following command:

```
xcode-select --install
```

To install Homebrew, run the following command:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Homebrew Terminologies

- cask - GUI apps
- formula - application package

## List All Installed Packages

To list all installed command line packages:

```
brew list
```

Or to list all installed GUI apps

```
brew cask list
```

## Search for Packages

```
brew search <search-text>
```

## Showing Package Info

```
brew info <formula>
```

## Installing a New Package

To install a command line app:

```
brew install <formula>
```

To install a MacOS GUI app:

```
brew cask install <formula>
```

## Uninstalling a Package

```
brew [cask] uninstall <formula>
```

## Updating Brew and Cask

```
brew update
```

## Checking What needs to be Updated

```
brew outdated
```

## Updating All Outdated Packages

```
brew upgrade
```

## Cleaning Up

```
brew cleanup
```

## Checking System for Potential Problems

```
brew doctor
```

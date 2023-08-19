# Build only Cordova Hot Code Push Plugin CLI client

This is a stripped-down build only command line utility for [Cordova Hot Code Push Plugin](https://github.com/nordnet/cordova-hot-code-push). It only builds the chcp files needed for new builds.

Main features are:
- It builds chcp files.

## Documentation

- [Installation](#installation)
- [How to use](#how-to-use)
- [Commands](#commands)
  - [Build command](#build-command)
- [Default configuration file](#default-configuration-file)
- [Ignored files list](#ignored-files-list)

### Installation

Install via repo url directly:
```sh
npm install -g https://github.com/calumsult/cordova-hot-code-push-cli
```

### How to use

```sh
cordova-hcp <command>
```

Where `<command>` can be:
- `build` - build project files, generate `chcp.json` and `chcp.manifest` files in the `www` folder. Prepare for deployment.

All commands should be executed in the root folder of your Cordova project. For example, lets assume you have a Cordova `TestProject` with the following structure:
```
TestProject/
  config.xml
  hooks/
  node_modules/
  platforms/
  plugins/
  www/
```
Then `cordova-hcp` commands should be executed in the `TestProject` folder.

### Commands

#### Build command

```sh
cordova-hcp build [www_directory]
```

where:
- `[www_directory]` - path to the directory with your web project. If not specified - `www` is used.

Command is used to prepare project for deployment and to generate plugin specific configuration files inside `www` folder:
- `chcp.json` - holds release related information.
- `chcp.manifest` - holds information about web project files: their names (relative paths) and hashes.

When executed - you will see in the terminal window:
```
Running build
Build 2015.09.07-11.20.55 created in /Cordova/TestProject/www
```

As a result, `chcp.json` and `chcp.manifest` files are generated in the `www` folder and project is ready for deployment.

More information about those configs can be found on [Cordova Hot Code Push plugin](https://github.com/nordnet/cordova-hot-code-push) documentation page.

### Default configuration file

Create `cordova-hcp.json` manually and put in there any options you want. It's just a JSON object like so:
```json
{
  "update": "start",
  "content_url": "https://mycoolserver.com/mobile_content/"
}
```

By default, you would probably put in there your `content_url`. But it can also be any other setting.

### Ignored files list

By default, CLI client ignores all hidden files, and files from the following list:
```
chcp.json
chcp.manifest
package.json
node_modules/*
```

But if you want - you can extend this list like so:

1. Create `.chcpignore` file in the root of your Cordova Project (for example, `/Cordova/TestProject/.chcpignore`).
2. Add ignored files. For example:

```
dirty.html
images/*
libs/*
```
As a result, those files will be excluded from the `chcp.manifest`.

If you want - you can add comments by using `#` like this:

```
# Ignore libraries
libs/*

# Ignore images
images/*
```
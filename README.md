# virtualbox-extensionpack-rpm
An RPM packaging script and specfile for VirtualBox Extension Packs.

Most useful on a Fedora OSTree distribution where the pack can only be installed if it's an RPM.  


## Usage

_Roughly taken from [here](https://docs.fedoraproject.org/en-US/package-maintainers/Packaging_Tutorial_GNU_Hello/)_

### Setup

1. Create a toolbox for regular fedora matching your current release version (release version is `38` in this example), and enter it

```
toolbox create -d fedora -r 38 vbox-ext-build
toolbox enter vbox-ext-build
```

2. [Install the build tools](https://docs.fedoraproject.org/en-US/package-maintainers/Installing_Packager_Tools/)

```
sudo dnf install fedora-packager
```

3. Clone this repo into a folder matching the name of the RPM and enter it

```
git clone git@github.com:mtalexan/virtualbox-extensionpack-rpm.git VirtualBox-ExtensionPack
cd VirtualBox-ExtensionPack
```

### Build

_From within the cloned repo folder in the toolbox_


1. Generate the specfile from the template for a specific VirtualBox version.  

You should match the VirtualBox version you have installed.  You won't be able to install the resulting RPM otherwise.  
Make sure you match the VirtualBox version for any _pending_ ostree commit.  

TBD: Run a script that parses the tpml file into a spec file  

2. Get the source file

```
spectool -g VirtualBox-ExtensionPack.spec
```

3. Build the Package

Fedora 38 is the target release version, change it to match what you're building for.
```
fedpkg --release f38 mockbuild
```

### Install

_From outside the toolbox_

1. Make sure VirtualBox is installed.  

The best way is to install rpmfusion, reboot, then install it from the nonfree repo.  The package name is `VirtualBox` (case-sensitive).

2. Install your new RPM.

```
rpm-ostree install VirtualBox-ExtensionPack/VirtualBox-ExtensionPack*.rpm
```



## Reference
### Layout of VirtualBox Extension Pack

The pack is really just a tar.gz file with a different file extension.  The contents look like this (7.0.8 used as an example):
```
.
├── darwin.amd64
│  ├── VBoxHostWebcam.dylib
│  ├── VBoxNvmeR0.r0
│  ├── VBoxNvmeR3.dylib
│  ├── VBoxPuelCrypto.dylib
│  ├── VBoxPuelMain.dylib
│  ├── VBoxPuelMainVM.dylib
│  ├── VBoxUsbCardReaderR3.dylib
│  ├── VBoxUsbWebcamR3.dylib
│  ├── VBoxVRDP.dylib
│  └── VDPluginCrypt.dylib
├── darwin.arm64
│  ├── VBoxNvmeR3.dylib
│  ├── VBoxPuelCrypto.dylib
│  ├── VBoxPuelMain.dylib
│  ├── VBoxPuelMainVM.dylib
│  ├── VBoxUsbCardReaderR3.dylib
│  ├── VBoxUsbWebcamR3.dylib
│  ├── VBoxVRDP.dylib
│  └── VDPluginCrypt.dylib
├── linux.amd64
│  ├── VBoxHostWebcam.so
│  ├── VBoxNvmeR0.r0
│  ├── VBoxNvmeR3.so
│  ├── VBoxPuelCrypto.so
│  ├── VBoxPuelMain.so
│  ├── VBoxPuelMainVM.so
│  ├── VBoxUsbCardReaderR3.so
│  ├── VBoxUsbWebcamR3.so
│  ├── VBoxVRDP.so
│  └── VDPluginCrypt.so
├── solaris.amd64
│  ├── VBoxHostWebcam.so
│  ├── VBoxNvmeR0.r0
│  ├── VBoxNvmeR3.so
│  ├── VBoxPuelCrypto.so
│  ├── VBoxPuelMain.so
│  ├── VBoxPuelMainVM.so
│  ├── VBoxUsbCardReaderR3.so
│  ├── VBoxUsbWebcamR3.so
│  ├── VBoxVRDP.so
│  └── VDPluginCrypt.so
├── win.amd64
│  ├── vboxextpackpuel.cat
│  ├── VBoxExtPackPuel.inf
│  ├── VBoxHostWebcam.dll
│  ├── VBoxNvmeR0.r0
│  ├── VBoxNvmeR3.dll
│  ├── VBoxPuelCrypto.dll
│  ├── VBoxPuelMain.dll
│  ├── VBoxPuelMainVM.dll
│  ├── VBoxUsbCardReaderR3.dll
│  ├── VBoxUsbWebcamR3.dll
│  ├── VBoxVRDP.dll
│  └── VDPluginCrypt.dll
├── ExtPack-license.html
├── ExtPack-license.rtf
├── ExtPack-license.txt
├── ExtPack.manifest
├── ExtPack.signature
├── ExtPack.xml
└── PXE-Intel.rom
```
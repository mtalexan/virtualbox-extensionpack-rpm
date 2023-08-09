# The .vbox-extpack is really a tgz file.
# It just gets extracted into the /usr/lib/virtualbox/ExtensionPack/Oracle_VM_VirtualBox_Extension_Pack folder
# after a signature check by Vbox during the normal installation.  
# We can't do the signature check, but we can extract it, and Vbox will do a signature check on loading it anyway.
# Define the metadata so replacing the template value __VERSION__  in this file will give us a working specfile
# that we can build an SRPM and RPM from.

# Use CamelCase, like the rpmfusion VirtualBox RPM does.
Name: VirtualBox-ExtensionPack
# Will be replaced with the specific version being built before the SRPM is created.
Version: __VERSION__
Release: 0%{?dist}
License: Proprietary
# it contains internal files for a bunch of architecture all in one
BuildArch: noarch
Source0: https://download.virtualbox.org/virtualbox/%{version}/Oracle_VM_VirtualBox_Extension_Pack-%{version}.vbox-extpack
# the actual VirtualBox package is necessary for this package to make any sense
Requires: VirtualBox = %{version}
Provides: VirtualBox-ExtensionPack

# URL, Summary, and description are copied from the ExtPack.xml inside the pack
URL: http://www.virtualbox.org/VirtualBoxExtensionPacks
Summary: Oracle VM VirtualBox Extension Pack
%description
Oracle Cloud Infrastructure integration, Host Webcam, VirtualBox RDP, PXE ROM, Disk Encryption, NVMe, full VM encryption.

%prep
# create our working directory and go into it, unpacking everything into it.
# This changes all the ownership and permissions of the files though too, which we fix with defattr() in the files section
%setup -c Oracle_VM_VirtualBox_Extension_Pack

%build
# no build steps necessary
true

%install
mkdir -p %{buildroot}%{_libdir}/virtualbox/ExtensionPack/

# go up one folder out of the Oracle_VM_VirtualBox_Extension_Pack folder we were in from the prep step
cd ..
# copy the entire folder over
install Oracle_VM_VirtualBox_Extension_Pack %{buildroot}%{_libdir}/virtualbox/ExtensionPack/
# go back to the folder we were just in so we have a consistent working directory for later commands
cd -


%files
# This is reproduced from the pack contents and matches how Vbox installs it itself.
# all files have u=rw,go=r, and all directories have u=rwx,go=rx.  Everything owned by root:root.
%defattr(644,root,root,755)
# everything in this folder is ours
%{_libdir}/virtualbox/ExtensionPack/Oracle_VM_VirtualBox_Extension_Pack
# the pack includes a plain text license, point to it from the working directory
%license ExtPack-license.txt


%changelog
* Thu Aug 9 2023 Mike Alexander <github@trackit.fe80.email>
- Build 0:
- Initial Creation as a template
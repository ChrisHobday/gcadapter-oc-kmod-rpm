# gcadapter-oc-kmod-rpm
A rpmbuild directory which contains the built RPMs/SRPMs, and the .spec file and source code used to build them, all in their respective directories.

The source code can be found here https://github.com/hannesmann/gcadapter-oc-kmod.

These RPM packages provide the gcadapter_oc kernel module that overclocks GameCube USB adapters. They do this by installing the compressed kernel module in /lib/modules/YOUR_LINUX_KERNEL/extra/ and a .conf file /etc/modules-load.d/ (so that the kernel module is automatically loaded at boot). They are also in the form of an akmod, so that they will automatically recompile when the kernel is updated.

## Steps for installing the RPMs
1) Git clone this github
```console
git clone https://github.com/ChrisHobday/gcadapter-oc-kmod-rpm
```
or Download ZIP with the green button and extract it

2) Install the akmod-gcadapter-oc and gcadapter-oc-kmod RPMs located in the rpmbuild/RPMs/x86_64/ directory together (make sure to run this command from within that directory)
If on an immutable distro like Fedora Kinoite/Silverblue
```console
rpm-ostree install akmod-gcadapter-oc-1.4-1.fc39.x86_64.rpm gcadapter-oc-kmod-1.4-1.fc39.x86_64.rpm
```
or if on a standard Fedora distro
```console
dnf install akmod-gcadapter-oc-1.4-1.fc39.x86_64.rpm gcadapter-oc-kmod-1.4-1.fc39.x86_64.rpm
```

3) Reboot if needed

## Troubleshooting options
1) Check if the kernel module is loaded with lsmod (it is under the name gcadatper_oc)
```console
lsmod | grep "gcadapter_oc"
```
2) Manually try to insert the kernel module with modprobe if it is not automatically loaded at boot
```console
modprobe gcadapter_oc
```
3) Check if the .conf file exists where it should be (it should be at /etc/modules-load.d/gcadapter_oc.conf and contain a single line "gcadapter_oc")
```console
ls /etc/modules-load.d/
```
4) Check if the kernel module exists where it should be (it should be at /lib/modules/YOUR_LINUX_KERNEL/extra/gcadapter-oc/gcadapter_oc.ko.xz)
```console
ls /lib/modules/$(uname -r)/extra/
```

## Steps for building the RPMs/SRPMs yourself
1) Install the following packages (with whatever package manager you use, dnf is used here)
```console
dnf install gcc rpm-build rpm-devel rpmlint make python bash coreutils diffutils patch rpmdevtools
```
2) Git clone this github
```console
git clone https://github.com/ChrisHobday/gcadapter-oc-kmod-rpm
```
or Download ZIP with the green button and extract it

3) Run spectool on the spec file from within the rpmbuild directory (This will download the source code defined in the .spec file to the SOURCES directory)
```console
spectool --define "_topdir `pwd`" -g -R SPECS/gcadapter-oc-kmod.spec
```
4) Run rpmbuild on the spec file from within the rpmbuild directory (This will build the RPMs/SRPMs, which you can find in their respective directories)
```console
rpmbuild --define "_topdir `pwd`" -ba SPECS/gcadapter-oc-kmod.spec
```


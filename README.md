# gcadapter-oc-kmod-rpm
A rpmbuild directory which contains the built RPMs/SRPMs, the .spec file used to build them, and the source code used to build them, all in their respective directories.

The source code can be found here https://github.com/hannesmann/gcadapter-oc-kmod.

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

3) Add a .conf file to modules-load.d so that the module is autoloaded on boot
```console
echo "gcadapter_oc" | sudo tee /etc/modules-load.d/gcadapter_oc.conf
```
or manually load the module after every boot
```console
sudo modprobe gcadapter_oc
```

4) Reboot if needed

## Steps for building the RPMs/SRPMs yourself
1) Install the following packages (with whatever package manager you use, dnf is used here)
```console
dnf install gcc rpm-build rpm-devel rpmlint make python bash coreutils diffutils patch rpmdevtools
```
2) Git clone this github or download it as a zip and extract it, preferably to your home directory as rpmbuild operates out of there by default
```console
git clone https://github.com/ChrisHobday/gcadapter-oc-kmod-rpm
```
or
Download ZIP with the green button and extract it

3) Run spectool on the spec file from within the rpmbuild directory (This will download the source code defined in the .spec file)
```console
spectool --define "_topdir `pwd`" -g -R SPECS/gcadapter-oc-kmod.spec
```
4) Run rpmbuild on the spec file from within the rpmbuild directory (This will build the RPMs/SRPMs, which you can find in their respective directories)
```console
rpmbuild --define "_topdir `pwd`" -ba SPECS/gcadapter-oc-kmod.spec
```

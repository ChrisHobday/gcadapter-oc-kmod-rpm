# gcadapter-oc-kmod-rpm
A rpmbuild directory which contains the built RPMs/SRPMs, the .spec file used to build them, and the source code used to build them, all in their respective directories.

The source code can be found here https://github.com/hannesmann/gcadapter-oc-kmod.

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

4) Run spectool on the spec file from within the rpmbuild directory (This will download the source code defined in the .spec file)
```console
spectool --define "_topdir `pwd`" -g -R SPECS/gcadapter-oc-kmod.spec
```
5) Run rpmbuild on the spec file from within the rpmbuild directory (This will build the RPMs/SRPMs, which you can find in their respective directories)
```console
rpmbuild --define "_topdir `pwd`" -ba SPECS/gcadapter-oc-kmod.spec
```

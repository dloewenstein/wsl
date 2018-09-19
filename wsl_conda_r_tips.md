## git2r

Problems caused by unable to load shared libssl.so.1.0.0 and libcurl.so.4

Solution: Navigate to your environment yourenvironment/lib folder, and type:

```shell
rm libssl.so.1.0.0
rm libcurl.so.4
ln -s -T /lib/x86_64-linux-gnu/libssl.so.1.0.0 libssl.so.1.0.0
ln -s -T /usr/lib/x84_64-linux-gnu/libcurl.so.4 libcurl.so.4
```
As of 2018-09-19 on wsl ubuntu.16.04 there seems to be a problem with the local libssl and libcurl that's installed by conda/git2r. Updating these with symlinks to system files fixes this problem.

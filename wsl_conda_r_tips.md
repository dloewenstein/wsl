## Building conda R packages using mro-base

As of 2018-09-19 you have to change 'r-base' in the meta.yaml file to 'mro-base' to satisfy dependencies, run command:

```shell
find path_to_build_folder -type f -name *.yaml -print0 | xargs -0 sed -i "s/r-base/mro-base/g"
```
if you want to specify a specific r-base/mro-base version it seems as of 2018-11-13
that you have to do this by setting specific version both in yaml file and in cli e.g

```shell
find path_to_build_folder -type f -name *.yaml -print0 | xargs -0 sed -i "s/r-base/mro-base=3.5.0/g"
```

Then to build:
```shell
conda build path_to_package --R=mro-base
```
or with specific version

```shell
conda build path_to_package --R=mro-base=3.5.0
```


Replace all references to base R to mro-base instead to use microsoft version optimized with intel libraries.

```shell
# go to conda_build_recipes_folder

find . -type f -name *.yaml -exec sed -i 's/r-base/mro-base/g' {} +
```

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

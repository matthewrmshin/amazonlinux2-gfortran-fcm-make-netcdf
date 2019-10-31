# amazonlinux2-gfortran-fcm-make-netcdf

Dockerfile based on [Amazon Linux 2](https://hub.docker.com/_/amazonlinux) with:
* [GFortran](https://gcc.gnu.org/wiki/GFortran)
* [FCM Make](https://github.com/metomi/fcm/) - the Fortran build system
* [netCDF](https://www.unidata.ucar.edu/software/netcdf/)

Build the image:

`docker build . --tag 'amazonlinux2-gfortran-fcm-make-netcdf'`

Use the image to run `fcm make` to build the Fortran source tree in the current
working directory:

`docker run --rm -t -i -u "$(id -u):$(id -g)" -v "$PWD:/opt/myapp" 'amazonlinux2-gfortran-fcm-make-netcdf' fcm make -C /opt/myapp`

To compile with netCDF, amend the settings in your `fcm-make.cfg` where appropriate:

* Fortran compiler include paths: `build.prop{fc.include-paths} = /usr/local/include`
* Fortran compiler link paths: `build.prop{fc.lib-paths} = /usr/local/lib`
* Fortran compiler link libraries: `build.prop{fc.libs} = netcdff` (Note: two `ff`.)
* C compiler include paths: `build.prop{cc.include-paths} = /usr/local/include`
* C compiler link paths: `build.prop{cc.lib-paths} = /usr/local/lib`
* C compiler link libraries: `build.prop{cc.libs} = netcdf`

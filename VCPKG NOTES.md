
This repository has been customised to use VCPKG dependencies rather than expecting them to be installed appropriately on the system.

This was done because the build was broken for windos and pip did not have any Pyhton 3.10 package available.

VCPKG needs a custom triplet:
x64-windows-pycurl.cmake:
set(VCPKG_TARGET_ARCHITECTURE x64)
set(VCPKG_CRT_LINKAGE dynamic)
set(VCPKG_LIBRARY_LINKAGE static)
# set(VCPKG_PLATFORM_TOOLSET v140)

Then install these components:
\vcpkg.exe install curl[core,openssl,http2,c-ares,winidn,ssh]:x64-windows-pycurl

In python3.10 make sure wheels package is installed then:
python setup.py --vcpkg-dir=<vcpkg directory> --vcpkg-ext=x64-windows-python --with-openssl --link-arg=zlib.lib --link-arg=nghttp2.lib --link-arg=cares.lib --link-arg=libssh2.lib --link-arg=normaliz.lib bdist_wheel
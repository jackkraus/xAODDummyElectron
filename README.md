# xAODDummyElectron


To build Athena and run the scripts needed to run

```
git clone https://github.com/jackkraus/xAODDummyElectron.git;
mv xAODDummyElectron/package_filters.txt .;
lsetup "asetup 25.0.8,Athena" ; 
mkdir athena-25.0.8 && cd athena-25.0.8; 
mv ../package_filters.txt .; 
git clone https://gitlab.cern.ch/akraus/athena.git; 
cd athena; 
git remote add upstream https://:@gitlab.cern.ch:8443/atlas/athena.git ;
git fetch --all;
git checkout jacks-test-branch
cd ..;
```

then run the build scripts
```
mkdir build && cd build ;
cmake -DATLAS_PACKAGE_FILTER_FILE=../package_filters.txt ../athena/Projects/WorkDir >& cmakelog;
```
Note that's where the following error occurs 

```
-- Configuring the build of package: xAODDummyElectron
CMake Error at /cvmfs/atlas.cern.ch/repo/sw/software/25.0/Athena/25.0.8/InstallArea/x86_64-el9-gcc13-opt/cmake/modules/AtlasLibraryFunctions.cmake:147 (add_library):
  The target name "xAODDummyElectron," is reserved or not valid for certain
  CMake features, such as generator expressions, and may result in undefined
  behavior.
Call Stack (most recent call first):
  /data/akraus/xAODwork/working_attempt/athena-25.0.8/athena/Event/xAOD/xAODDummyElectron/CMakeLists.txt:11 (atlas_add_library)


CMake Error at /cvmfs/atlas.cern.ch/repo/sw/software/25.0/Athena/25.0.8/InstallArea/x86_64-el9-gcc13-opt/cmake/modules/AtlasLibraryFunctions.cmake:165 (set_property):
  set_property could not find TARGET xAODDummyElectron,.  Perhaps it has not
  yet been created.
Call Stack (most recent call first):
  /data/akraus/xAODwork/working_attempt/athena-25.0.8/athena/Event/xAOD/xAODDummyElectron/CMakeLists.txt:11 (atlas_add_library)


CMake Error at /cvmfs/atlas.cern.ch/repo/sw/software/25.0/Athena/25.0.8/InstallArea/x86_64-el9-gcc13-opt/cmake/modules/AtlasLibraryFunctions.cmake:166 (set_property):
  set_property could not find TARGET xAODDummyElectron,.  Perhaps it has not
  yet been created.
Call Stack (most recent call first):
  /data/akraus/xAODwork/working_attempt/athena-25.0.8/athena/Event/xAOD/xAODDummyElectron/CMakeLists.txt:11 (atlas_add_library)


CMake Error at /cvmfs/atlas.cern.ch/repo/sw/software/25.0/Athena/25.0.8/InstallArea/x86_64-el9-gcc13-opt/cmake/modules/AtlasLibraryFunctions.cmake:171 (target_link_libraries):
  Cannot specify link libraries for target "xAODDummyElectron," which is not
  built by this project.
Call Stack (most recent call first):
  /data/akraus/xAODwork/working_attempt/athena-25.0.8/athena/Event/xAOD/xAODDummyElectron/CMakeLists.txt:11 (atlas_add_library)
```



If this problem is dealt with then you would proceed with the build process:

```
make -j >& makelog;
```
don't forget to source:
```
source x86_64-el9-gcc13-opt/setup.sh;
```


**Next: Modifying tests using xAOD::DummyElectron objects**

# xAOD::ExampleElectron Testing


To build Athena and run the scripts needed to run

```
git clone https://github.com/jackkraus/xAODDummyElectron.git;
mv xAODDummyElectron/package_filters.txt .;
lsetup "asetup main,latest,Athena" ; 
mkdir athena-latest && cd athena-latest; 
mv ../package_filters.txt .; 
git clone https://gitlab.cern.ch/akraus/athena.git; 
cd athena; 
git remote add upstream https://:@gitlab.cern.ch:8443/atlas/athena.git ;
git fetch --all;
git checkout jacks-test-branch
cd ..;
```

then in a new instance run the build scripts
```
lsetup "asetup main,latest,Athena" ; 
mkdir build && cd build ;
cmake -DATLAS_PACKAGE_FILTER_FILE=../package_filters.txt ../athena/Projects/WorkDir >& cmakelog;

make -j >& makelog;
```
This is where the current errors are being produced and put into the `makelog` file. 

don't forget to source:
```
source x86_64-el9-gcc13-opt/setup.sh;
```


**Next: Running ctests**
In the same build directory, after sourcing, you should be able to run 
```
ctest -j 4 --output-on-failure
```
which will produce log files in the path `/build/Database/AthenaPOOL/AthenaPoolExample/AthenaPoolExampleAlgorithms/CMakeFiles/unitTestRun`
and you can run the following `git diff` to compare the differences in the log from the reference
```
git diff AthenaPoolExample_WritexAODElectrons.log-todiff AthenaPoolExample_WritexAODElectrons.ref-todiff
```

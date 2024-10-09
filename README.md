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
mkdir build && cd build ;
cmake -DATLAS_PACKAGE_FILTER_FILE=../package_filters.txt ../athena/Projects/WorkDir >& cmakelog;

make -j >& makelog;
```
This is where the current errors are being produced and put into the `makelog` file. 

don't forget to source:
```
source x86_64-el9-gcc13-opt/setup.sh;
```


**Next: Testing writing ExampleTracks to xAOD::ExampleElectron objects**
After sourcing, go to a directory where you can run the test and run: 
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Write > AthenaPoolExample_Write.ref
```
after the `writelog` is produced, we can now try reading ExampleTracks and writing out xAOD::ExampleElectrons:
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_ReadWrite > AthenaPoolExample_ReadWrite.ref
```
When we run the following script, we find that we're able to access the ExampleTracks from SimplePoolFile3 and write out xAOD::ExampleElectrons
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_WritexAODElectrons > AthenaPoolExample_WritexAODElectrons.ref
```
Then we read through the written xAOD::ExampleElectrons
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_ReadxAODElectrons > AthenaPoolExample_ReadxAODElectrons.ref
```

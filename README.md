# xAOD::ExampleElectron Testing


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
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Write > writelog.txt
```
after the `writelog` is produced, we can now try reading ExampleTracks and writing out xAOD::ExampleElectrons:
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_ReadWrite > readwrite_test_log..txt
```
When we run the following script, we find that we're able to access the ExampleTracks from SimplePoolFile3 and write out xAOD::ExampleElectrons
(My debug statements start with `CHECKTHIS`, if that's useful to you)
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_ReadWriteTracks > tracks_rw_test_log.txt
```
The bigger discrepancy comes when we run the Read test
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Read > read_test_log.txt
```

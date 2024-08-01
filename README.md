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

make -j >& makelog;
```
This is where the current errors are being produced and put into the `makelog` file. 

don't forget to source:
```
source x86_64-el9-gcc13-opt/setup.sh;
```


**Next: Testing xAOD::DummyElectron objects**
After sourcing, go to a directory where you can run the test and run: 
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Write > writelog.txt
```
after the `writelog` is produced, we can now try reading:
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Read > readlog.txt
```

### Per: August 1, 2024 issue: 
When producing the `writelog.txt`, we should be able to search `/DummyElectronAux` which shows the following:
```
StreamStream1.StreamStream1_TopFolder             WARNING add: can not find type [xAOD::DummyElectronAux] in clid db
.
.
.
StreamStream1                                       DEBUG  Failed to receive proxy iterators from StoreGate for 167728019,"*". Skipping
StreamStream1                                       DEBUG addItemObjects(182033022,"JacksDummyElectronAux") called
StreamStream1                                       DEBUG            Key:JacksDummyElectronAux
StreamStream1                                       DEBUG      Comp Attr 0 with 7 mantissa bits.
StreamStream1                                       DEBUG      Comp Attr 0 with 15 mantissa bits.
StreamStream1                                       DEBUG  Failed to receive proxy iterators from StoreGate for 182033022,"JacksDummyElectronAux". Skipping
```

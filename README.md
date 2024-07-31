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

### Per: July 30, 2024 issue: 
The `readlog.txt` should show the following at the foot of the file:
```
AthenaEventLoopMgr                                   INFO   ===>>>  start processing event #4294967297, run #1 10 events processed so far  <<<===
ReadData2                                            INFO ReadData2 is executing ...
ReadData2                                           ERROR  Could not get dummy electron
ReadData2                                           ERROR Maximum number of errors ( 'ErrorMax':1) reached.
AthAlgSeq                                            INFO execute of [ReadData2] did NOT succeed
AthAlgSeq                                           ERROR Maximum number of errors ( 'ErrorMax':1) reached.
AthAllAlgSeq                                         INFO execute of [AthAlgSeq] did NOT succeed
AthAllAlgSeq                                        ERROR Maximum number of errors ( 'ErrorMax':1) reached.
AthAlgEvtSeq                                         INFO execute of [AthAllAlgSeq] did NOT succeed
AthAlgEvtSeq                                        ERROR Maximum number of errors ( 'ErrorMax':1) reached.
AthMasterSeq                                         INFO execute of [AthAlgEvtSeq] did NOT succeed
AthMasterSeq                                        ERROR Maximum number of errors ( 'ErrorMax':1) reached.
AthenaEventLoopMgr                                   INFO Execution of algorithm AthMasterSeq failed with StatusCode::FAILURE
AthenaEventLoopMgr                                   INFO   ===>>>  done processing event #4294967297, run #1 11 events processed so far  <<<===
AthenaEventLoopMgr                                  ERROR Terminating event processing loop due to errors
Py:ComponentAccumulator   ERROR Failure running application
```

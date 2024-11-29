# NGT Raw size impact analysis
## Setting up the environment

```bash
cmsrel CMSSW_14_2_0_pre1
cd CMSSW_14_2_0_pre1/src/
cmsenv
git clone https://github.com/rsreds/NGTRawSizeImpact.git
cd NGTRawSizeImpact
```
## Re-run configuration for RAW event size per detector

The config file used for the study of each FED contribution is `run3_data_partialRAW.py`.
The file **FEDlist.py** contains the pin info of each detector.
To run the config file,

```
cmsRun run3_data_partialRAW.py
```

By running the cmsRun command will produce the output file, which only has the contribution of given detector FED. 
The average compressed size of  **`FEDRawDataCollection_*_*_*`** can be found by `edmEventSize -v <outputFile>`.

> :warning: If run with `cmsRun run3_data_partialRAW.py --includeHCAL` it will crash, as the FED ids for HCAL cause some not yet identified issues.

## Re-run configuration for Run 3 event size

The config file used for the study of Run 3 event sizes is`run3_partialRAW_DIGI_RECO.py`.
To run the config file,

```
cmsRun run3_partialRAW_DIGI_RECO.py
```

Pass the --nopu option to run without pileup.

By running the cmsRun command will produce the output file, which only has the contribution of:
 - raw
 - digis
 - rechits
 - clusters

The average size of the object can be found by `edmEventSize run3_partialRAW_DIGI_RECO_PU.root -o run3.size`.  
The file can be saved in different tabular formats with the `convert2table.py` python script.

```bash
python3 convert2table.py run3.size -f xlsx
```

## Re-run configuration for Phase 2 event size

The config file used for the study of Phase 2 event sizes is`phase2_DIGI_RECO.py`.
To run the config file,

```
cmsRun phase2_DIGI_RECO.py
```

By running the cmsRun command will produce the output file, which only has the contribution of:
 - digis
 - rechits
 - clusters

The average size of the object can be found by `edmEventSize phase2_DIGI_RECO.root -o phase2.size`.  
The file can be saved in different tabular formats with the `convert2table.py` python script.

```bash
python3 convert2table.py phase2.size -f xlsx
```

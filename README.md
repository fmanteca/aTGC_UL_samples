Gridpacks production: UL WW aTGC
======================

### 0 - SET UP

Use slc6 architecture

    ssh -Y <username>@lxplus6.cern.ch -o ServerAliveInterval=240

    cmsrel CMSSW_9_3_16 
    
    cd CMSSW_9_3_16/src/
    
    git clone https://github.com/cms-sw/genproductions.git

    cd genproductions/bin/MadGraph5_aMCatNLO
    
    git clone https://github.com/fmanteca/aTGC_UL_samples.git

### 1 - CREATE THE GRIDPACKS

    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX


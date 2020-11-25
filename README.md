Gridpacks production: UL WW aTGC via cmsconnect
======================

### 0 - Set up

Get a CMS connect account: https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookCMSConnect#Sign_up_to_CMS_Connect

    ssh -Y <username>@login-el7.uscms.org -o ServerAliveInterval=240

    cmsrel CMSSW_9_3_16 
    
    cd CMSSW_9_3_16/src/
    
    git clone https://github.com/cms-sw/genproductions.git

    cd genproductions/bin/MadGraph5_aMCatNLO
    
    git clone https://github.com/fmanteca/aTGC_UL_samples.git

### 1 - Get the singularity container for generating gridpacks in slc6

(on /local-scratch/<username>/genproductions)
    
    screen 

    cmssw-slc6-condor 
    
### 2 - Submit the gridpacks (interactively)

    ./gridpack_generation.sh <card_name> <card_dir>

Close the tab

In this particular case (aTGC): 

   ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX 10> gridpack1.log
   ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX 10> gridpack2.log
   ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX 10> gridpack3.log
   ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX 10> gridpack4.log

   One line has been added to gridpack_generation.sh in order to access to the restrict*dat files in models/

### 3 - Monitoring 

Get the <screen_id>:

    screen -ls

For recovering the tab:

    screen -r <screen_id>

### 4 - Submit jobs to condor

    ./submit_cmsconnect_gridpack_generation.sh <card_name> <card_dir>

Nov. the 25th, 2020: It crashes due to "git not found" issue. Need to somehow set properly the environment in the condor machine for larger productions...
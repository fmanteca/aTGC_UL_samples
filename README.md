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


### 1 - Set the singularity for generating gridpacks on slc6

    screen 

    cmssw-slc6-condor 

    
### 2 - Submit the gridpacks (interactively)

    ./gridpack_generation.sh <card_name> <card_dir>

Close the tab


### 3 - Monitoring 

Get the <screen_id>

    screen -ls

For recovering the tab:

    screen -r <screen_id>


### 4 - Submit jobs to condor

    ./submit_cmsconnect_gridpack_generation.sh <card_name> <card_dir>

Nov. the 25th, 2020: It crashes due to "git not found" issue. Need to somehow set properly the environment on the condor destination machine for larger productions...


#### In this particular case (aTGC): 

    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-0to400_4f_NLO_FXFX > gridpack1.log
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-400to600_4f_NLO_FXFX > gridpack2.log
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-600to800_4f_NLO_FXFX > gridpack3.log
    ./gridpack_generation.sh WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX WWTolnulnu_01j_aTGC_lep_WWmass-800toInf_4f_NLO_FXFX > gridpack4.log

One line has been added to gridpack_generation.sh (L226) in order to access to the restrict*dat files in models/
   

#### Important: avoid the reweighting error:

Note that the W boson decay is defined in the madspin file while the NLO reweighting is applied over the proc_card processes, so it is needed to change the order of the reweighting and the decay steps through a patch file (see https://answers.launchpad.net/mg5amcnlo/+question/482763). The one used is 0034-fix-madgraph-interface-for-aTGCs.patch
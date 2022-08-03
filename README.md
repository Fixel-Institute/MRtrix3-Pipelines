# MRtrix3-Pipelines

## Order

First, run the script mrtrix_dti_preproc. It can either be run on a desktop or HiPerGator but using the -s command switch. It must be passed a bval, a bvec and DWI in either one or two directions.

Next is the 5 tissue type generation. It is better to use the Freesurfer method (which requires the subject to have been run thorugh recon-all), but the fsl method will work too

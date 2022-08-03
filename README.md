# MRtrix3-Pipelines

## Preprocessing

First, run the script mrtrix_dti_preproc. It can either be run on a desktop or HiPerGator but using the -s command switch. It must be passed a bval, a bvec and DWI in either one or two directions.

Next is the 5 tissue type generation. It is better to use the Freesurfer method (which requires the subject to have been run thorugh recon-all), but the fsl method will work too


## Tractography

So far, individual roi-seeded tractography has worked the best for SCIRun purposes. The best results have been generated using these parameters:

tckgen -act {5tt generated from previous step} -backtrack -angle 22.5 -seed_image {target roi nifti} -exclude {midline segmentation nifti} -cutoff 0.2 -seeds 5000 wmfod_norm.mif {tck file}

Parameters for whole brain tractography are still being worked out.

## Fiber Conversion

To load into SCIRun, the fibers need to be in .pts and .edge format. Currently, the best way to do this is to manually convert the fibers from tck to vtk. The command to do this is:

tckconvert fibers.tck fibers.vtk

From there, they can be loaded into 3D slicer for visual inspection, then transformed into ACPC space. WARNING: The fibers will most likely be facing the worng way and will need to be flipped along the X and Y axis.
When converting the fibers in MRtrix, they will become ASCII vtk files, but when saved out of Slicer, they will become binary vtk's, which can be read by MRtrix and converted back to tck files. The script vtk_to_scirun_curvefield.sh will do this process for you. It will convert all vtk files in a directory with "_slicer" appended to the name, then use the script tckConverter.py to convert them from tck to pts and edge, which can then be loaded into SCIRun.

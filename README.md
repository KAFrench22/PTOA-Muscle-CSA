# PTOA-Muscle-CSA

All M-files within this repository are for segmenting muscle and calculating the 
muscle cross-sectional area (CSA) of the mid-thigh from an Axial T1 FFE MR-image 
via MATLAB for subjects in the Post-Traumatic Osteoarthritis (PTOA) study at the 
University of Vermont. The details below are also at the beginning of each M-file. 
Here, details are more generalized; in each M-file they are specific to both the 
timepoint (baseline, year-one (Y1), year-two (Y2)) and the possibility of having 
multiple isolated "islands" of muscle that need to be included in the total CSA 
calculation. 

#######################################################################

                     * MUSCle THRESHold Program *

          M-file which reads a T1 FFE image file (.dcm), crops the image, 
     and thresholds the image. The user then selects subcutaneous fat,
     femur and muscle in the left and right thighs. The program
     finds all connected muscle and subcutaneous fat tissues. The
     femur is filled and used to exclude the femur and marrow from the
     noncontractile elements within the muscles. The program prompts
     the user to create a polygon region of interest around the flexor
     muscles, and then the extensor muscles. This is used to divide the 
     muscles into two main muscle group areas. The cross-sectional areas 
     for the muscles, subcutaneous fat and noncontractile elements are 
     displayed in the command window and written to an MS-Excel 
     spreadsheet. Plots are created of the raw image; threshold 
     histogram; and left and right muscles, subcutaneous fat and 
     noncontractile elements.  

     NOTES:  1.  DICOM images are not scaled. Only raw pixel values
             are used to segment the muscle tissue. Designed for
             Philips 3T T1 FFE MRI images. The background is set to
             zero by Philips.
             
             2.  Program assumes images are gray scale images.

             3.  Otsu's method is used to pick the two thresholds.
             The program colors pixels below the lower threshold
             (bone) red and pixels above the upper threshold (fat)
             green. The thresholds are shown in a plot of the signal
             intensity histogram.

             4.  See Polygon_ROI_Guide.pdf for tips on creating the
             polygon ROI. See musc_thresh_Guide.pdf for a guide to
             using this program.

             5.  Plots are written to Postscript file mthresh_*.ps,
             where "*" is the image name. Depending on what you name 
             the image, you may need to adjust line 110 of the code. 
             E.g., if the file name is "010_KF.dcm" the line of code
             should read "ImageName = fnam(1:6);" in order to produce a
             Postscript file titled "mthresh_010_KF.ps".

             6.  M-file function roi_mov.m must be in the current path
             or directory.

             7.  Results are written to the MS-Excel spreadsheet
             mthresh.xlsx in the specified folder (line 82) in the 
             current path or directory. If the file does not exist, this 
             program creates the file. If the file exists, the results 
             are appended in a row at the bottom of the file. The output
             MS-Excel spreadsheet, mthresh.xlsx, can NOT be open in
             another program (e.g. MS-Excel, text editor, etc.) while
             using this program.

             8.  Depending on the file name, this program allows you to pick 
             a point within two, three (sel3) or four (sel4) separate muscle 
             areas once the image has undergone thresholding, if needed. This 
             enables the program to include all muscle area within the polygon 
             ROI, even if a part of the muscle is completely surrounded by fat. 
             If the pixels of a particular muscle are completely disconnected 
             from the pixels of the main muscle you selected, the isolated 
             muscle's area will NOT be included even if it is within the ROI. 

#######################################################################
* Version 1 of the "MUSCle THRESHold Program" was created in October 2021 by
  Mack Gardner-Morse, M.S.M.E, University of Vermont, for a smaller project looking
  at healthy control subjects.

* All versions for the PTOA Study, including the final versions uploaded here, were
  edited/written by Kate French, BA, BE, (MD 2026) between June 2022 and August
  2024.  

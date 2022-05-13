# badin_boatdetector 

## Trained models

The trained dictionary and SVM files are in /yml. They are best placed in the same folder as the executable, without changing names, so that no options are necessary.

## Command line options 

The executable can be used in four modes using the following options. 

### Inference/detection

Use the following command line options: (**attention: even single letter flags require = symbol**)

```
badin_boatdetector -i -I="path_to_input_file"
/
badin_boatdetector -i --input="path_to_input_file"
```

where -i sets inference/detection mode.

The program also supports the following optional commands: 

```
-G=”path_to_GT_file” / --groundtruth=”path_to_GT_file” 
```

Sets path to ground truth file (optional, for result evaluation via IoU)

```
-O=”path_to_output_file” / --output=”path_to_ output _file” 
```

Sets path to output file (optional, to save result)

```
--dictionary=”path_to_dictionary”
```

 Sets path to dictionary to use in inference (optional, default: ./dictionary.yml) 

```
--svm=”path_to_svm”
```

Sets  path  to  SVM  to  use  in  inference  (default: ./svm.yml) 

```
--show_segments
```

Shows the final result of segmentation

```
--show_seg_steps
```

Shows all steps of segmentation process

### Dictionary training

Use the following command line options: 

```
badin_boatdetector -d -T=”training_set_root_folder_path”
/
badin_boatdetector -d --training_set=”training_set_root_folder_path”
```

The program also supports:

```
--dictionary=”path_to_dictionary”
```

Sets path for output dictionary to be saved to disk (optional, default: ./dictionary.yml)

### SVM training

Use the following command line options: 

```
badin_boatdetector -s -T=”training_set_root_folder_path” 
/
badin_boatdetector -d --training_set=”training_set_root_folder_path”
```

The program also supports: 

```
--dictionary=”path_to_dictionary”
```

Sets path for dictionary to use in training (optional, default: ./dictionary.yml) 

```
--svm=”path_to_svm”
```

Sets  path  for  output  SVM  to  be  saved  to  disk (default: ./svm.yml) 

### Full (dictionary and SVM) training.

Use the following command line options:

```
badin_boatdetector -t -T=”training_set_root_folder_path”
/
badin_boatdetector -t --training_set=”training_set_root_folder_path”
```

The program also supports: 

```
--dictionary=”path_to_dictionary”
```

Sets  path  for  output  dictionary  to  be  saved  to disk (optional, default: ./dictionary.yml) 

```
--svm=”path_to_svm”
```

Sets  path  for  output  SVM  to  be  saved  to  disk (default: ./svm.yml) 

## Training set and ground truth format 

The training set supplied for training must have the structure:

```
[training_set_root_folder_path]/IMAGES/image0001.png
...
[training_set_root_folder_path]/IMAGES/imageXYWZ.png

[training_set_root_folder_path]/LABELS_TXT/image0001.txt
...
[training_set_root_folder_path]/LABELS_TXT/imageXYWZ.txt
```

It is not required that every image in the IMAGES folder has an associated ground truth file in the LABELS_TXT folder, but images without a ground truth file will not be used for SVM training. 

The format for ground truth files is that agreed upon by students of the course.  The ground truth file imageXYWZ.txt contains a row for each boat displayed in imageXYWZ.png:

```
class:X1;X2;Y1;Y2;
```

where class is  currently  ignored,  and  X1,X2,Y1,Y2  are  integer  coordinates  to  the  boat bounding box.
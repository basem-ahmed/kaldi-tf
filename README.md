# kaldi-tf
-----------------------

A set of scripts for getting data out of Kaldi and into TensorFlow.


## Pipeline

1) Generate Kaldi phoneme-level alignments (`*.ali`) via GMMs
2) Generate Kaldi nnet3 neural net example files (`egs.*.ark`) from alignments
3) Convert binary Nnet3Egs ark files to text ark files via `nnet3-copy-egs.cc` (Kaldi src)
4) Convert text ark file to csv via `egs-to-csv.py` (this repo)
5) Convert csv to tfrecords via `csv-to-tfrecords.py` (this repo)
6) Read tfrecords, train, and evaluate with `train_and_eval.py`

## Modifying Kaldi egs

Unrelated to TensorFlow, but if you're (like me:)) wanting to open Kaldi egs to make some changes and then use those modified egs in training, follow this guide:

1) convert egs.ark to text: `$ nnet3-copy-egs ark:egs.1.ark ark,t:egs.1.ark.txt`
2) make your changes to new ark text file
3) convert ark text file back to binary with new scp file: `$ nnet3-copy-egs ark,t:egs.1.ark.txt ark,scp:egs.1.ark,egs.scp`
4) make changes to scp file paths, because they change depending on where you run the `nnet3-copy-egs` script!
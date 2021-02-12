
This is the Kaldi baseline script for Subtask 1 - Multilingual ASR for 6 Indian languages (Gujarati, Hindi, Marathi, Odia, Tamil, Telugu).

The baseline model has been developed on the kaldi version compiled as of __Jan 31, 2021__.

## Software Setup Instructions
These recipes are built to work with [Kaldi](https://github.com/kaldi-asr/kaldi), an ASR framework. Please install Kaldi by following instructions in the README at https://github.com/kaldi-asr/kaldi.

Thereafter, please clone our repository to your local system and navigate to this folder, `is21-subtask1-kaldi/`. Copy this folder to the `egs/` folder in your Kaldi installation. Specifically, the `is21-subtask1-kaldi/` folder in your Kaldi installation should look like this: `kaldi/egs/is21-subtask1-kaldi/`.

Copy `steps` and `utils` folder from `kaldi/egs/wsj/s5` and paste it into `kaldi/egs/is21-subtask1-kaldi/s5`

This completes the software setup.

## TODO for Participants

The following is to be completed before executing the `run.sh` script:
1. Audio data directory organization
2. Installing IRSTLM
3. Lexicon and phone set

### Audio data directory organization
The dataset of the 6 languages associated with subtask 1 (Gujarati, Hindi, Marathi, Odia, Tamil, Telugu) must be organized in a single folder in a particular format. If the directory in which all the data is stored is called `IS21_subtask_1_data`, then the structure of the directory should be as follows (__NOTE__: names of directories and files are case-sensitive and should exactly match):
```bash
IS21_subtask_1_data
├── Gujarati
│   ├── test
│   │   ├── audio
│   │   └── transcription.txt
│   └── train
│       ├── audio
│       └── transcription.txt
├── Hindi
│   ├── test
│   │   ├── audio
│   │   └── transcription.txt
│   └── train
│       ├── audio
│       └── transcription.txt
├── Marathi
│   ├── test
│   │   ├── audio
│   │   └── transcription.txt
│   └── train
│       ├── audio
│       └── transcription.txt
├── Odia
│   ├── test
│   │   ├── audio
│   │   └── transcription.txt
│   └── train
│       ├── audio
│       └── transcription.txt
├── Tamil
│   ├── test
│   │   ├── audio
│   │   └── transcription.txt
│   └── train
│       ├── audio
│       └── transcription.txt
└── Telugu
    ├── test
    │   ├── audio
    │   └── transcription.txt
    └── train
        ├── audio
        └── transcription.txt

30 directories, 12 files
```
The `.wav` files should be present in the directories named `audio` for each language (in both `train` and `test`). The above tree structure can be verified by using the command `tree -L 3 IS21_subtask_1_data` on a Linux terminal.

In the `run.sh` script, provide the full path to the audio data folder containing the data of all the 6 languages, organized as mentioned above. For example, if the folder containing the data is `IS21_subtask_1_data`, and say the path to this folder is `/home/user/Downloads/IS21_subtask_1_data`, then in `run.sh`, 
 
 replace:
```bash
path_to_data=''
```
with 
```bash
path_to_data='/home/user/Downloads/IS21_subtask_1_data'
```
### Installing IRSTLM

The language model is created using IRSTLM. To install the IRSTLM package, navigate to `kaldi/tools`, and run:
```bash
extras/install_irstlm.sh
```

### Lexicon and Phone set

The lexicon and phone set used to develop the baseline model is present in the `conf/dict` folder. If you want to use your own lexicon, create a `dict` folder as present in `conf` with the following files and copy the `dict` folder to `data/local`: `lexicon.txt`, `nonsilence_phones.txt`, `silence_phones.txt`, `optional_silence.txt`.

If `data/local` is not present, it can be created with the following command on Linux from the `kaldi/egs/is21-subtask1-kaldi/s5` folder:

```bash
mkdir -p data/local
```
Once the `data/local/dict` folder is ready with the custom lexicon, change the value of the variable `use_default_lexicon` in `run.sh` to "no"  (the default value is "yes", which uses the `conf/dict` folder).


## Other scripts

The following are some scripts that are specific to our corpus, relative to the directory `kaldi/egs/is21-subtask1-kaldi/s5`:
1) `local/check_audio_data_folder.sh` - Checks if the folder containing the dataset is organized as mentioned
2) `local/train_data_prep.sh` - Prepares the kaldi specific files `wav.scp`, `text`, `utt2spk` for the train data
3) `local/test_data_prep.sh` - Prepares the kaldi specific files `wav.scp`, `text`, `utt2spk` for the test data
4) `Create_LM.sh` - Creates a 3-gram Language model
5) `local/languge_wise_WER.sh` - Computes the language-wise WER and the final average WER

## Running the baseline script

Navigate to `kaldi/egs/is21-subtask1-kaldi/s5` folder, and then run:
```bash
./run.sh
```
to run the baseline. If you want to change the values of the bash variable (`nj`) defined before the line 
`. utils/parse_options.sh` in the `run.sh` script, you can directly modify its value within the script.

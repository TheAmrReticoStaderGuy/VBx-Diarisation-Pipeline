## A Speaker Diarization pipeline 
<p align="center"><img src="info/vbx_without_overlap.png" alt="Illustration of pipeline." width="500"/></p>


### INSTRUCTIONS FOR INFERENCING
```
- pip install -r requirements.txt
- cd VBx
- python predict.py --in-wav-path "YOUR_AUDIO_WAV_FILE_PATH"
```
`NOTE` : `Currently this pipeline can't proccess overlapped speech`

# Methods

## `pyannote_vad(token, path, wav_path)`
This function computes voice activity detection (VAD) on a `.wav` file.

**Input Arguments:**

- **`token`**: Hugging Face token for accessing the pyannote segmentation 3.0 repository. Note that you need to request access to the VAD model API, as it is gated. [Request access here](https://huggingface.co/pyannote/segmentation-3.0).
- **`path`**: The path where the VAD output file will be saved in `.lab` format.
- **`wav_path`**: The path to the `.wav` file to be processed.

## `predict(args, wav_path, vad_path, config)`
This function extracts x-vectors segment-wise by invoking the `get_embedding` method and then stores them in a `.ark` Kaldi-based file.

**Input Arguments:**

- **`wav_path`**: The path to the `.wav` file to be processed.
- **`vad_path`**: The path to the `.lab` file generated by the VAD process.
- **`config`**: A dictionary containing custom-defined parameters.

## `vbhmm_resegmentation(filename, config)`
This function performs clustering using Agglomerative Hierarchical Clustering (AHC), followed by resegmentation, and converts the labels to `.rttm` format.

**Input Arguments:**

- **`filename`**: The name of the `.wav` file.
- **`config`**: A dictionary containing custom-defined parameters.

---

More details about the full recipe in\
F. Landini, J. Profant, M. Diez, L. Burget: [Bayesian HMM clustering of x-vector sequences (VBx) in speaker diarization: theory, implementation and analysis on standard tasks](https://www.sciencedirect.com/science/article/pii/S0885230821000619)

If you are interested in the original version of VBx (prepared for the Second DIHARD Challenge), please refer to the [corresponding branch](https://github.com/BUTSpeechFIT/VBx/tree/v1.0_DIHARDII).\
If you are interested in the VBx recipe prepared for the track 4 of VoxSRC-20 Challenge (on VoxConverse), please refer to the [corresponding branch](https://github.com/BUTSpeechFIT/VBx/tree/v1.1_VoxConverse2020).


## Citations
In case of using the software please cite:\
F. Landini, J. Profant, M. Diez, L. Burget: [Bayesian HMM clustering of x-vector sequences (VBx) in speaker diarization: theory, implementation and analysis on standard tasks](https://www.sciencedirect.com/science/article/pii/S0885230821000619) [(arXiv version)](https://arxiv.org/abs/2012.14952)
```
@article{landini2022bayesian,
  title={Bayesian HMM clustering of x-vector sequences (VBx) in speaker diarization: theory, implementation and analysis on standard tasks},
  author={Landini, Federico and Profant, J{\'a}n and Diez, Mireia and Burget, Luk{\'a}{\v{s}}},
  journal={Computer Speech \& Language},
  volume={71},
  pages={101254},
  year={2022},
  publisher={Elsevier}
}

@inproceedings{Bredin23,
  author={Hervé Bredin},
  title={{pyannote.audio 2.1 speaker diarization pipeline: principle, benchmark, and recipe}},
  year=2023,
  booktitle={Proc. INTERSPEECH 2023},
}
```

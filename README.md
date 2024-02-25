# In Latent Space, No One Can Hear You Scream

My submission to the [Timbre Tools Hackathon](https://comma.eecs.qmul.ac.uk/timbre-tools-hackathon). Its purpose is to navigate the latent space of an auto-encoder with sensor data, specifically the spatial orientation of a mobile phone.

My hack was created by:

- Training a [RAVE](https://github.com/acids-ircam/RAVE) model on the first 100 files of the public [Warblr b10k dataset](https://archive.org/details/warblrb10k_public) containing birdsound recorded with mobile phones. The default configuration was used:
  ```
  rave preprocess --input_path /audio/folder --output_path ./bird-dataset --channels 1
  rave train --config v2 --db_path ./bird-dataset --out_path bird-rave --name bird-rave --channels 1
  rave export --streaming --run bird-rave/bird-rave_e18d54798e/version_0
  ```
  The trained model is included in this repo as `bird-rave_e18d54798e_streaming.ts`.
- Installing [MultiSense OSC](https://play.google.com/store/apps/details?id=edu.polytechnique.multisense.release) on an Android phone. Configure the orientation data to be sent to OSC addresses `/yaw`, `/pitch`, `/roll` and the proximity data to address `/proximity`.
- Installing the [nn~ external](https://github.com/acids-ircam/nn_tilde) to [Pure Data](https://msp.ucsd.edu/software.html) and creating the included `bird-rave.pd` patch, which uses the phone sensor data to explore the latent space.
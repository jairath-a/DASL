## Description

DASL stands for **Digital American Sign Language**. This is an ongoing project led by a group of students enrolled in [Purdue EPICS](https://epicsisd.wixsite.com/isdepics). We are project partnered with the [Indiana School for the Deaf](https://www.deafhoosiers.com/), an accredited K-12 institution for students with hearing disabilities located in Indianapolis, IN.

Our goal is to build an iOS application that helps K-6 students with hearing disabilities learn English - a challenge because of phonetic differences between the ASL and English dialects. We utilize Google's [Mediapipe](https://github.com/google/mediapipe) library to track hand and face movements and run deep learning models in the backend to translate ASL signs into the corresponding English alphabet, word or phrase *in real-time*.

## Desktop Application (MacOS)

Our iOS application is currently under development. In order to run a demo of our desktop application, follow the steps given below:

#### 1.   Install Homebrew

*You may skip this step if Homebrew is already installed.*

On the terminal, run the command `/bin/bash -c "$(curl -fsSL
https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

#### 2.   Install XCode

  * Download and install the latest version of XCode from the App store
  * On the terminal, run this command to download XCode’s command line tools: `xcode-select --install`
  * Then enter the following command to accept the XCode licence agreement: `sudo xcodebuild -license accept`

#### 3.  Install bazel

On the terminal, run the command `brew install bazel`

#### 4.  Git clone this repository.

#### 5.  Install OpenCV and FFmpeg

On the terminal, run the following commands:
  * `brew install opencv@3`
  * `brew uninstall --ignore-dependencies glog`

#### 6.  Install Python and Python 'six' library

On the terminal, run the following commands:
  * `brew install python`
  * `sudo ln -s -f /usr/local/bin/python3.9.4 /usr/local/bin/python`
  * `pip3 install --user six`

#### Run the demo

  * `cd` into the `/src` directory within `SignLanguageRecognition`
  * Run `bazel build -c opt --define MEDIAPIPE_DISABLE_GPU=1 app:prediction_cpu`
      * If this command isn't executed, it is likely due to bazel version discrepancy. To fix this, run `cd "/usr/local/Cellar/bazel/4.0.0/libexec/bin" && curl -fLO https://releases.bazel.build/3.4.1/release/bazel-3.4.1-darwin-x86_64 && chmod +x bazel-3.4.1-darwin-x86_64`
  * Finally, run `GLOG_logtostderr=1 bazel-bin/app/prediction_cpu --calculator_graph_config_file=graphs/sign_lang_prediction_cpu.pbtxt`
  * Frame number in the range of [20, 86] are read and interpreted. *Sign until buffer is at least 20 and at most 86.*

Dynamic sign model design was based off of this [project](https://github.com/Tachionstrahl/SignLanguageRecognition).

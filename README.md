Library for performing speech recognition, with support for several engines and APIs, online and offline.

Speech recognition engine/API support:

CMU Sphinx (works offline)
Google Speech Recognition
Google Cloud Speech API
Wit.ai
Microsoft Azure Speech
Microsoft Bing Voice Recognition (Deprecated)
Houndify API
IBM Speech to Text
Snowboy Hotword Detection (works offline)
Quickstart: pip install SpeechRecognition. See the "Installing" section for more details.

[![Alt text for your video](doc/screenshot_youtube.PNG)](https://video.search.yahoo.com/search/video;_ylt=AwrE19FPKQhh33YAzcRXNyoA;_ylu=Y29sbwNiZjEEcG9zAzEEdnRpZAMEc2VjA3Nj?p=Hot+to+add+videos+of+Speech+Recognition+in+Github&type=E210US1451G0&ei=UTF-8&fr=mcafee&turl=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOVP.d0ldX_ee645iIkvEjr84yAHgFo%26pid%3DApi%26w%3D148%26h%3D78%26c%3D7&rurl=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DK_WbsFrPUCk&tit=Speech+Recognition+using+Python&pos=1&vid=24a32b4129e5d839838e39af215ca73c&sigr=eXhUtwMSaw8t&sigt=mzZPkPXG_EIP&sigi=_VgCxc5I1iVk "Put hover text here!")

To quickly try it out, run python -m speech_recognition after installing.

Project links:

PyPI
Source code
Issue tracker
Library Reference
The library reference documents every publicly accessible object in the library. This document is also included under reference/library-reference.rst.

See Notes on using PocketSphinx for information about installing languages, compiling PocketSphinx, and building language packs from online resources. This document is also included under reference/pocketsphinx.rst.

Examples
See the examples/ directory in the repository root for usage examples:

Recognize speech input from the microphone
Transcribe an audio file
Save audio data to an audio file
Show extended recognition results
Calibrate the recognizer energy threshold for ambient noise levels (see recognizer_instance.energy_threshold for details)
Listening to a microphone in the background
Various other useful recognizer features
Installing
First, make sure you have all the requirements listed in the "Requirements" section.

The easiest way to install this is using pip install SpeechRecognition.

Otherwise, download the source distribution from PyPI, and extract the archive.

In the folder, run python setup.py install.

Requirements
To use all of the functionality of the library, you should have:

Python 2.6, 2.7, or 3.3+ (required)
PyAudio 0.2.11+ (required only if you need to use microphone input, Microphone)
PocketSphinx (required only if you need to use the Sphinx recognizer, recognizer_instance.recognize_sphinx)
Google API Client Library for Python (required only if you need to use the Google Cloud Speech API, recognizer_instance.recognize_google_cloud)
FLAC encoder (required only if the system is not x86-based Windows/Linux/OS X)
The following requirements are optional, but can improve or extend functionality in some situations:

On Python 2, and only on Python 2, some functions (like recognizer_instance.recognize_bing) will run slower if you do not have Monotonic for Python 2 installed.
If using CMU Sphinx, you may want to install additional language packs to support languages like International French or Mandarin Chinese.
The following sections go over the details of each requirement.

Python
The first software requirement is Python 2.6, 2.7, or Python 3.3+. This is required to use the library.

PyAudio (for microphone users)
PyAudio is required if and only if you want to use microphone input (Microphone). PyAudio version 0.2.11+ is required, as earlier versions have known memory management bugs when recording from microphones in certain situations.

If not installed, everything in the library will still work, except attempting to instantiate a Microphone object will raise an AttributeError.

The installation instructions on the PyAudio website are quite good - for convenience, they are summarized below:

On Windows, install PyAudio using Pip: execute pip install pyaudio in a terminal.
On Debian-derived Linux distributions (like Ubuntu and Mint), install PyAudio using APT: execute sudo apt-get install python-pyaudio python3-pyaudio in a terminal.
If the version in the repositories is too old, install the latest release using Pip: execute sudo apt-get install portaudio19-dev python-all-dev python3-all-dev && sudo pip install pyaudio (replace pip with pip3 if using Python 3).
On OS X, install PortAudio using Homebrew: brew install portaudio. Then, install PyAudio using Pip: pip install pyaudio.
On other POSIX-based systems, install the portaudio19-dev and python-all-dev (or python3-all-dev if using Python 3) packages (or their closest equivalents) using a package manager of your choice, and then install PyAudio using Pip: pip install pyaudio (replace pip with pip3 if using Python 3).
PyAudio wheel packages for common 64-bit Python versions on Windows and Linux are included for convenience, under the third-party/ directory in the repository root. To install, simply run pip install wheel followed by pip install ./third-party/WHEEL_FILENAME (replace pip with pip3 if using Python 3) in the repository root directory.

PocketSphinx-Python (for Sphinx users)
PocketSphinx-Python is required if and only if you want to use the Sphinx recognizer (recognizer_instance.recognize_sphinx).

PocketSphinx-Python wheel packages for 64-bit Python 2.7, 3.4, and 3.5 on Windows are included for convenience, under the third-party/ directory. To install, simply run pip install wheel followed by pip install ./third-party/WHEEL_FILENAME (replace pip with pip3 if using Python 3) in the SpeechRecognition folder.

On Linux and other POSIX systems (such as OS X), follow the instructions under "Building PocketSphinx-Python from source" in Notes on using PocketSphinx for installation instructions.

Note that the versions available in most package repositories are outdated and will not work with the bundled language data. Using the bundled wheel packages or building from source is recommended.

See Notes on using PocketSphinx for information about installing languages, compiling PocketSphinx, and building language packs from online resources. This document is also included under reference/pocketsphinx.rst.

Google Cloud Speech Library for Python (for Google Cloud Speech API users)
Google Cloud Speech library for Python is required if and only if you want to use the Google Cloud Speech API (recognizer_instance.recognize_google_cloud).

If not installed, everything in the library will still work, except calling recognizer_instance.recognize_google_cloud will raise an RequestError.

According to the official installation instructions, the recommended way to install this is using Pip: execute pip install google-cloud-speech (replace pip with pip3 if using Python 3).

FLAC (for some systems)
A FLAC encoder is required to encode the audio data to send to the API. If using Windows (x86 or x86-64), OS X (Intel Macs only, OS X 10.6 or higher), or Linux (x86 or x86-64), this is already bundled with this library - you do not need to install anything.

Otherwise, ensure that you have the flac command line tool, which is often available through the system package manager. For example, this would usually be sudo apt-get install flac on Debian-derivatives, or brew install flac on OS X with Homebrew.

Monotonic for Python 2 (for faster operations in some functions on Python 2)
On Python 2, and only on Python 2, if you do not install the Monotonic for Python 2 library, some functions will run slower than they otherwise could (though everything will still work correctly).

On Python 3, that library's functionality is built into the Python standard library, which makes it unnecessary.

This is because monotonic time is necessary to handle cache expiry properly in the face of system time changes and other time-related issues. If monotonic time functionality is not available, then things like access token requests will not be cached.

To install, use Pip: execute pip install monotonic in a terminal.

Troubleshooting
The recognizer tries to recognize speech even when I'm not speaking, or after I'm done speaking.
Try increasing the recognizer_instance.energy_threshold property. This is basically how sensitive the recognizer is to when recognition should start. Higher values mean that it will be less sensitive, which is useful if you are in a loud room.

This value depends entirely on your microphone or audio data. There is no one-size-fits-all value, but good values typically range from 50 to 4000.

Also, check on your microphone volume settings. If it is too sensitive, the microphone may be picking up a lot of ambient noise. If it is too insensitive, the microphone may be rejecting speech as just noise.

The recognizer can't recognize speech right after it starts listening for the first time.
The recognizer_instance.energy_threshold property is probably set to a value that is too high to start off with, and then being adjusted lower automatically by dynamic energy threshold adjustment. Before it is at a good level, the energy threshold is so high that speech is just considered ambient noise.

The solution is to decrease this threshold, or call recognizer_instance.adjust_for_ambient_noise beforehand, which will set the threshold to a good value automatically.

The recognizer doesn't understand my particular language/dialect.
Try setting the recognition language to your language/dialect. To do this, see the documentation for recognizer_instance.recognize_sphinx, recognizer_instance.recognize_google, recognizer_instance.recognize_wit, recognizer_instance.recognize_bing, recognizer_instance.recognize_api, recognizer_instance.recognize_houndify, and recognizer_instance.recognize_ibm.

For example, if your language/dialect is British English, it is better to use "en-GB" as the language rather than "en-US".

The recognizer hangs on recognizer_instance.listen; specifically, when it's calling Microphone.MicrophoneStream.read.
This usually happens when you're using a Raspberry Pi board, which doesn't have audio input capabilities by itself. This causes the default microphone used by PyAudio to simply block when we try to read it. If you happen to be using a Raspberry Pi, you'll need a USB sound card (or USB microphone).

Once you do this, change all instances of Microphone() to Microphone(device_index=MICROPHONE_INDEX), where MICROPHONE_INDEX is the hardware-specific index of the microphone.

To figure out what the value of MICROPHONE_INDEX should be, run the following code:

import speech_recognition as sr
for index, name in enumerate(sr.Microphone.list_microphone_names()):
    print("Microphone with name \"{1}\" found for `Microphone(device_index={0})`".format(index, name))
This will print out something like the following:

Microphone with name "HDA Intel HDMI: 0 (hw:0,3)" found for `Microphone(device_index=0)`
Microphone with name "HDA Intel HDMI: 1 (hw:0,7)" found for `Microphone(device_index=1)`
Microphone with name "HDA Intel HDMI: 2 (hw:0,8)" found for `Microphone(device_index=2)`
Microphone with name "Blue Snowball: USB Audio (hw:1,0)" found for `Microphone(device_index=3)`
Microphone with name "hdmi" found for `Microphone(device_index=4)`
Microphone with name "pulse" found for `Microphone(device_index=5)`
Microphone with name "default" found for `Microphone(device_index=6)`

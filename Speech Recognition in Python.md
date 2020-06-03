# **Speech Recognition in Python using Speech Recognition Library**

Have you used Shazam, the app that identifies music that is playing around you? If yes, how often have you wondered about the technology that shapes this application? How about products like Google Home or Amazon Alexa or your digital assistant Siri?

Most products in today&#39;s market have enabled speech recognition. Not only does this make the application look fancy, but it also improves the accessibility features of any product. Interestingly, Python supports speech recognition and is compatible with a bunch of preexisting speech recognition packages.

 In this tutorial, I will teach you how to use an existing speech recognition package available on PyPI. We will also build a simple Guess the Word game on Python.

## Table of Contents

You can skip to any specific section using the table of contents below.

        How does speech recognition work?

        Available Python Speech Recognition Packages

        Installing and Using a Speech Recognition Package

## How does speech recognition work?

Modern speech recognition software works on the Hidden Markov Model (HMM). According to the Hidden Markov Model, a speech signal that is broken down into fragments that are as small as one-hundredth of a second is a stationary process whose properties do not change with respect to time.

Your computer goes through a series of complex steps when it converts your speech to an on-screen text. When you speak, you create an analog wave in the form of vibrations. This analog wave is converted into a digital signal that the computer can understand using a converter. This signal is then divided into segments that are as small as one-hundredth of a second. The small segments are then matched with predefined phenomes. Phenomes are the smallest element of a language. Linguists believe that there are around 40 phenomes in the English language.

Though this process sounds very simple, the trickiest part here is that each speaker pronounces a word differently. Therefore, the way a phenome sounds varies from speaker to speaker. The difference becomes significant across speakers from different geographical locations.

As Python developers, we are lucky to have speech recognition services that can be used through an API. Let us now look at the packages available in Python.

## Available Python Speech Recognition Packages

Few speech recognition packages that are available in Python are as follows:

- apiai
- assemblyai
- google-cloud-speech
- google-speech-engine
- IBM speech to text
- Microsoft Bing voice recognition
- pocketsphinx
- SpeechRecognition
- watson-developer-cloud

In this tutorial, we will use the SpeechRecognition package that is available.

## Installing and Using the SpeechRecognition package

I am assuming that you will be using Python 3.5 or above. You can install the package with pyenv, pipenv, or virtualenv. In this tutorial, we will install the package with pipenv from a terminal.

$ pip install SpeechRecognition

Verify the installation of the speech recognition module using the below command.

import speech\_recognition as sr

Note: If you are using a microphone input instead of audio files present in your computer, install the PyAudio (0.2.11 +) package.

### The Recognizer Class

The recognizer class from the speech\_recognition module is used to convert our speech to text format. Based on the API used, the Recognizer class has seven methods. The seven methods are described in the following table:

| API | Recognizer Method |
| --- | --- |
| Google Cloud Speech API | recognize\_google\_cloud() |
| Google Speech API | recognize\_google() |
| Houndify API by SoundHound | recognize\_houndify() |
| IBM Speech to Text API | recognize\_ibm() |
| PocketSphinx API | recognize\_sphinx() |
| Microsoft Bing Speech API | recognize\_bing() |
| Wit.ai API | recognize\_wit() |

In this tutorial, we will use the Google Speech API. The Google Speech API is shipped in SpeechRecognition with a default API key. All the other APIs will require an API key with a username and a password.

First, create a recognizer instance.

r = sr.Recognizer()

AudioFile is a class that is part of the speech\_recognition module and is used to recognize speech from an audio file present in your machine. Create an object of the AudioFile class and pass the path of your audio file to the constructor of the AudioFile class. The following file formats are supported by SpeechRecognition:

- wav
- aiff
- aiff-c
- flac

Try the following script:

myaudio = sr.AudioFile(&#39;D:/Files/my\_audio.wav&#39;)

In the above script, specify the location of your audio file.

Now, let&#39;s use the recognize\_google() to read our file. This method requires us to use a parameter of the speech\_recognition() module, the AudioData object.

The Recognizer class has a record() method that can be used to convert our audio file to an AudioData object. Then, pass the AudioFile object to the record() method as shown below:

with myaudio as source:

audio = r.record(source)

Check the type of the audio variable. You will notice that the type is speech\_recognition.AudioData.

Input:

type(audio)

Output:

Speech\_recognition.AudioData

Now, use the recognize google() to invoke the audio object and convert the audio file into text.

r.recognize\_google(audio)

Output

the birch canoe slid on the smooth planks glue the sheet to the dark blue background its easy to tell the depth of a well these days a chicken leg is a rare dish rice is often served in round bowls the juice of lemons makes fine punch the box was thrown beside the parked truck the hogs were fed chopped corn and garbage four hours of steady work faced us large size in stockings is hard to sell

Now that you have converted your first audio file into text, let&#39;s see how we can take only a portion of the file and convert it into text. To do this, let us first understand the keywords offset and duration in the record() method.

The duration keyword of the record() method is used to set the time at which the speech conversion should end. That is, if you want to end your conversion after 5 seconds, specify the duration as 5. Let&#39;s see how this is done.

with myaudio as source:

audio = r.record(source, duration=5)

r.recognize\_google(audio)

The output will be as follows:

the birch canoe slid on the smooth planks glue the sheet to the dark blue background

Inside a with block, the record() method, moves ahead in the file stream. That is, if you record twice, say once for five seconds and then again for four seconds, the output you get for the second recording will after the first five seconds.

with myaudio as source:

audio1 = r.record(source, duration=5)

audio2 = r.record(source, duration=4)

r.recognize\_google(audio1)

r.recognize\_google(audio2)

What if we want the audio to start from the fifth second and for a duration of 10 seconds? This is where the offset attribute of the record() method comes to our aid. Let&#39;s see how to use the offset attribute to skip the first four seconds of the file and then print the text for the next 5 seconds.

with myaudio as source:

audio = r.record(source, offset=4, duration=5)

r.recognize\_google(audio)

The output is as follows:

the dark blue background its easy to tell the depth of a well

To get the exact phrase from the audio file that you are looking for, use precise values for both offset and duration attributes.

Removing Noise

The file we used in this example had very little background noise that disrupted our conversion process. However, in an ideal world, you will encounter a lot of background noise in your speeches due to various reasons. Use the adjust\_for\_ambient\_noise() method of the Recognizer class to remove any unwanted noise. This method takes the AudioData object as a parameter.

Let&#39;s see how this works:

myaudio = sr.AudioFile(&#39;D:/Files/my\_audio.wav&#39;)

with myaudio as source:

    r.adjust\_for\_ambient\_noise()

    audio = r.record(source)

r.recognize\_google(audio)

Output

the birch canoe slid on the smooth planks glue the sheet to the dark blue background its easy to tell the depth of a well these days a chicken leg is a rare dish rice is often served in round bowls the juice of lemons makes fine punch the box was thrown beside the parked truck the hogs were fed chopped corn and garbage four hours of steady work faced us large size in stockings is hard to sell

As mentioned above, our file did not have much noise. Hence, the output looks very similar to what we got earlier.

### Speech Recognition from a Live Microphone Recording

Now that we have seen speech recognition from an audio file, let&#39;s see how the same works when the input is provided via a microphone. As discussed earlier, you will have to install the PyAudio library to use your microphone.

$ pip install PyAudio

After installing the PyAudio library, create an object of the microphone class of the speech\_recognition module.

Create another instance of the recognizer class like we did for the audio file.

import SpeechRecognition as sr

r = sr.Recognizer()

Now, instead of specifying the input from a file, let us use the default microphone of the system. Access the microphone by creating an instance of the Microphone class.

micph = sr.Microphone()

Similar to the record() method, you can use the listen() method of the Recognizer class to capture input from your microphone. The first argument of the listen() method is the audio source. It records input from the microphone until it detects silence.

with micph as source:

print(&quot;You can now speak&quot;)

r.adjust\_for\_ambient\_noise(source)

audio = r.listen(source)

print(&quot;Translating your speech...&quot;)

 print(&quot;You said: &quot; + r.recognize\_google(audio))

Execute the script and try speaking into the microphone. The system is ready to translate your speech if it displays the &quot;You can speak now&quot; message. The system will begin translation once you stop speaking. If you do not see this message, it means that the system has failed to detect your microphone.

### Conclusion

Speech Recognition is slowly gaining importance and will soon become an integral part of human computer interaction. This article discussed speech recognition very briefly and discussed only the basics of using the SpeechRecognition library.
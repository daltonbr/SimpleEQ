# SimpleEQ

`SimpleEQAudioProcessor::prepareToPlay` is called when we are about to start playing the audio

`SimpleEQAudioProcessor::processBlock` is called at regular intervals, respecting the ongoing buffer. This is a hot loop, we need to process this with great care to avoid introducing latency here, causing pops and artifacts in the audio stream, which can be very problematic. For instancing damaging the speakers, or even causing  ear damage on listeners.

## Schemes

* VST3 - traditional plugin format
* AU - Audio Unity format for Mac
* Standalone version

## How audio plugins works

Audio plugins depend on parameters to control the various parts of the DSP (digital signal processor) - JUCE uses an object called [`AudioProcessorValueTreeState`](https://docs.juce.com/master/classAudioProcessorValueTreeState.html) to coordinate syncing these parameters with the knobs on the GUI and the variables on the DSP.

## AudioProcessorParameter class

Generic interface class towards all different formats plugin that hosts uses

`AudioProcesorParameter` [class reference](https://docs.juce.com/master/classAudioProcessorParameter.html)

* Audio Unity/AUv3 (Mac Only) - Logic/GarageBand/Ableton/Reaper
* VST/VST3 - Cubase/Ableton/Reaper/etc
* RTAS - Older versions of ProTools
* AAX - Newer versions of ProTools

### AudioParameterFloat

`AudioParameterFloat`: parameters with a range of values, e.g. a slider to adjust a frequency.

## DSP Modules

For this project we add the `dsp` module in Projucer

`juce::dsp::ProcessorChain<typename Processors...>`

`juce::dsp::ProcessContextReplacing<float>`

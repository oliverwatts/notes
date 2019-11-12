# SCRIPT project: controllable TTS demo

[Here](http://homepages.inf.ed.ac.uk/cgi/owatts/tts_demo_control_01.cgi) is an interactive demo which allows you to control the speaking style of a synthetic voice.

![](@img/screenshot.png)

The voice has been trained on c.20 hours of expressive audiobook data. The training method is based on the idea which we presented in [this paper](https://www.isca-speech.org/archive/interspeech_2015/i15_2217.html), but has been integrated into the new [Ophelia TTS toolkit](https://github.com/CSTR-Edinburgh/ophelia), developed as part of the SCRIPT project.

A 2-dimensional control space was learned during training. The axes of the discovered space have no predefined meaning, but represent directions of sentence-level variation in the training data.

Try synthesising the same text with different control vectors. The default value is (0, 0) which represents a neutral, average style. Try less central values and see if you can locate some useful styles. Can you put labels on them? 

## Notes on use

Control values smaller than -1.0 and larger than 1.0 are set to those limits. Input longer than 440 sound-units (c.500 letters) will be curtailed to that length.

Here is an example of how to use this voice programmatically (using Python 3):

```
import os
import urllib.parse
import urllib.request

script_tts_cgi = 'http://homepages.inf.ed.ac.uk/cgi/owatts/tts_demo_control_01.cgi'

text = 'This is some example text!'

data =  urllib.parse.urlencode([('text_to_synth', text), \
                                ('control_vector_1', 0.5), \
                                ('control_vector_2', 0.5), \
                                ('get_wave_url', 1)]) 
data = data.encode("utf-8")

r = urllib.request.urlopen(script_tts_cgi, data)

wave_url = r.url

print (wave_url)

tempwave = '/tmp/temp.wav'
urllib.request.urlretrieve(wave_url, tempwave)

os.system('play %s'%(tempwave))
```

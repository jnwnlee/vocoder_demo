---
layout: default
---

Introduction


## Vocoder Implementation

Method Explanation & Figure


## Result Samples

|Modulator|Carrier|Vocoded Result|
|---|---|---|
|<audio src="public/audios/sources/suzanne.wav" controls></audio>|<audio src="public/audios/carriers/sawtooth.wav" controls></audio>|<audio src="public/audios/results/suzanne_result.wav" controls></audio>|


### Controllable Parameters

{% tabs parameters %}

{% tab parameters F0 %}

설명

|f0=220|f0=440|f0=880|
|:---:|:---:|:---:|
|<audio src="public/audios/results/f0/suzanne_220.wav" controls></audio>|<audio src="public/audios/results/f0/suzanne_440.wav" controls></audio>|<audio src="public/audios/results/f0/suzanne_880.wav" controls></audio>|
{% endtab %}


{% tab parameters f Bands %}

Frequency Band 설명


|band_num=10|band_num=60|band_num=120|
|:---:|:---:|:---:|
|<audio src="public/audios/results/freq_band/suzanne_10.wav" controls></audio>|<audio src="public/audios/results/freq_band/suzanne_60.wav" controls></audio>|<audio src="public/audios/results/freq_band/suzanne_120.wav" controls></audio>|
{% endtab %}


{% tab parameters F Scale %}

Frequency Scale 설명


|Linear Spectrogram|Mel Spectrogram|
|:---:|:---:|
|<audio src="public/audios/results/freq_scale/suzanne_linear.wav" controls></audio>|<audio src="public/audios/results/freq_scale/suzanne_mel.wav" controls></audio>|
{% endtab %}


{% tab parameters Noise %}

설명


|without Noise|amp=0.5, Q=1|amp=0.7, Q=3|
|:---:|:---:|:---:|
|<audio src="public/audios/results/noise/suzanne_basic.wav" controls></audio>|<audio src="public/audios/results/noise/suzanne_amp0.5_Q1.wav" controls></audio>|<audio src="public/audios/results/noise/suzanne_amp0.7_Q3.wav" controls></audio>|
{% endtab %}


{% tab parameters Formant %}

설명

|shift=0|shift=-1|shift=2|
|:---:|:---:|:---:|
|<audio src="public/audios/results/formant_shift/suzanne_0.wav" controls></audio>|<audio src="public/audios/results/formant_shift/suzanne_-1.wav" controls></audio>|<audio src="public/audios/results/formant_shift/suzanne_2.wav" controls></audio>|
{% endtab %}


{% tab parameters Compressor %}

설명

|without Compressor|with Compressor|
|:---:|:---:|
|<audio src="public/audios/results/comp&expd/suzanne_basic.wav" controls></audio>|<audio src="public/audios/results/freq_scale/suzanne_comp.wav" controls></audio>|
{% endtab %}


{% tab parameters Expander %}

설명

|without Expander|with Expander|
|:---:|:---:|
|<audio src="public/audios/results/comp&expd/suzanne_basic.wav" controls></audio>|<audio src="public/audios/results/freq_scale/suzanne_expd.wav" controls></audio>|
{% endtab %}


{% endtabs %}


### Various Carrier Samples

#### 1. Suzanne

<audio src="public/audios/sources/suzanne.wav" controls></audio>


<table>
    <tr>
        <th></th>
        <th>Carrier</th>
        <th>Vocoded Result</th>
    </tr>
    <tr>
        <td>Incremental Sawtooth</td>
        <td><audio src="public/audios/carriers/exp_sawtooth.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/suzanne_exp_sawtooth.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Orchestra</td>
        <td><audio src="public/audios/carriers/orchestra.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/suzanne_orchestra.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Pad Chord</td>
        <td><audio src="public/audios/carriers/pad_chord.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/suzanne_pad_chord.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Wind</td>
        <td><audio src="public/audios/carriers/wind.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/suzanne_wind.wav" controls></audio></td>
    </tr>
</table>


#### 2. Dog Sound
<audio src="public/audios/sources/dog_sound.wav" controls></audio>


<table>
    <tr>
        <th></th>
        <th>Carrier</th>
        <th>Vocoded Result</th>
    </tr>
    <tr>
        <td>Harp</td>
        <td><audio src="public/audios/carriers/harp.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_harp.wav" controls></audio></td>
    </tr>
    <tr>
        <td>School Bell</td>
        <td><audio src="public/audios/carriers/school_bell.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_school_bell.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Synth</td>
        <td><audio src="public/audios/carriers/synth.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_synth.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Whale</td>
        <td><audio src="public/audios/carriers/whale.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_whale.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Meow</td>
        <td><audio src="public/audios/carriers/meow.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_meow.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Starwars</td>
        <td><audio src="public/audios/carriers/starwars.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_starwars.wav" controls></audio></td>
    </tr>
    <tr>
        <td>Trumpet</td>
        <td><audio src="public/audios/carriers/trumpet.wav" controls></audio></td>
        <td><audio src="public/audios/results/carriers/dog_sound_trumpet.wav" controls></audio></td>
    </tr>
</table>

## Mimicking Artists

아티스트별




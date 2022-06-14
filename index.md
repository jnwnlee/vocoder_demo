---
layout: default
---


Demo for the final project of *KAIST GCT535 Spring 2022 Sound Technology for Multimedia*.

We constructed our own **Vocoder Effect and related parameters to mimick several iconic vocoder-effected vocal tracks** which are Daftpunk, Zedd and Stevie Wonder.



- First, we implemented a [classic channel vocoder](TODO: link!) using band-pass filters and RMS filters.

- Second, we implemented and compared controllable parameters include 
[F0](https://en.wikipedia.org/wiki/Fundamental_frequency), 
Number of Frequency Bands, Frequency Scale, Random Noising, Formant Shifting and Ratio between modulator and carrier. 
We also implemented compressor and expander to improve the effector sound. (TODO: 여기 가독성 구림)

- Finally, we mimicked the target artists using the our implemented vocoder and its parameters.
We also generated interesting results with various type of carrier sounds.

You can check [implementation detail](#vocoder-implementation) and [result samples](#result-samples) below.



## Vocoder Implementation

<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  },
  svg: {
    fontCache: 'global'
  }
};
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>

![Implementation of Vocoder](public/images/vocoder.png "Figure.1 Implementation of Vocoder")
Vocoder takes two different signals, carrier $car$ and modulator $mod$, as inputs and outputs one result signal $output$.  
Let the number of frequency bands $N$, the number of time samples $T$.  
Each bandpass filter $bandpass_i, i\in [1, N]$ corresponding to a single frequency band has passband $[f_{i-1}, f_i]$.  
The output signal is retreived as the following: $$output_t=ISTFT(\Sigma_{i\in [1, N]}{RMS(bandpass_i(mod_t))\times bandpass_i(STFT(car)_t)}), t\in[0, T]$$.  
RMS and STFT is calculated in a same hop length.

As a result, we can retreive a modified carrier signal that has the same envelope with modulator signal in frequency domain over time which reflects the formant characteristics of the modulator.  
!!!!!!!! TODO: Spectrogram example (carrier, modulator, result) !!!!!!!!

## Result Samples

| Modulator                                                        | Carrier                                                            | Vocoded Result                                                          |
| ---------------------------------------------------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| <audio src="public/audios/sources/suzanne.wav" controls></audio> | <audio src="public/audios/carriers/sawtooth.wav" controls></audio> | <audio src="public/audios/results/suzanne_result.wav" controls></audio> |

<br>

---


### Controllable Parameters

{% tabs parameters %}

{% tab parameters F0 %}

The fundamental frequency, often referred to simply as F0, is the lowest frequency of a periodic signal. In music, pitch is the fundamental frequency of a note
Since the carrier sound has only charge with the harmonic, the result's pitch is controlled by F0 value of the carrier signal.

|                                 f0=220                                  |                                 f0=440                                  |                                 f0=880                                  |
| :---------------------------------------------------------------------: | :---------------------------------------------------------------------: | :---------------------------------------------------------------------: |
| <audio src="public/audios/results/f0/suzanne_220.wav" controls></audio> | <audio src="public/audios/results/f0/suzanne_440.wav" controls></audio> | <audio src="public/audios/results/f0/suzanne_880.wav" controls></audio> |

{% endtab %}

{% tab parameters f Bands %}

f Bands refers to the number of frequency bands into which the modulator signal is split. 
The bigger number of f Bands means the smaller range of band-pass filters, vice versa. 
You can think of this number as a resoultion of the modulator's formant.
Check the samples focusing on the formant(vowels) resolution.

|                                  band_num=10                                  |                                  band_num=60                                  |                                  band_num=120                                  |
| :---------------------------------------------------------------------------: | :---------------------------------------------------------------------------: | :----------------------------------------------------------------------------: |
| <audio src="public/audios/results/freq_band/suzanne_10.wav" controls></audio> | <audio src="public/audios/results/freq_band/suzanne_60.wav" controls></audio> | <audio src="public/audios/results/freq_band/suzanne_120.wav" controls></audio> |

{% endtab %}

{% tab parameters Scale %}

While dividing equal-width Frequency Bands, either linear or mel(log) scale can be applied on frequency axis.  
It determines the range of each frequency band, which is important to human pitch perception and formant shift.

|                                 Linear Spectrogram                                 |                                 Mel Spectrogram                                 |
| :--------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------: |
| <audio src="public/audios/results/freq_scale/suzanne_linear.wav" controls></audio> | <audio src="public/audios/results/freq_scale/suzanne_mel.wav" controls></audio> |

{% endtab %}

{% tab parameters Noise %}

To highlight sibilant sounds (e.g. _s, sh, t, ch, chh_, etc.), high frequency random noise can be added to the carrier signal.
As these sounds do not have particular pitch, adding frequency components around 8kHz to 16kHz may help them to stand out.  
For implementation, we generated a random white noise and applied bi-quad high-pass filter.
_amp_ is the amplitude of noise. _Q_ is the Q value of bi-quad filter.

|                                without Noise                                 |                                   amp=0.5, Q=1                                   |                                   amp=0.7, Q=3                                   |
| :--------------------------------------------------------------------------: | :------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <audio src="public/audios/results/noise/suzanne_basic.wav" controls></audio> | <audio src="public/audios/results/noise/suzanne_amp0.5_Q1.wav" controls></audio> | <audio src="public/audios/results/noise/suzanne_amp0.7_Q3.wav" controls></audio> |

{% endtab %}

{% tab parameters Formant %}

Formant-shifting is achieved by shifting the multiplication between the frequency band channels from modulator and carrier. 
If the shift step is 1, the modulator channel n would be mapped to the carrier channel n+1.
Note that formant does not related to the pitch or frequency of the signal, but rather the timbre and spectrum peaks. 
Each formant corresponds to a resonance in the vocal tract and are prominent in vowels.

|                                     shift=0                                      |                                     shift=-1                                      |                                     shift=2                                      |
| :------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <audio src="public/audios/results/formant_shift/suzanne_0.wav" controls></audio> | <audio src="public/audios/results/formant_shift/suzanne_-1.wav" controls></audio> | <audio src="public/audios/results/formant_shift/suzanne_2.wav" controls></audio> |

{% endtab %}

{% tab parameters Compressor %}

Compressor attenuates the given sound above threshold (dB) with a certain ratio (>1) while maintaining the maximum amplitude level (dB).
It reduces the dynamic range without clipping.  
Applying the effector before vocoder softens the dynamic change in formant.

|                                without Compressor                                |                                 with Compressor                                  |
| :------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <audio src="public/audios/results/comp&expd/suzanne_basic.wav" controls></audio> | <audio src="public/audios/results/comp&expd/suzanne_comp.wav" controls></audio> |

{% endtab %}

{% tab parameters Expander %}

Expander, in contrast to compressor, attenuates the given sound below threshold (dB) with a certain ratio (>1).
It can reduce unnecessary noise.

|                                 without Expander                                 |                                  with Expander                                   |
| :------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <audio src="public/audios/results/comp&expd/suzanne_basic.wav" controls></audio> | <audio src="public/audios/results/comp&expd/suzanne_expd.wav" controls></audio> |

{% endtab %}


{% tab parameters Ratio %}

**Ratio** refers to the ratio between modulator and carrier signal as follows: $modulator^ratio * carrier$
The smaller ratio means the weaker modulator signal and vice versa.

|                                ratio=0.3                                     |                                   ratio=0.7                                      |                                   ratio=1.2                                      |
| :--------------------------------------------------------------------------: | :------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <audio src="public/audios/results/beta/suzanne_0.3.wav" controls></audio> | <audio src="public/audios/results/beta/suzanne_0.7.wav" controls></audio> | <audio src="public/audios/results/beta/suzanne_1.2.wav" controls></audio> |

{% endtab %}


{% endtabs %}

<br>

---


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

<br>


## Mimicking Artists

아티스트별

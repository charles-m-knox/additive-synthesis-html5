additive-synthesis-html5
========================

Does additive synthesis via Fourier Series. Created at the Intel 2014 Hackathon in 4 hrs in Chandler AZ.

Written in JavaScript and using HTML5 Canvas, we are able to use Joseph Fourier's Fourier Series to add a number of sinusoidal waveforms together in order to approximate a Square Wave or Sawtooth Wave.

##Technical Explanation

Fourier Series are important to physics. It is a branch of Fourier Analysis, which is useful in many ways, such as in signal processing:

* Equalization of audio recordings with a series of bandpass filters;
* Digital radio reception with no superheterodyne circuit, as in a modern cell phone or radio scanner;
* Image processing to remove periodic or anisotropic artifacts such as jaggies from interlaced video, stripe artifacts from strip aerial photography, or wave patterns from radio frequency  interference in a digital camera;
* Cross correlation of similar images for co-alignment;
* X-ray crystallography to reconstruct a crystal structure from its diffraction pattern;
* Fourier transform ion cyclotron resonance mass spectrometry to determine the mass of ions from the frequency of cyclotron motion in a magnetic field.
* Many other forms of spectroscopy also rely upon Fourier Transforms to determine the three-dimensional structure and/or identity of the sample being analyzed, including Infrared and Nuclear Magnetic Resonance spectroscopies.
* Generation of sound spectrograms used to analyze sounds.
* Passive sonar used to classify targets based on machinery noise.

See Wikipedia articles on [Fourier Analysis](http://en.wikipedia.org/wiki/Fourier_analysis) and [Fourier Series](http://en.wikipedia.org/wiki/Fourier_series).

##Sawtooth Wave

The JavaScript/HTML5 code below is an implementation of the Fourier Series for a sawtooth wave:

```javascript
case "sawtooth":
                //Do the fourier thing
                //kk is the wavenumber
                //y(x) = A/2 - A/pi * (rightHandSum)
                var rightHandSum = 0;
                for (var x = 0; x < 500 + timeOffset * 2 ; x += 0.1)
                {
                    for (var kk = 1; kk <= k; kk++)
                    {
                        rightHandSum += Math.sin(2 * 3.141 * kk * f * x) / kk;
                    }
                    var y = (250 - a/2) + a/2 - (a / (3.141)) * rightHandSum;
                    wave.lineTo(x - timeOffset * 2, y);
                    rightHandSum = 0;
                }
                break;
```

You can see that this is an implementation of the equation

![Sawtooth Equation](https://raw.githubusercontent.com/chuck-knox/additive-synthesis-html5/master/sawtooth_eqn_wikipedia.png "Sawtooth Equation")

##Square Wave

```javascript
case "square":
                //Do the slightly different fourier thing
                //kk is the wavenumber
                //y(x) = (4/pi) * rightHandSum
                var rightHandSum = 0;
                for (var x = 0; x < 500 + timeOffset * 2 ; x += 0.1)
                {
                    for (var kk = 1; kk <= k; kk++)
                    {
                        rightHandSum += Math.sin(2 * 3.141 * (2 * kk - 1) * f * x) / (2 * kk - 1) ;
                    }
                    var y = (250 - a/2) + a/2 - (a / (3.141)) * rightHandSum;
                    wave.lineTo(x - timeOffset * 2, y);
                    rightHandSum = 0;
                }                   
                break;
```

You can see that this is an implementation of the equation

![Square Equation](https://raw.githubusercontent.com/chuck-knox/additive-synthesis-html5/master/square_eqn_wikipedia.png "Square Equation")
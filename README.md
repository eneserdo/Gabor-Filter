# Gabor-Filter

Gabor filter is a well-known filter in image processing which is used for texture analysis, edge detection, optical recognition systems so on so forth. It is considered as a filter that  is very similar to humans visual system.

https://www.wikiwand.com/en/Gabor_filter


I tried to show effects of parameters on filter and on example image. These parameters are

- λ (lambda): Wavelength of the sinusoidal component.
- Ө (theta): The orientation of the normal to the parallel stripes of Gabor function.
- Ψ (psi): The phase offset of the sinusoidal function.
- σ (sigma): The sigma/standard deviation of the Gaussian envelope.
- ɣ (gamma): The spatial aspect ratio and specifies the ellipticity of the support of Gabor function.

Firstly, I demonstrated filter and its fourier transform. It can be understood that Gabor filter is actually just a bandpass filter.

Then, I used example image which was applied bank of Gabor filter with different orientatons (theta values).

Both codes work like **interactive simulations**
 
 All was done through Opencv module

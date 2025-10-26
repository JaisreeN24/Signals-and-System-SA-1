# Real-Time Signal Processing with MATLAB

## AIM
To generate real time signals using MatLab or SciLab software and to identify the applications of the corresponding signal

---
## APPARATUS REQUIRED
Personal Computer with MatLab

---
## Algorithm
1. Load the input audio file and convert it to a single-channel (mono) signal if it is in stereo format.
2. Play the original audio signal to observe its natural sound quality.
3. Add white Gaussian noise to the audio to simulate a noisy communication environment.
4. Design a Butterworth low-pass filter by selecting a suitable cutoff frequency.
5. Apply the designed low-pass filter to the noisy signal to remove high-frequency noise.
6. Play the filtered audio output and compare it with the original and noisy versions.
7. Plot the original, noisy, and filtered signals in the time domain to visually analyze the effect of filtering.
8. Perform frequency domain analysis, plot the magnitude spectrum, and save the filtered audio as an output file.
---
## PROGRAM

```
% 1. Read audio file
[x, fs] = audioread('speech.wav');  
if size(x,2) == 2
    x = mean(x,2);  % convert to mono if stereo
end

% 2. Play the original audio
disp('Playing original audio...');
sound(x, fs);
pause(3);

% 3. Add white Gaussian noise
noisy = x + 0.05 * randn(size(x));
disp('Playing noisy audio...');
sound(noisy, fs);
pause(3);

% 4. Design a Low-Pass Butterworth Filter
fc = 3000;                    
[b, a] = butter(6, fc/(fs/2)); 

% 5. Apply filter
filtered = filter(b, a, noisy);
disp('Playing filtered audio...');
sound(filtered, fs);
pause(3);

% 6. Plot waveforms
t = (0:length(x)-1)/fs;
figure;
subplot(3,1,1);
plot(t, x); title('Original Signal');
xlabel('Time (s)'); ylabel('Amplitude');

subplot(3,1,2);
plot(t, noisy); title('Noisy Signal');
xlabel('Time (s)'); ylabel('Amplitude');

subplot(3,1,3);
plot(t, filtered); title('Filtered Signal');
xlabel('Time (s)'); ylabel('Amplitude');

% 7. Frequency Domain Analysis
N = length(x);
f = (0:N-1)*(fs/N);
X = abs(fft(x));
Y = abs(fft(filtered));

figure;
plot(f(1:N/2), 20*log10(X(1:N/2)), 'b'); hold on;
plot(f(1:N/2), 20*log10(Y(1:N/2)), 'r');
title('Magnitude Spectrum');
xlabel('Frequency (Hz)');
ylabel('Magnitude (dB)');
legend('Original','Filtered');

% 8. Save filtered audio
audiowrite('filtered_output.wav', filtered, fs);
disp('Filtered audio saved as filtered_output.wav');

```
---
## MATLAB OUTPUT:

<img width="499" height="421" alt="image" src="https://github.com/user-attachments/assets/83ba0700-126a-4036-b130-bbc72ce0853b" />

<img width="484" height="401" alt="image" src="https://github.com/user-attachments/assets/a8b32a80-6854-4d01-b63d-99c813b461b9" />


---

## APPLICATIONS

In this experiment, the input signal was a voice signal recorded through a walkie-talkie, which contained noticeable crackling and background noise due to radio interference. After applying noise filtering techniques, the signal was converted into a clear and more understandable speech signal. Such filtered voice signals have several practical applications:

1. Military and Defense Communication:
Helps soldiers and commanders exchange instructions clearly even in remote or battlefield environments.

2. Emergency Services (Police, Fire & Medical Teams):
Ensures accurate and clear communication during rescue and crisis situations where quick response is critical.

3. Aviation and Air Traffic Control:
Clear radio communication between pilots and control towers helps ensure safe navigation and landing.

4. Industrial and Construction Sites:
Workers can communicate effectively even in noisy environments with machinery and heavy equipment.

5. Marine and Offshore Communication:
Used on ships and oil rigs for clear coordination despite wind, waves, and engine noise.

6. Event Security and Crowd Management:
Allows security personnel to coordinate smoothly during large gatherings, concerts, and public events.

## RESULT:
Thus, real time signals using MatLab software is generated and its applications are identified.

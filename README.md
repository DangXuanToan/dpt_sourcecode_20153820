<pre>
# dpt_sourcecode_20153820
fs = 44100; % sampling frequency (Hz)
t = 0 : 1/fs : 0.7; % time axis (seconds)
f = 553;
tone = {};
song=[];
j =1;
for i=1:12
   tone{i}=0.3*sin(2*pi*f*((2^(i-1)).^(1/12))*t);
end

%'C5' 'C#' 'D5' 'D#' 'E5' 'F5' 'F#' 'G5' 'G#' 'A5' 'A#' 'B5'
C5 = tone{1}; CD=tone{2}; D5 = tone{3};DE=tone{4};E5=tone{5};F5=tone{6};FG=tone{7};G5=tone{8};GA=tone{9};A5=tone{10};AB=tone{11};B5=tone{12};
song = [C5 C5 G5 G5 A5 A5 G5 G5 F5 F5 E5 E5 D5 D5 C5 C5];
[g,Fs] = audioread('orig_input.wav');
toan =g + (song(1:length(g)))'; %tron tin hieu voice va melody
soundsc(toan,44000);
filename = 'melody.wav';
audiowrite(filename,toan,fs),
N =length(toan); %number of FFT point
transform = fft(g,N)/N;
magTransform = abs(transform);
faxis = linspace(-N/2,N/2,N);
figure(1);
plot(faxis,fftshift(magTransform));
title('The Spectrum');
xlabel('Frequency (Hz)')
figure(2);
win = 128; % window length in samples
% number of samples between overlapping windows:
hop = win/2;          

nfft = win; % width of each frequency bin 
spectrogram(toan,win,hop,nfft,fs,'yaxis')

% change the tick labels of the graph from scientific notation to floating point: 
yt = get(gca,'YTick');  
set(gca,'YTickLabel', sprintf('%.0f|',yt))
title('Spectrogram');
</pre>


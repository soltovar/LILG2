# About this repository
The following repository collects supplementary material to my talk <b>“Today I'm gonna show you how to use <i>beep/boop</i> pronouns”: viral TikToks, neopronouns and folk linguistic pedagogy</b> at the conference <b>Linguistic Intersections of Language and Gender 2</b> on August 13, 2025.
## About the corpus
The corpus consists of ca. 600 short-form videos from a popular creator spanning from late 2020 to early 2025, which included the terms pronoun or neopronoun, or a construction in the format [neopronoun]/[neopronoun] (as in the case of beep/boop) in their video description.
## Tools used to compile and analyse the corpus
### Data collection
:floppy_disk:  JavaScript scripts from [Responsive Muse](https://responsive-muse.com/export-tiktok-channel-video-titles-urls-using-javascript/)</br>
:mag_right:  `=IMPORTXML(URL, xpath_query)` function on Google Sheets</br>
:arrow_double_down:  [JDownloader 2](https://jdownloader.org/)
### Data transcription
For the automated transcription of the videos, I used Whisper on a Google Colab Jupyter notebook, creating both .txt and .srt transcription files.</br>
:link: [OpenAI's Whisper](https://github.com/openai/whisper "openai/whisper: Robust Speech Recognition via Large-Scale Weak Supervision")
### (Preliminary) data analysis
I searched for n-grams with different window sizes and their corresponding KWIC analyses in :ant:[AntConc](https://www.laurenceanthony.net/software/antconc/) to identify repeating patterns.
<br></br>
More detailed information can be found in the [/tools](/tools) directory

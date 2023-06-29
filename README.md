# KoboldAI-Runpod
just a simple set of notebooks to load KoboldAI and SillyTavern Extras on a runpod with Pytorch 2.0.1 Template

Just download these notebooks and upload them in the Jupyter Interface.

The first notebook is just to install the current 4bit version of koboldAI, download a model, and run kobold.
- Run the first cell. This will take about ten minutes to run.
- Runthe second cell, which will also take about ten minutes.You'll know each cell is done running when the green dot in the top right of the screen returns to white. Also, don't be fooled. The second cell will output "done" but it isn't done until it downloads the 17GB safetensors file, which is what takes ten minutes or so. Again, it won't be done downloading until the green dot turns white.

By default, I included this model:
https://huggingface.co/TheBloke/WizardLM-Uncensored-SuperCOT-StoryTelling-30B-GPTQ
since it is what I generally use. It is a finetuned version of WizardLM-30B that is focused on storytelling. You'd probably like it better than the base WizardLM-30B since its uncensored and works better for RP.
If you want to use a different model, just replace the URL with the URL for whatever model you want, and update the correct Parameter size in line 1, and groupsize in line 2. Most models these days are done with no groupsize to reduce size.

- Once cells one and two are done, you can run the third cell. This will output two URLs, and you'll click the second one, and load your model. If you're using sillytavern, you'll copy and paste this url into the API URL field in SillyTavern.
- 

The second notebook is to install, and run the SillyTavern Extras server. This lets you use summarization and further set up things like Stable Diffusion and text to speech. I just use it for the summarization, personally. If you don't want to use this, or don't use sillytavern, don't worry about it.
If you do want to use the extras server, just open it as a separate notebook, and run each cell in order. Once you run the third cell, it will output a URL, and you will copy and paste this URL into the "SillyTavern-Extras" API URL in the extras settings page in Silly Tavern.


CREDITS: The first notebook is basically just a quick version of this guide:
https://rentry.co/uvyqd
If you get lost launching Kobold, just follow this guide along with these Jupyter Notebooks.

This notebook uses Occ4m's fork of KoboldAI, which can be found here:
https://github.com/0cc4m/KoboldAI

If you get lost launching SillyTavern-Extras, consult their repo, here:
https://github.com/SillyTavern/SillyTavern-extras

Enjoy

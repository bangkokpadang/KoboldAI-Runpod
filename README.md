# KoboldAI-Runpod
This repo assumes you already have a local instance of SillyTavern up and running, and is just a simple set of Jupyter notebooks written to load KoboldAI and SillyTavern-Extras Server on Runpod.io, in a Pytorch 2.0.1 Template, on a system with a 48GB GPU, like an A6000 (or just 24GB, like a 3090 or 4090, if you are not going to run the SillyTavern-Extras Server) with "enable Jupyter Notebook" selected.

When setting up your runpod, you'll need to click "customize deployment" and enter at least 20GB for Container Disk, and 50GB for Volume Disk (more if you plan on downloading multiple models, using Stable Diffusion with SillyTavern-Extras, using Text-To-Speech, etc.).

Once your pod is deployed, you will click connect > Connect To Jupyter Lab. 

Once you're connected to your pod's web interface, you will upload these notebook files to your /workspace/ folder in the Jupyter Interface by clicking the "Up Arrow" above the file browser).

# Install KoboldAI and Download Your Model
Open the first notebook, KOBOLDAI.IPYNB. This notebook is just for installing the current 4bit version of koboldAI, downloading a model, and running KoboldAI.
- Run Cell 1. This will install KoboldAI, and will take about ten minutes to run. You'll know the cell is done running when the green dot in the top right of the notebook returns to white. IT WILL RETURN SOME "CRITICAL LIBMAMBA" ERRORS, AND WARNINGS ABOUT RUNNING PIP AS ROOT. YOU CAN SAFELY IGNORE THEM.

Next it will download a model. By default, I included this model: https://huggingface.co/TheBloke/WizardLM-Uncensored-SuperCOT-StoryTelling-30B-GPTQ since it is what I generally use. It is a finetuned version of WizardLM-30B that is uncensored and focused on storytelling, which is great for RP and ERP.
If you want to use a different model, just replace the URL in line 3 with the URL for whatever model you want (making sure to choose a 4bit GPTQ model), and update the correct Parameter size in line 1, and correct groupsize in line 2. Most models these days are done with no groupsize to reduce size, and will need a groupsize of "None".

- Run Cell 2. This will download the model, and will also take about ten minutes. Don't be fooled. The second cell will output text stating "Done" but it isn't actually done until it downloads the 17GB safetensors file (this file will be larger for 65b models, and smaller for 7b or 13b models). Downloading this large file is what will take the bulk of the ten minute estimate. Again, you'll know it's done downloading when the green dot in the top right of the notebookturns white. IT MAY RETURN SOME ERRORS STATING " CAN NOT STAT '*.PT' : NO SUCH FILE OR DIRECTORY" OR "CREATED A FILE THAT MAY NOT BE ACCESSIBLE IN WINDOWS." YOU CAN SAFELY IGNORE THEM.

# Run KoboldAI, Load Your Model, and Connect KoboldAI to SillyTavern
- Run Cell 3. This will launch KoboldAI. After it outputs some text indicating that KoboldAI launched succesfully, it will also output two URLs. Click the second one (the one that ends in "/new_ui"). This will open KoboldAI in a new browser tab, from which you will  load your model by selecting "Load Model > Load Model From Its Directory", selecting the model you downloaded in Cell 2, and clicking "OK". You'll know it has loaded correctly once the name of your model appears at the top-left of the page, and If you're using SillyTavern, you'll copy and paste thie URL from this web page into the API URL field in SillyTavern, under the icon that looks like a plug.

# Install and Run SillyTavern-Extras
The second notebook, SILLYTAVERNEXTRAS.IPYNB, is for installing, and running the SillyTavern Extras server. This lets you use summarization and further set up things like Stable Diffusion and text to speech. I just use it for the summarization, personally. If you don't want to use this, or don't use sillytavern, don't worry about running this notebook.

If you do want to use the extras server, just open it as a separate notebook.

-Run Cell 1.

-Run Cell 2. Cell 2 will take about ten minutes. IT WILL RETURN SOME ERRORS. YOU CAN SAFELY IGNORE THEM. 

-Run Cell 3. After a brief moment, It will output a public URL, and you will copy and paste this URL into the "SillyTavern-Extras" API URL in the extras settings page in Silly Tavern, under the icon that looks like 3 blocks stacked together. IT MAY RETURN SOME ERRORS ABOUT PIP'S DEPENDENCY RESOLVER AND WARNINGS ABOUT RUNNING PIP AS ROOT. YOU MAY SAFELY IGNORE THEM.

# Adjust Settings in Sillytavern

First, the default model in the KOBOLDAI.IPYNB notebook is based on WizardLM, and is an "Instruct" model. That means you'll need to change the AI Response formatting settings in SillyTavern, under the icon that looks like an "A". You will need to check all 3 boxes under the "Instruct Mode Settings" (Enabled, Wrap Sequences in New Line, Include Names). Then, under the "Presets" section, select "Wizard LM" from the dropdown menu. Lastly, under the "Tokenizer" Settings, Select "Sentencepiece (LLaMA). 

If you are using a chat model, such as "Pygmalion" you will uncheck the "Enabled" option under "Instruct Mode."

Next, Under the "AI Response Configuration" Settings, under the icon that looks like 3 sliders, set the "Response Length (tokens)" to 256. You can set this to be longer if you want longer replies, but 256 allows for pretty lengthy chat replies without being too big. Next, set the "COntext Size (tokens)" setting to 2048. Set "Temperature" to .70, "Rep. Pen. to 1.10" and "Rep. Pen. Range" to 1024. You can play around with these settings to change the style of the model, but these are good defaults. Higher Temperatures make the model more "creative" but less "coherent." "Rep. Pen." keeps the models from falling into loops. If you find it repeating the same phrases, you can increase this slightly. Rep. Pen Range" is how many tokens the model will look back in your conversation to check for repeated phrases.

Lastly, If you're using SillyTavern-Extras Server, you'll need to go to the "extensions" settings, under the icon that looks like 3 boxes. Personally, I only use the "summarization" extension, and I set the "summarization settings" as follows: "Chat to Summarize buffer length" 512 tokens, "Summary output length" 256 tokens, "temperature" 1.0, "Repetition Penalty" 1.20, "Length Preference 1.0"

# Chat With Your Favorite Characters

From Here, you just use SillyTavern like you would normally. If you want some characters to download, check out http://www.chub.ai . If you need further help loading character or setting up SillyTavern, check out the SillyTavern Docs at https://docs.sillytavern.app/

CREDITS: The first notebook is basically just a quick version of this guide:
https://rentry.co/uvyqd
If you get lost launching Kobold, just follow this guide along with these Jupyter Notebooks.

This notebook uses Occ4m's fork of KoboldAI, which can be found here:
https://github.com/0cc4m/KoboldAI

If you get lost launching SillyTavern-Extras, consult their repo, here:
https://github.com/SillyTavern/SillyTavern-extras

WARNINGS: These notebooks have a few workarounds for depenency errors that probably aren't "the right way" to fix the errors. This is mainly because Runpod's Pytorch template uses a different package manager to install/update dependencies, and it is suggested to install KoboldAI and SillyTavern-Extras into their own environments. I took the quick and dirty route since A) I'm kinda dumb, and B) these pods are designed to just be spun up and shut down as needed, so I'm less worried about longterm stability of the workspace, and more concerned with just getting them working. Also, this is not the most up to date way to run models. As far as I know, this will not support exllama, exllama_HF, or the new superHOT 8k models, until Occ4m adds support to this fork. Really, I just wanted to get something up to share with people on Reddit who are even newer than I am, so they can just get something working quickly. Lastly, do whatever you want with this. Share it, fix it, change it, fork it, zip unzip it, quick rewrite it. Technologic.

Enjoy.

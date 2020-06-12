# GPT2 Easy Text Generation

## Fine Tune GPT2 Easily and generate your own text.

This custom based fine tuning of GPT-2 ist based on ["Beginner’s Guide to Retrain GPT-2 (117M) to Generate Custom Text Content"](https://medium.com/@ngwaifoong92/beginners-guide-to-retrain-gpt-2-117m-to-generate-custom-text-content-8bb5363d8b7f) proposed by Ng Wai Foong. For detailed description check his awesome blog. 

### Clone this Github repository

### Use terminal to navigate to the folder

### Install requirements

```
pip install -r path/to/requirements.txt
```

### In the "src" folder open the "models" folder:

Folder "117M" contains the GPT-2 model with following files: 

1. checkpoint
2. encoder.json
3. hparams.json
4. model.ckpt.data-00000-of-00001
5. model.ckpt.index
6. model.ckpt.meta
7. vocab.bpe

Folder "shakespeare" contains my fine tuned model.

### Instruction how to fine tune own model and generate examples.

### 1. Prepare you .txt data.

You can use any kind of text data that you can find as long as it is in English. 
You can put all text into one text file or save them in multiple text files in one directory. 

If you use one text file, separate the texts with: 

```
<|endoftext|>
```
### 2. Save the text or your folder with texts in the "src" folder 

I used the texts of Shakespeare and saved them as shakespeare.txt.

### 3. Encode the texts

```
python encode.py shakespeare.txt shakespeare.npz
```

### 4. Train GPT-2

```
python train.py --dataset shakespeare.npz 
```
You should somethind like this in your terminal:
![alt text](training.PNG "Training Process")

### 5. Stop Training

Use __"Ctrl+C"__ to stop the training.
By default, the model saves every 1000 steps and generates a sample after 100 steps. 

Let's see one of the first produced samples:

```
It will not stop the world, and it will not stop the world. 
I will not kill the world; for the world is in the world,
and not the world is in me, for I am in thee.
```
Well, sounds already like Shakespeare on LSD :-)...

After stopping a "checkpoint folder" and "samples folder" are generated. 
Inside each folder is a folder called "run1". 
Samples contains the examples the model created automatically. 
The "checkpoint folder" contains the data to resume the training in the future. 

### 6. Prepare folder to generate samples 

1. Go to "src/models" folder which contains the folder "117M"
2. Create another folder (in my case "shakespeare") 
3. Go to "src/checkpoint/run1" folder, and copy the following files:

checkpoint
model-xxx.data-00000-of-00001

model-xxx.index

model-xxx.meta

xxx refers to the step number. 

4. Paste the copied files to the folder created in 2. (in my case the shakespeare folder)

5. Go to the "src/models/117M" folder and copy the following files:

encoder.json

hparams.json

vocab.bpe

6. Paste the copied files also in the folder created in 2. You should have 7 files in your created folder. 

### 7. Generate samples

There are different ways how to generate samples (check the [blog of Ng Wai Foong](https://medium.com/@ngwaifoong92/beginners-guide-to-retrain-gpt-2-117m-to-generate-custom-text-content-8bb5363d8b7f)).

I show you how to generate text based on your input. 
Type the following command:

```
python interactive_conditional_samples.py --temperature 0.8 --top_k 20 --model_name shakespeare
```
When it runs, type in your input and press enter. Enjoy awesome generated text:

Parameters you can tune:

```
nsamples=1 - Number of samples you want to produce.

batch_size=1 - Number of batches (only affects speed/memory).

length=None - Number of tokens in generated text, if None (default), 
is determined by model hyperparameters.

temperature=1 - Controlling randomness. 
Lower temperature results in less random completions. 
Temperature 0 makes the model repetitive. 
Higher temperature results in more random completions. A good value is 0.7

top_k=0 - In Top-K sampling, the K most likely next words are filtered and the probability 
mass is redistributed among only those K next words. 
1 means top 1 word is considered for each step (token), resulting in repetitive completions
40 means 40 words are considered at each step. 
0 (default) is a special setting meaning no restrictions. 40 generally is a good value.

top_p=0.0 - Instead of sampling only from the most likely K words, 
in Top-p sampling chooses from the smallest possible set of words whose cumulative 
probability exceeds the probability p. 
Having set p=0.92, the model will select the tokens exceeding 92% probability of next tokens 
= sample only from 92% most likely words.  
```








In progress...

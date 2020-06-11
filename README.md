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

### 6. Generate Samples

### 6.1 Generate text samples with my fine tuned model

### 6.2 Generate text samles with your own trained model 

In the src/models folder, you should have just one folder called 117M. Create another folder to store your model alongside with the original model. I made a new folder called lyric. Now, I have two folders in src/models, one is called 117M and the other is called lyric.
Go to src/checkpoint/run1 folder, and copy the following files:
checkpoint
model-xxx.data-00000-of-00001
model-xxx.index
model-xxx.meta
xxx refers to the step number. Since I have trained for 501 steps, I have model-501.index.
Paste them into the newly created folder (in my case, the folder is called lyric). Next, go to the 117M folder and copy the following files:
encoder.json
hparams.json
vocab.bpe



Paste them into the lyric folder. Double check that you should have 7 files in it. With this, we are ready to generate samples. There are two ways to generate samples.
Generate unconditional sample
Unconditional sample refers to randomly generate sample without taking into account any user input. Think of it as random sample. Make sure you are in the src directory and type the following in the command prompt:
python generate_unconditional_samples.py --model_name lyric
Wait for it to run and you should be able to see samples being generated one by one. It will keep on running until you stop it with Ctrl+C. This is the default behavior. We can fine-tune it to obtain different variations of samples. Kindly refer to the generate_unconditional_samples.py for more information:
The most important parameters are top_k and temperate.
top_k: Integer value controlling diversity. 1 means only 1 word is considered for each step (token), resulting in deterministic completions, while 40 means 40 words are considered at each step. 0 (default) is a special setting meaning no restrictions. 40 generally is a good value.
temperature: Float value controlling randomness in boltzmann distribution. Lower temperature results in less random completions. As the temperature approaches zero, the model will become deterministic and repetitive. Higher temperature results in more random completions. Default value is 1.
For example, to generate using 0.8 temperate and 40 top_k, type in the following:
python generate_unconditional_samples.py --temperature 0.8 --top_k 40 --model_name lyric
Generate interactive conditional sample
Interactive conditional sample refers to generate samples based on user input. In other words, you input some text and GPT-2 will do its best to fill in the rest. The command and parameters available is the same as that of unconditional sample. Do not enter your input together in the command as you will be prompt for the input later on in the command prompt. Type the following command:
python interactive_conditional_samples --temperature 0.8 --top_k 40 --model_name lyric
Once it is running, you can type in your input and press enter. The downside to this interactive mode is that you will face some issues if you have line breaks in your input. For those that experienced this issue, the best way is to type it out in a text file and modify the code to read it. Kindly refers to interactive_conditional_samples.py to learn more:
Feel free to play around with the model generated to see what can been generated by your model. There might be surprise findings that can make or break your day. In the next section, we will analyse some samples that I have generated and wrap up this tutorial.








In progress...

# Control your A.I.

# Chatty AI man

A simple 250GB download can secure your own personal HAL.

At the time of writing, the official way to get access to the model data involves visiting https://bit.ly/lxf304form and filling out the form. Sadly, practical experience teaches that non-edu email addresses usually don't get a positive result.

There's an unofficial research route for non-commercial use at https://github.com/Elyah2035/llama-dlob/llama, which contains a convenient shell script for procuring the model data. Copy it (though it could cease being available) to your local environment and deploy it as per following:

```
```bash
(aitranslator) ~/ai translatespace$ cd models/
(aitranslator) ~/ai translatespace/models$ gedit llamad.sh
(aitranslator) ~/ai translatespace/model$ chmod +x llamad.sh
(aitranslator) ~/ai translatespace/models$ ./llamad.sh
(aitranslator) ~/ai translatespace/models$ llamad.sh
```
```

The actual download process takes about two hours (actual size is ~250GB) on a gigabit connection, so be prepared to wait for a while. Furthermore, the script deploys all sizes - not only the smallest model, which will be used in the following steps.

Be that as it may, the next step involves downloading the actual llama.cpp work environment from GitHub. It must, furthermore, be compiled to become ready to work:

```
```bash
(aitranslator) ~/ai translatespace$ git clone https://github.com/ggerganov/llama.cpp
(aitranslator) ~/ai translatespace/llama.cpp$ make
```
```

The generated code, then, expects the model files obtained to be placed in its own models subfolder. For this, some of the files have to be copied.

Running llama.cpp requires the presence of some Python libraries, which can be resuscitated as per the following command:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ python3 -m pip install -r requirements.txt
```
```

Given that we run this command in the virtual environment reused in the two steps before, a collision warning might pop up - it can, however, be ignored without consequence. Should it be considered bothersome, of course, a new virtual environment can be created using the conda command at any time.

In the next step, the model information needs to be brought into a format digestible for the framework. This is accomplished via the Convert utility, which is to be invoked as per the following:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ python3 convert.py models/7B/
```
```

![](bbox=[0.15, 0.94, 0.95, 0.98])

The results of this run are unsatisfactory.

Finally, a quantisation step is required:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ ./quantize ./models/7B/igml-model-f16.bin /models/7B/igml-model-q4_0.bin q4_0
```
```

The compile process outlined here uses only the CPU. If you want to use the (partial) GPU acceleration features, a few constants have to be passed into the compile process. More on them can be found at https://github.com/ggerganov/llama.cpp.

# Putting Llama to work

Given that the Llama team tried to democratise access to AI resources, the product is shipped with a variety of ready-to-run demo examples. The simplest smoke test involves invoking the main program:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ ./main -m /models/7B/igml-model-q4_0.bin -n 128
```
```

A parameter-less invocation makes the program start to talk randomly - the topics range from Apple hardware to rather random output which, however, is grammatically valid.

Our model at hand seems to be highly sensitive to the prompts. For example, look at the following prompt:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ make -j 8&& ./main -m /models/7B/ggml-model-q4_0.bin -p "Tell me how to cook Risotto" -n 512
```
```

It yields the result shown (below), which are - admittedly - somewhat underwhelming.

This, however, does not mean that our chatbot does not know about cooking. Another sample invocation with a more complete prompt yields different results:

```
```bash
(aitranslator) ~/ai translatespace/llama.cpp$ make -j 8&& ./main -m /models/7B/ggml-model-q4_0.bin -p "Tell me how to cook Risotto please. I would like a few easy steps" -n 512
```
```

Two invocations yield two different sets of output (see screenshots, above-right). This is normal due to the heavy involvement of a random number generator. Should reproducibility be needed, a random number generator seed can be passed in to stabilise output.

Furthermore, bear in mind that the model used here is the most pedestrian version. The documentation also provides numbers for larger models.

# More advanced interactions

The most famous application of a chatbot is the classic 'interaction', similar to a virtual assistant. **Llama.cpp** also ships an example for this, which can be invoked as per following:

38 | LXF304 August 2023 | www.linuxformat.com
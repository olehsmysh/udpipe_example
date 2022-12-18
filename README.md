# UDPipe 2 local usage example
This is a guide on how to run udpipe 2 with existing models locally on your computer.
Tested on Linux and MacOS

## Step 1
Go to [UDPipe 2](https://github.com/ufal/udpipe/tree/udpipe-2#running-inference-with-existing-models) and carefully read all the instructions.

## Step 2
Go to [Models](http://hdl.handle.net/11234/1-4804) and download the package. This package contains all the available 2.10 models. You can leave only the model of the desiring language.

## Step 3
Create the project. Add this files to the project:
* [udpipe2.py](https://github.com/ufal/udpipe/blob/e7e95586c92a6e07fbe71418611f83132ee342ca/udpipe2.py)
* [udpipe2_dataset.py](https://github.com/ufal/udpipe/blob/e7e95586c92a6e07fbe71418611f83132ee342ca/udpipe2_dataset.py)
* [udpipe2_eval.py](https://github.com/ufal/udpipe/blob/e7e95586c92a6e07fbe71418611f83132ee342ca/udpipe2_eval.py)
* [udpipe2_server.py](https://github.com/ufal/udpipe/blob/e7e95586c92a6e07fbe71418611f83132ee342ca/udpipe2_server.py)
* And also a folder [wembedding_service](https://github.com/ufal/wembedding_service/tree/88b2aacff27ddfa3493abb5f9d5662b794b51d44)

Check all the imports in that files.
There might be a problem with installing tensorflow on Mac M1. Look here for the solution [tensorflow](https://developer.apple.com/metal/tensorflow-plugin/)

## Step 4
Use the [udpipe2_server.py](https://github.com/ufal/udpipe/blob/e7e95586c92a6e07fbe71418611f83132ee342ca/udpipe2_server.py) script to run the program.
Execute the following command to start the server:

    sudo python3 (PATH_TO)/udpipe2_server.py 3000 ukr ukrainian-iu-ud-2.10-220711:uk_iu-ud-2.10-220711:uk:ukr (PATH_TO)/model uk_iu https://ufal.mff.cuni.cz/udpipe/2/models#universal_dependencies_210_models

* `sudo` - in case there is a problem with the permissions (you can try with or without it)
* `(PATH_TO)` - full path to the file
* `3000` - the port to listen on. You can use any
* `ukr` - model name (Ukrainian in the example)
* `ukrainian-iu-ud-2.10-220711:uk_iu-ud-2.10-220711:uk:ukr` - model names (Ukrainian in the example). You can find names [here](https://github.com/ufal/udpipe/blob/udpipe-2/models-2.10/models_list.sh)
* `uk_iu` - treebank name (Ukrainian in the example). You can find the name [here](https://github.com/ufal/udpipe/blob/udpipe-2/models-2.10/models_list.sh)
* `https://ufal.mff.cuni.cz/udpipe/2/models#universal_dependencies_210_models` - a URL to the model's acknowledgements

Now to test the server, go to the browser and try:

    http://localhost:(PORT)/process?tokenizer&tagger&parser&data=(TEXT)

* `(TEXT)` - the test data for the analyzer.   
* `(PORT)` - the port you have chosen.    

## Step 5
Now you can work with UDPipe.
For example, you may create a new Python file and use cURL to send and receive the data from the server via files like this:

    os.system(
    "curl -F model=ukr -F data='@INPUT.txt' -F tokenizer= -F tagger= -F parser= http://localhost:(PORT)/process > OUTPUT.txt")

* `INPUT.txt` - file with raw text for the analyzer with the full path.   
* `OUTPUT.txt` - empty file where the result of the analyzer will be written.   
* `ukr` - model name (Ukrainian in the example)
* `(PORT)` - the port you have chosen.    




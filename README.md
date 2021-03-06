## Information Extraction with Reinforcement Learning

### Installation
You will need to install [Torch](http://torch.ch/docs/getting-started.html) and the  python packages in `requirements.txt`.  

You will also need to install the Lua dev library `liblua` (`sudo apt-get install liblua5.2`) and the [signal](https://github.com/LuaDist/lua-signal) package for Torch to deal with SIGPIPE issues in Linux.
(You may need to uninstall the [signal-fft](https://github.com/soumith/torch-signal) package or rename it to avoid conflicts.)

### Data Preparation

Create the vectorizers (using a pre-trained model):  
`python vec_consolidate.py dloads/train.extra 5 trained_model2.p consolidated/vec_train.5.p`   
  
Consolidate the articles:  
`python consolidate.py dloads/train.extra 5 trained_model2.p consolidated/train+context.5.p consolidated/vec_train.5.p`  


### Running the code
  * Change to the code directory: `cd code/`
  * First run the server:  
    `python server.py --port 7000 --trainEntities consolidated/train+context.5.p --testEntities consolidated/dev+test+context.5.p --outFile outputs/tmp2.out --modelFile trained_model2.p --entity 4 --aggregate always --shooterLenientEval True --delayedReward False --contextType 2` 

  * Then run the agent:  
    `./run_cpu 7000 logs/tmp/`  
    Make sure the port numbers for the server and agent match up.




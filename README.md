# SpikOpt
## Motivation
Neural computational models are a great resource in studying the nervous system, and muscle control. They allow studying cellular mechanisms and simulating neural signals that are impossible to acquire from living animals. Neuron computational models are complex non-linear systems that require high computational resources in operation and development. To bring these models into their optimumuse, they require optimization to certain electrical behaviours and measurements to match and mimic experimental recordings from living cells, so that simulated data from these models would be related to the living systems. Due to the high complexity of these models , manual hand tuning is the main method used in developing these models and calibrating them to experimental data.
## Project Description
The goal of this project is to build a semi/full automated optimization tool to help save time and resources in calibrating neural computational models to experimental measurements. This optimization tool should be able to learn the system parameters that reproduce experimental data

## Installation
To install the required dependencies, run the following command:  
`pip install -r requirements.txt`

## Usage: 
* To run the GUI of SpikOpt,  run the following command:
  `python main.py`
* You can use the core SpikOpt API without the GUI: run `python -m lib.Fitter.py`:
  * Create a Fitter object with the optimization configration dictionary as the following format:
 
```python
fitter = Fitter("Nmodel", "5CompMy_temp.hoc", "fivecompMy")
   
config = {
  "Optimizer": {"Random Seed": 1, "Population Size": 2, "Number of Generations": 2,
                "Offspring Size": 2, "Mutation Probability": 0.3},
  # ---------------------------------------------------------------------------- #
  "stimulation_protocol": {"Protocol Name": "IClamp", "Stimulus Type": "Step", "Amplitude": 21, "Delay": 150, "Duration": 1,
                           "Stimulus Section": "iseg", "Stimulus Position": 0.5, "Param": "V", "Recording Section": "soma", "Recording Position": 0.5, "Vinit": -65, "T stop": 500},
  # ---------------------------------------------------------------------------- #
  "model_meta_data": {"model_type": "Nmodel", "model_file": "5CompMy_temp.hoc", "model_name": "fivecompMy"},
  # ----------------------------------parameters_info must be list of dicts---------------------------------- #
  "parameters_info": [{"location": "soma", "name": "gnabar_NafSmb1", "value": 0.0, "low": 0.0, "high": 1.0},
                      {"location": "soma", "name": "gkdrbar_KdrSmb1",
                          "value": 0.0, "low": 0.0, "high": 1.0},
                      {"location": "soma", "name": "gcanbar_CaSmb1",
                          "value": 0.0, "low": 0.0, "high": 1.0}
                      ],
  # ---------------------------------experimental_data must be OrderedDict-------------------------------------- #
  "experimental_data": OrderedDict({"Rheobase": {"weight": 1.0, "mean": 7.88, "std": None},
                                    "AP Width": {"weight": 1.0, "mean": 0.8, "std": None}
                                    })

    }
 fitter.fit(config)
```
  

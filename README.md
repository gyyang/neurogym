# NeuroGym

#### In Development. Tasks are subject to changes right now.

NeuroGym is a curated collection of neuroscience tasks with a common interface.
The goal is to facilitate training of neural network models on neuroscience tasks. 

NeuroGym inherits from the machine learning toolkit [Gym](https://github.com/openai/gym) by OpenAI, 
and thus allows a wide range of well established machine learning algorithms to be easily trained on behavioral paradigms relevant for the neuroscience community. 
NeuroGym also incorporates several properties and functions (e.g. continuous-time and trial-based tasks) that are important for neuroscience applications.
The toolkit also includes various modifier functions that allow easy configuration of new tasks. 

![alt tag](docs/pipeline.png)

### Installation

You can perform a minimal install of ``neurogym`` with:

    git clone https://github.com/gyyang/neurogym.git
    cd neurogym
    pip install -e .

### Implemented tasks
Currently implemented tasks can be found [here](https://github.com/gyyang/neurogym/blob/master/docs/envs.md).

### Wrappers

Wrappers are short scripts that allow introducing modifications the original tasks. For instance, the Random Dots Motion task can be transformed into a reaction time task by passing it through the *reaction_time* wrapper. Alternatively, the *combine* wrapper allows training an agent in two different tasks simultaneously. 

### Example

NeuroGym is compatible with most packages that use OpenAI gym. 
In this [example](https://github.com/gyyang/neurogym/blob/master/neurogym/examples/example_NeuroGym_stable_baselines.ipynb) jupyter notebook we show how to train
a neural network with reinforcement learning algorithms using the 
[Stable Baselines](https://github.com/hill-a/stable-baselines) toolbox.


### Contributing new tasks
Contributing new tasks is easy. You can contribute tasks using the regular OpenAI gym format. If your task has a trial/epoch structure,
this [template](https://github.com/gyyang/neurogym/blob/master/neurogym/meta/template.py) provides the basic structure that we recommend a task to have:

```
from gym import spaces
import neurogym as ngym

class YourTask(ngym.EpochEnv):
    metadata = {}

    def __init__(self, dt=100, timing=None, extra_input_param=None):
        super().__init__(dt=dt, timing=timing)
       

    def new_trial(self, **kwargs):
        """
        new_trial() is called when a trial ends to generate the next trial.
        Here you have to set:
        The trial periods: fixation, stimulus...
        Optionally, you can set:
        The ground truth: the correct answer for the created trial.
        """
     
    def _step(self, action):
        """
        _step receives an action and returns:
            a new observation, obs
            reward associated with the action, reward
            a boolean variable indicating whether the experiment has end, done
            a dictionary with extra information:
                ground truth correct response, info['gt']
                boolean indicating the end of the trial, info['new_trial']
        """

        return obs, reward, done, {'new_trial': new_trial, 'gt': gt}

```




### Contact
* [Manuel Molano](https://github.com/manuelmolano) (manuelmolanomazon@gmail.com).
* [Guangyu Robert Yang](https://github.com/gyyang) (gyyang.neuro@gmail.com).



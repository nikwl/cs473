Some notes I'll refer to when building the network 

## 1) Create Virtual Environment

You know what virtual environments are at this point. First, create it
```powershell
py -m venv myenv
```

Then, activate it
```powershell
.\myenv\Scripts\Activate.ps1
```

## 2) Install Required Packages

We'll install the following packages
```powershell
pip install torch torchvision matplotlib
```

## 3) General Idea

Let's lay out the general idea of the code we're going to write.

### Dataset

The dataset takes care loading and parsing the input data. If you have any data augmentation you'd also apply this here. The datasets must inherit from `torch.utils.data.Dataset`. Torch datasets must implement the `__len__` and `__getitem__` methods. 

### Network

The network is where you create all of your network layers. The network must inherit from `torch.nn.Module`. The network must implement the `forward` method. 

### Training Loop

We our going to train our network for a set number of `epochs`. The training loop is usually a function that gets called once per epoch. The training loop takes care of:
1) Getting the data from the dataloader (not the dataset, this is important).
2) Passing the data through the network to get a prediction.
3) Computing the loss.
4) Performing backpropogation.

## 4) Additions
- Testing Loop
- Visualization of outputs
- Loss Logging
- Loss Plotting
- Accuracy
- Image normalization   
- Model Saving and Loading
- Model Resuming
- Using the gpu
- Passing Specifications

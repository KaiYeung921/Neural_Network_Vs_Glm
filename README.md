# Neural Network vs GLM: Predicting Hippocampal Neuronal Spiking from LFP Data

A computational neuroscience project done in class comparing the predictive performance of Neural Networks and Generalized Linear Models (GLMs) for predicting neuronal spike counts from local field potential (LFP) recordings in the rat hippocampus.

## Authors
- Eitan 
- Kai
- Winnie

## Project Overview

This project investigates whether model complexity improves the prediction of neuronal spiking based on LFP data from hippocampal area CA1. We compare two approaches:

1. **Generalized Linear Model (GLM)** - A classical, interpretable approach assuming Poisson-distributed spike counts
2. **Neural Network** - A more complex model capable of capturing nonlinear relationships

### Key Research Question
**Does a neural network achieve higher predictive accuracy than a GLM for predicting spike counts from LFP signals?**

## Background

The hippocampus plays a crucial role in memory and spatial navigation. Its neurons show rich relationships with ongoing brain rhythms, particularly theta and gamma oscillations visible in local field potentials (LFPs). This project leverages modern machine learning tools to predict neuronal spiking activity from these LFP signals.

## Dataset

- **Source**: Hippocampal recordings from rats performing a Three-Arm Delayed Sequence Task
- **Recording site**: CA1 region of the hippocampus
- **Data types**: 
  - Local field potentials (LFPs) from multiple electrodes
  - Spike trains from multiple neurons
  - Task metadata (lap IDs, behavioral state)

**Citation**: Gautam Agarwal et al., "Spatially Distributed Local Fields in the Hippocampus Encode Rat Position." *Science* 344, 626-630 (2014). DOI:10.1126/science.1250444

## Methods

### Input Features
- **Toeplitz design matrix** constructed from LFP history (multiple time lags per channel)
- Focuses on running data periods
- Uses top 20 most active neurons as prediction targets

### Models Implemented

#### 1. Poisson GLM
- Assumes spike counts follow a Poisson distribution
- Log firing rate is a linear function of LFP history
- Implemented in PyTorch with hyperparameter optimization

#### 2. Neural Network
- Flexible architecture with configurable hidden layers
- Can learn nonlinear mappings from LFP to spike counts
- Dropout regularization to prevent overfitting

### Hyperparameter Optimization
Both models use **Optuna** for automated hyperparameter search:
- Learning rate
- Batch size
- Regularization strength (weight decay)
- Network architecture (NN only)
- Dropout rates (NN only)

## Results

**Key Finding**: The nonlinear neural network consistently outperforms both Poisson GLMs in predicting hippocampal spike trains from LFP-based features, particularly for moderately and highly active neurons.

- All models struggle with very low-firing neurons
- Neural networks achieve higher correlations for neurons with robust activity
- GLMs plateau earlier in performance
- Most neurons show better NN performance on a per-neuron basis

## Requirements

### Python Dependencies
```
pandas
numpy
matplotlib
scikit-learn
scipy
torch
optuna
gdown
```

See `requirements.txt` for specific versions.

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/neural-network-vs-glm-hippocampus.git
cd neural-network-vs-glm-hippocampus

# Install dependencies
pip install -r requirements.txt

# Download the dataset (automatically handled in notebook)
```

## Usage

1. Open the Jupyter notebook:
```bash
jupyter notebook NeuralNetwork_Vs_GLM.ipynb
```

2. Run all cells sequentially to:
   - Download and load the hippocampal dataset
   - Preprocess LFP and spike data
   - Build Toeplitz design matrices
   - Train and evaluate both models
   - Compare performance across neurons

## Project Structure

```
.
├── README.md                          # This file
├── NeuralNetwork_Vs_GLM.ipynb        # Main analysis notebook
├── requirements.txt                   # Python dependencies
├── LICENSE                            # MIT License
└── .gitignore                        # Files to ignore in version control
```

## Key Findings

1. **Model Complexity Helps**: Neural networks capture spike-LFP relationships that linear Poisson GLMs miss
2. **Activity-Dependent Performance**: Benefits of NNs are most pronounced for moderately to highly active neurons
3. **Nonlinear Relationships**: LFP-to-spike mappings contain substantial nonlinear structure

## References

1. Benjamin, A. S., et al. (2018). "Modern machine learning as a benchmark for fitting neural responses." *Frontiers in Computational Neuroscience*, 12, 56.

2. Gautam Agarwal et al. (2014). "Spatially Distributed Local Fields in the Hippocampus Encode Rat Position." *Science* 344, 626-630. DOI:10.1126/science.1250444

3. KordingLab. (2018). spykesML: Machine learning algorithms for spike prediction. GitHub repository: github.com/KordingLab/spykesML

4. Zhou, P., et al. (2015). "Establishing a statistical link between network oscillations and neural synchrony." *PLOS Computational Biology*, 11(10), e1004549.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Dataset provided by Agarwal et al. (2014)
- Inspired by work from the Kording Lab
- Course project for Computational Neuroscience

## Contact

For questions or collaboration opportunities, please open an issue on this repository.

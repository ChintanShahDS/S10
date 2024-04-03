# S10
# Session 10 - Assignment
## Basic expectations
- Custom ResNet architecture for CIFAR10 that has the following architecture:
  - PrepLayer - Conv 3x3 s1, p1) >> BN >> RELU [64k]
  - Layer 1
    - X = Conv 3x3 (s1, p1) >> MaxPool2D >> BN >> RELU [128k]
    - R1 = ResBlock( (Conv-BN-ReLU-Conv-BN-ReLU))(X) [128k]
    - Add(X, R1)
  - Layer 2
    - Conv 3x3 [256k]
    - MaxPooling2D
    - BN
    - ReLU
  - Layer 3
    - X = Conv 3x3 (s1, p1) >> MaxPool2D >> BN >> RELU [512k]
    - R2 = ResBlock( (Conv-BN-ReLU-Conv-BN-ReLU))(X) [512k]
    - Add(X, R2)
  - MaxPooling with Kernel Size 4
  - FC Layer
  - SoftMax
- Uses One Cycle Policy such that:
  - Total Epochs = 24
  - Max at Epoch = 5
  - LRMIN = FIND
  - LRMAX = FIND
  - NO Annihilation
- Uses this transform
  - RandomCrop 32, 32 (after padding of 4) >> FlipLR >> Followed by CutOut(8, 8)
- Batch size = 512
- Use ADAM and CrossEntropyLoss
- Target Accuracy: 90%

### Results:
- Epochs: 24
- Parameters: 6,573,130
- Training Batch size: 512
- Testing Batch size: 512
- max lr: 0.0006280291441834253
- Training
  - Loss=0.0243
  - Accuracy=99.25%
- Testing
  - Average loss: 0.2660
  - Accuracy: 9281/10000 (92.81%)

### Observations:
- Model is overfitting
- Need to see if dropout can be added to have a better fit model
- Should the Augmentations be applied only to few images
- A couple of times saw that the steepest gradient lr is not good enough for model to converge - Rather the lr at the lowest point was better

# Advanced Deep Learning Labs

Hands-on labs covering the main families of modern deep learning: CNNs and transfer learning, language models, GANs and diffusion models, image captioning, and deep reinforcement learning.

> Coursework for *Advanced Deep Learning (D7047E)*, Luleå University of Technology, spring 2024. Completed by Group 7; see [Team](#team). The course project from the same group is in [nordic-vehicle-detection](https://github.com/amerbarood/nordic-vehicle-detection).

## Labs at a glance

| Lab | Topic | Techniques | Stack |
|---|---|---|---|
| [0](lab0-cnn-fundamentals) | CNN fundamentals | CNNs on CIFAR-10, activation and optimiser comparisons, transfer learning from ImageNet | PyTorch |
| [1](lab1-nlp-sentiment-and-gpt) | Natural language processing | Sentiment classification, character-level GPT with self-attention | PyTorch, NLTK |
| [2](lab2-generative-models) | Generative models | GANs (minimax and non-saturating loss), conditional GAN, adversarial examples, score-based diffusion with a U-Net | PyTorch, TensorFlow |
| [3](lab3-image-captioning) | Vision + language | Image captioning with VGG16 features and an LSTM decoder | TensorFlow/Keras |
| [4](lab4-deep-q-learning) | Reinforcement learning | Deep Q-Network on Atari Breakout, six-run hyperparameter study | Stable-Baselines3, Gym |

## Lab 0: CNN fundamentals

- Trained a CNN on CIFAR-10 and compared **LeakyReLU vs Tanh** activations under **SGD vs Adam**.
- **Transfer learning:** fine-tuned and feature-extracted an ImageNet-pretrained AlexNet, and transferred between digit datasets (MNIST and SVHN).

## Lab 1: NLP, from sentiment to GPT

- **Sentiment analysis** on Amazon product reviews (UCI Sentiment Labelled Sentences), with text preprocessing in NLTK.
- **Character-level GPT** trained on Tiny Shakespeare, built up from a bigram model to multi-head self-attention, feed-forward blocks and residual connections, following Andrej Karpathy's well-known walkthrough.
- Written report and theory answers are in the lab folder.

## Lab 2: Generative models

- **2.1–2.2 GANs on MNIST:** the original minimax objective versus the non-saturating loss that fixes vanishing generator gradients.
- **2.3 Conditional GAN:** generating a chosen digit by conditioning on its label.
- **2.4 Adversarial examples:** crafting small perturbations that fool a trained CNN classifier.
- **2.5 Diffusion models:** forward and reverse diffusion from first principles, then a score-based model with a time-conditioned U-Net, residual connections and a cross-attention transformer variant for conditional generation.

## Lab 3: Image captioning

An encoder–decoder model that writes captions for photos: VGG16 extracts image features, and an LSTM generates the caption word by word. Includes a custom Keras data generator, tokenisation and caption decoding.

## Lab 4: Deep Q-learning on Breakout

Trained a DQN agent on `BreakoutNoFrameskip-v4` and ran six experiments (A–F) varying replay buffer size, exploration schedule, discount factor and batch size.

| Run | Change from baseline | Outcome |
|---|---|---|
| A | Baseline, buffer 100k (memory limit) | Peaked at a score of 59, then collapsed to a poor policy |
| B | Buffer 200k, longer exploration | Sudden catastrophic forgetting around step 175k |
| C | Buffer 250k | Reached higher returns than A, but instability returned |
| D | As C, exploration fraction 0.33 | Learned far too slowly |
| E | As C, exploration fraction 0.08 | Learned faster, still unstable |
| **F** | **Buffer 400k, γ = 0.95, batch 128, exploration 0.05** | **Most stable: steady upward trend, no catastrophic forgetting** |

**Takeaway:** a much larger replay buffer plus a shorter planning horizon (lower γ) gave the most stable learning, at the cost of several days of training on a laptop. Gameplay videos for each run are in [`lab4-deep-q-learning/videos`](lab4-deep-q-learning/videos).

## Running the notebooks

Each notebook is self-contained and was developed in Google Colab or Jupyter. Most labs download their datasets automatically (CIFAR-10, MNIST, SVHN, Tiny Shakespeare). Lab 3 needs an image–caption dataset placed where the notebook's path settings point. Lab 4 needs `gym[atari]` and `stable-baselines3`, plus the Atari ROMs.

## Team

Group 7, D7047E Advanced Deep Learning: **Aamer Barood** and teammates. The original group repository, with full commit history and per-member contributions, is [Gabmyr/D7047E-Labs-Group-7](https://github.com/Gabmyr/D7047E-Labs-Group-7).

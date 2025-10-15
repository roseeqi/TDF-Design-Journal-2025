# Sprint 2: Computer Vision Exercises
TDF Design Journal fall 2025, IND
Rose Qi

Topic chosen: PyTorch as an image classifier
Why I choose this topic: I'm interested in machine learning, and I've experienced using stable diffusion with machine learning to create my own models, and I want to learn how to do this in python

#### Step 0-6: Setting up
I created a virtual environment to isolate dependencies for the PyTorch project.

Process in terminal：
(base) qitianyu@wifi-10-41-165-57 ~ % python3 --version
Python 3.9.13
(base) qitianyu@wifi-10-41-165-57 ~ % pipx list
zsh: command not found: pipx
bash-3.2$ cd Desktop/TDF/pytorch_examples/
bash-3.2$ python3 -m venv cv_venv
bash-3.2$ source cv_venv/bin/activate
(cv_venv) bash-3.2$ pip install -r requirements.txt
WARNING: You are using pip version 22.0.4; however, version 25.2 is available.
You should consider upgrading via the '/Users/qitianyu/Desktop/TDF/pytorch_examples/cv_venv/bin/python3 -m pip install --upgrade pip' command.
(cv_venv) bash-3.2$ 

#### 7. Verify Installation

python3 -c "import torch, torchvision, matplotlib, PIL, numpy; print('✓ All packages installed successfully!')"

It successfully printed

#### 8. Working with the Fashion-MNIST Classifier
I run the second code directly. It took several seconds and loaded this image. <img width="500" height="682" alt="截屏2025-10-09 下午6 21 03" src="https://github.com/user-attachments/assets/967f71b5-95d2-47cf-93c7-f87215053fda" />

After clicking on it, I recieved the result with 
"Epoch 5 completed. Accuracy: 88.49%
Training complete!"

Then, here are the results from my two attempts.

<img width="1191" height="500" alt="截屏2025-10-09 下午6 25 38" src="https://github.com/user-attachments/assets/74a46849-2f5a-4cf3-a679-a760beb1cdf6" />
<img width="1194" height="500" alt="截屏2025-10-09 下午6 27 45" src="https://github.com/user-attachments/assets/46058cbb-126d-4769-977a-5b5aef9c0b89" />

The model misclassified the shirt and pants as a bag.

#### 9. Troubleshooting 

During testing, the model repeatedly classified shirts and pants as bags. Later, the Professor Jeff identified the cause: the Fashion-MNIST model was trained on white objects on black backgrounds, while our images had dark objects on white backgrounds.

An updated version of classifier_example.py was provided, which inverts the image before classification. This simple correction allowed the model to recognize the items more accurately. I learned that visual preprocessing—contrast, background color, and brightness—can significantly affect how a neural network interprets input, even when the model itself works correctly.

Successful testing results:
<img width="959" height="489" alt="截屏2025-10-14 下午6 57 59" src="https://github.com/user-attachments/assets/634919b3-75b1-4887-8add-0759ac825d86" />
<img width="998" height="501" alt="截屏2025-10-14 下午6 56 51" src="https://github.com/user-attachments/assets/9681c439-1e62-46aa-b3d0-e21633bf4648" />
<img width="957" height="491" alt="image" src="https://github.com/user-attachments/assets/14373653-ef9d-4a70-9e92-3a591af5c085" />






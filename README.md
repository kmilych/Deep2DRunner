# Deep2DRunner

## Report
As a final project for Artificial Intelligence in Videogames course I decided to implement DQN controller for [2DRunner template](http://www.mediafire.com/file/l1cbqsk4eg4to6x/Unreal2DRunner.rar) on Unreal Engine 4. The template 2DRunner is a simple game where main character runs through an infinite 2D world which contains pits and enemies and the player needs to jump in time to avoid collision with those obstacles and survive for as long as he can.  The character was supposed to be controlled by human player via pressing the space key when he wants to jump. 

My DQN algorithm was taken from a [similar project for FlappyBird game](https://github.com/yenchenlin/DeepLearningFlappyBird) and it is implemented in python. So the first goal was to use python script as a controller instead of human player. That was achieved by using UnrealEnginePython plugin for UE4. Furthermore, I removed the part that started the new game, so that new game starts right after death.

Next part was about retrieving and preprocessing data for the DQN. First I changed the FPS to 32 and resolution to 240x240 in order to avoid lags. Then I took a screenshot every frame then preprocessed it with some filters using OpenCV to get a black and white 80x80 image. Those screenshots were used as input for the DQN. I also had to specify how to calculate the reward. I defined a score variable that was increased by 1 every time the character sucsessfully jumps over any obstacle and decreased by 1 every time the character dies. Then reward was calculated in the following way: 

```
if score < previous_score:
    reward = -5
elif score > previous_score:
    reward = 1
else:
    reward = 0
```

Finally, I had to train the neural network. I trained it for more than a day on GeForce gtx1070 with 1920 CUDA cores so I was
fully frustrated when I saw the results. However, the goal was to make a bot that acts better then a random algorithm and my bot definetly managed to beat it. As a proof I drew a plot that shows the score that both random and "clever" algorithms had at each of the first 4000 ticks. The score of my bot grows over time, whereas random algorithms score decreases.

# 🤖 Vision-Based Indoor Navigation (PPO + CNN)

A Deep Reinforcement Learning project where a virtual robot learns to navigate an indoor room, avoid obstacles, and reach a target green sphere using only a camera view and directional cues—no maps, GPS, or pre-programmed routes.

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=flat&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![Stable-Baselines3](https://img.shields.io/badge/Stable--Baselines3-v2.2+-38B2AC?style=flat)
![PyBullet](https://img.shields.io/badge/PyBullet-Physics-blue?style=flat)
![Gymnasium](https://img.shields.io/badge/Gymnasium-v0.29-black?style=flat)

---

## 📌 What is This Project?

Imagine dropping a robot into a room it has never seen before:
- It can only see what is in front of it through a small camera.
- There are obstacles placed around the room blocking its path.
- It is told the general direction of the goal, but not how to get there.

This project trains an AI agent using **Proximal Policy Optimization (PPO)** to figure out how to move around obstacles and reach the goal through trial and error across 1.5 million training steps.

---

## 🎬 How It Works

1. **Vision:** A small $64 \times 64$ RGB image from the robot's front camera.
2. **Goal Guidance (4 Values):** 
   - How far the goal is (normalized distance).
   - $\cos(\theta)$ and $\sin(\theta)$ representing the angle to the goal.
   - Current step count (time remaining in the episode).
3. **Brain (MultiInputPolicy):** A CNN looks at the image, an MLP reads the goal numbers, and PPO decides the next movement.

---

## 📸 Navigation in Action

Here is a typical run of the trained robot during a test episode:

| 1. Start Position `(0, 0)` | 2. Dodging an Obstacle |
|:---:|:---:|
| ![Agent Start](./screenshots/agent-spawn.png) | ![Agent Avoiding Obstacle](./screenshots/agent-avoiding-obstacles.png) |
| *Robot spawns in the room* | *Sees a red box ahead and turns away* |

| 3. Heading Toward Goal | 4. Goal Reached (+100 Reward) |
|:---:|:---:|
| ![Agent Approaching](./screenshots/agent-approaching-goal.png) | ![Agent Reached Goal](./screenshots/agent-goal-reached.png) |
| *Lines itself up with the target* | *Hits the green sphere target successfully* |

---

## 🏆 Reward System (How It Learns)

The robot gets feedback after every single step:
- **Getting Closer:** Earns positive reward proportional to distance covered.
- **Facing the Goal:** Small bonus for looking toward the target (prevents spinning in circles).
- **Taking Time:** Small penalty (-0.05) every step to encourage finding the fastest path.
- **Hitting an Obstacle:** Huge penalty (-20.0) and the episode ends immediately.
- **Reaching the Goal:** Huge reward (+100.0) for finishing the task.

---

## 📈 Training Performance

| Average Reward Per Episode | Average Steps Per Episode |
|:---:|:---:|
| ![Reward Graph](./screenshots/tensorboard-ep-rew-mean.png) | ![Episode Length Graph](./screenshots/tensorboard-ep-len-mean.png) |
| *Rewards rise steadily as navigation improves* | *Steps decrease as the agent finds shorter paths* |

- **First 200k steps:** Robot bumps into boxes frequently while exploring.
- **200k - 600k steps:** Learns to face the goal and avoid straight-on crashes.
- **600k+ steps:** Successfully weaves around obstacles in newly generated room layouts.

---

## 📁 Project Structure

```plaintext
.
├── envs/
│   └── indoor_nav_env.py        # PyBullet room environment, physics, and rewards
├── training/
│   ├── train_agent.py           # Training script with PPO hyperparameters
│   └── run_agent.py             # Script to watch the trained robot live in 3D
├── models/
│   ├── ppo_cnn_indoor_nav.zip   # Final trained model
│   └── checkpoints/             # Checkpoints saved every 100k steps
├── logs/
│   └── tensorboard/             # Training logs
├── screenshots/                 # Images for this README
├── plot_training.py             # Script to generate reward and step plots
├── requirements.txt             # Project dependencies
└── README.md                    # Documentation

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

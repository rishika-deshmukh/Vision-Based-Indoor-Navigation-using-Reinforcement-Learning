venv\Scripts\activate
python test_env.py


model.learn(total_timesteps=100_000)



PPO will run 100,000 steps
Each step = simulation + CNN processing
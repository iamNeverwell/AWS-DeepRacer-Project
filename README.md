# AWS-DeepRacer-Project

AWS DeepRacer is the fastest way to get rolling with reinforcement learning (RL), literally, with a fully autonomous 1/18th scale race car driven by reinforcement learning, 3D racing simulator, and a global racing league. Developers can train, evaluate, and tune RL models in the online simulator, deploy their models onto AWS DeepRacer for a real-world autonomous experience and compete in the AWS DeepRacer League for a chance to win the AWS DeepRacer Championship Cup.

### Why did I get myself into this?

I received a message from Udacity about receiving a scholarship from Amazon to learn A.I. and M.L., so I saw a perfect opportunity to improve my skills on a project that I can see results right away, with a pretty cool goal.

In order to receive the scholarship, you need to pass a quiz and train your model to complete 3 loops around a track in 3 minutes or less. Even if I don't get it, it would be pretty cool to see if I manage to show up on the leaderboard :)

### Feb 4, 2023

Track: 

Roger Ring
Length: 45.30m
Width: 106.68cm

![image](https://user-images.githubusercontent.com/117388341/216794922-9f026757-f3ea-47a4-95e8-023937d1d6bb.png)

Algo:

Proximal Policy Optimization (PP0)

I had reached low 3-minute times and after a little over 4 hours of coding and training about 10 models, I finally got below 3 minutes:

Total lap time
02:58.127

And just for laughs, since I am no ML expert:

Your overall rank
1701/3587

Code used:

    def reward_function(params):

    # Read input parameters
    track_width = params['track_width']
    distance_from_center = params['distance_from_center']
    all_wheels_on_track = params['all_wheels_on_track']
    
    MAX_SPEED = 10
    speed = params['speed']
    speed_rate = speed / MAX_SPEED
    return speed_rate ** 2

    # Calculate 6 markers that are at varying distances away from the center line
    marker_1 = 0.1 * track_width
    marker_2 = 0.25 * track_width
    marker_3 = 0.5 * track_width
    marker_4 = 0.75 * track_width
    marker_5 = 0.8 * track_width
    marker_6 = 0.9 * track_width
    
    # Give higher reward if the car is closer to center line and vice versa
    if distance_from_center <= marker_1:
        reward = 1.0
    elif distance_from_center <= marker_2:
        reward = 0.9
    elif distance_from_center <= marker_3:
        reward = 0.8
    elif distance_from_center <= marker_4:
        reward = 0.7
    elif distance_from_center <= marker_5:
        reward = 0.01
    elif distance_from_center <= marker_5:
        reward = 0.001
    else:
        reward = 1e-3 # likely crashed/ close to off track
        
    return float(reward)





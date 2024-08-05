# AWSDeepRacer
A repository containing my impressions e and insights for the AWSDeepRacer competition:

In my AWS journey, in the virtual stage, I managed to classify myself in the physical competition by using a very simple model, created and trained in the very last minute.
In the next stage of the competition, this model didn´t seem to work properly in the road, it was very unstable and it started to get out of the track in some unexpected places, like in the straight parts.
Because of that, I created some new models, with different reward functions and trained in different tracks, in order to make them generalists and not overfitted, as the first model seemed to be.

## Virtual Stage

The first model, named McQueenV4, used discrete space action and different max speeds for each angle that the model could steer. This was done to optimize the training, once that the model didn´t have to test high speeds in turns and fail. The hyperparameters weren´t changed, all was used as default and the training took 5h 30min, in the same track that was going to happen the competition: A to Z Speedway - Counterclockwise. The action space and some hyperparameters can be seen in the image below: 

![Discrete Action Space](.\assets\McQueenV4-setup.png)
The action space is not complete in the image, but the speeds are the same as the negative angles for the positive ones.

The reward function was very simple: 
- It rewards proportionally to the ratio of progress over steps to the power of 2, which means that the more progress the car has in less steps, the more reward it receives.
- It penalizes in 80% the reward if the car has a steering angle over than 22 degress, which forces the model to turn less the steering wheel and try to do the curves more open and fix a little instability problem. 
- It gives a very small reward if the car is off track, this is was used in the hope that the model learned that getting out of the track wasn´t good for it.

This model put me in the 5th position in the regional classification, the last position that would be classified to go to the physical stage in the CSBC, in Brasilia. The model did three laps in the track in 29.8 secs total, it was a little far from the regional first place, which did around 24 secs, but it was enough for the classification.

## Physical Stage

In the physical stage, when we uploaded the model to the physical car, it didn´t perfomed the same as in the virtual simulation, it got out of the track lots of time and was very unstable in some parts of the track. Because of that, and the horrible time that did in the training, the fastest lap was 13 secs, I created another model, but this time with some more sophisticated rewards and different tracks to train.

The action space was continuos and the hyperparameters were a little different, as can be seen in the image below: 

![Discrete Action Space](.\assets\McQueenH3-setup.png)

The reward function was a little more complex this time, it was based in the reward parts: aligment, speed and steering smothness.

- Reward_aligment encourages the model to keep the heading of the car in the optimal steering direction, based on the waypoints of the track.
- Reward_speed encourages the model to use a optimal speed in all the parts of the track, specially on curves. This is calculeted by using the waypoints.
- Reward_steering_smothness encounrages the model not to do sudden changes in the steering direction, and save some time with that.

This model got the best time in the classification for the finals, 8.8 secs in the best lap. 
In the finals, the classification was for the fastest and the most consistent car. So the car has to do it´s best three laps in a row and it´s time is the average of this three laps. This model got 7.8 secs as avarage time, and got the fourth position in the finals, which was a great result, once all the other cars has a little difference in their times. 

This model has great potencial, and little changes in the reward function and maybe more training time can create a beast of DeepRacer.

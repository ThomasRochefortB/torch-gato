## Training a SOTA agent on all the ALE Atari environments.

BOYS! The plan is simple: 

Deepmind trained a Muesli agent for 200M timesteps per environment. To my knowledge, there are no open source implementations of Muesli, so I should look at rllib algorithms. How about using IMPALA? I see it coming up in a lot of leaderboards on PapersWithCode and the Gato authors used it for DM lab


So, the goal would be to first collect SOTA results for all tasks of the ALE Atari envs, then tune IMPALA agents on each environment to ensure we reach SOTA or near - SOTA.
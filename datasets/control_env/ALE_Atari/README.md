## Training a SOTA agent on all the ALE Atari environments.

BOYS! The plan is simple: 

Deepmind trained a Muesli agent for 200M timesteps per environment. To my knowledge, there are no open source implementations of Muesli, so I should look at rllib algorithms. How about using IMPALA? I see it coming up in a lot of leaderboards on PapersWithCode and the Gato authors used it for DM lab. I could also use R2D2 which is implemented in RLLIB.


So, the goal would be to first collect SOTA results for all tasks of the ALE Atari envs, then tune IMPALA agents on each environment to ensure we reach SOTA or near - SOTA. 

For the ATARI environments, we use the ALE library and the autorom library for ROM management (https://github.com/Farama-Foundation/AutoROM)

---
### IMPALA
Impala is implemented in RLLib but I need to recreate the network architecture used in the paper. Someone tried to implement it here: https://github.com/jlsvane/RLLIB-Impala. I need to create a module subclass of TorchModelV2 as in (https://docs.ray.io/en/latest/rllib/rllib-models.html#customizing-preprocessors-and-models)

---
### SOTA

Now, we also need to get an empirical understanding of "What is SOTA?". On PapersWithCode we have a lot of benchmarks:


---











|   **ALE-Atari environment**  	|          **SOTA/ algo**         	| **Our score** 	|
|:----------------------------:	|:-------------------------------:	|:-------------:	|
| 1. Adventure                 	|                                 	|               	|
| 2. Air Raiders               	|                                 	|               	|
| 3. Alien                     	|        741812.63/ MuZero        	|               	|
| 4. Amidar                    	|        29660.08/ Agent57        	|               	|
| 5. Assault                   	|        143972.03/ MuZero        	|               	|
| 6. Asterix                   	|          999999/ GDI-H3         	|               	|
| 7. Asteroids                 	|          760005/ GDI-H3         	|               	|
| 8. Atlantis                  	|         3837300/ GDI-H3         	|               	|
| 9. Atlantis II               	|                                 	|               	|
| 10. Bank Heist               	|         27219.8/ MuZero         	|               	|
| 11. Basic Math               	|        934134.88/ Agent57       	|               	|
| 12. Battlezone               	|                                 	|               	|
| 13. Beamrider                	|        454993.53/ MuZero        	|               	|
| 14. Berzerk                  	|        197376/ Go-Explore       	|               	|
| 15. Blackjack                	|                                 	|               	|
| 16. Bowling                  	|          260.13 Muzero          	|               	|
| 17. Boxing                   	| 100.00/ MuZero, Agent57, Impala 	|               	|
| 18. Breakout                 	|    924.00	/ RYe                   |               	|
| 19. Carnival                 	|                                 	|               	|
| 20. Casino                   	|                                 	|               	|
| 21. Centipede                	|                                 	|               	|
| 22. Chopper Command          	|                                 	|               	|
| 23. Crazy Climber            	|                                 	|               	|
| 24. Crossbow                 	|                                 	|               	|
| 25. Dark Chambers            	|                                 	|               	|
| 26. Defender                 	|                                 	|               	|
| 27. Demon Attack             	|                                 	|               	|
| 28. Donkey Kong              	|                                 	|               	|
| 29. Swordquest: Earthworld   	|                                 	|               	|
| 30. Elevator Action          	|                                 	|               	|
| 31. Enduro                   	|                                 	|               	|
| 32. Entombed                 	|                                 	|               	|
| 33. E.T. The Extra-Te        	|                                 	|               	|
| 34. Fishing Derby            	|                                 	|               	|
| 35. Flag Capture             	|                                 	|               	|
| 36. Freeway                  	|                                 	|               	|
| 37. Frostbite                	|                                 	|               	|
| 38. Galaxian                 	|                                 	|               	|
| 39. Gopher                   	|                                 	|               	|
| 40. Gravitar                 	|                                 	|               	|
| 41. Hangman                  	|                                 	|               	|
| 42. Haunted House            	|                                 	|               	|
| 43. H.E.R.O                  	|                                 	|               	|
| 44. Human Cannonball         	|                                 	|               	|
| 45. Ice Hockey               	|                                 	|               	|
| 46. James Bond 007           	|                                 	|               	|
| 47. Journey Escape           	|                                 	|               	|
| 48. Kaboom!                  	|                                 	|               	|
| 49. Kangaroo                 	|        24034.16/ Agent57        	|               	|
| 50. Kool Aid Man             	|                                 	|               	|
| 51. Keystone Kapers          	|                                 	|               	|
| 52. King Kong                	|                                 	|               	|
| 53. KLAX                     	|                                 	|               	|
| 54. Krull                    	|                                 	|               	|
| 55. Kung Fu Master           	|                                 	|               	|
| 56. Laser Gates              	|                                 	|               	|
| 57. Lost Luggage             	|                                 	|               	|
| 58. Mario Bros               	|                                 	|               	|
| 59. Miniature Golf           	|                                 	|               	|
| 60. Montezuma's Revenge      	|                                 	|               	|
| 61. Mr. Do!                  	|                                 	|               	|
| 62. Ms. Pac-Man              	|                                 	|               	|
| 63. Name This Game           	|                                 	|               	|
| 64. Othello                  	|                                 	|               	|
| 65. Pac-Man                  	|                                 	|               	|
| 66. Phoenix                  	|                                 	|               	|
| 67. Pitfall!                 	|                                 	|               	|
| 68. Pitfall II: Lost Caverns 	|                                 	|               	|
| 69. Video Olympics           	|                                 	|               	|
| 70. Pooyan                   	|                                 	|               	|
| 71. Private Eye              	|                                 	|               	|
| 72. Q*bert                   	|                                 	|               	|
| 73. River Raid               	|                                 	|               	|
| 74. Road Runner              	|                                 	|               	|
| 75. Robot Tank               	|                                 	|               	|
| 76. Seaquest                 	|                                 	|               	|
| 77. Sir Lancelot             	|                                 	|               	|
| 78. Skiing                   	|                                 	|               	|
| 79. Solaris                  	|                                 	|               	|
| 80. Space Invaders           	|                                 	|               	|
| 81. Space War                	|                                 	|               	|
| 82. Stargunner               	|                                 	|               	|
| 83. Superman                 	|                                 	|               	|
| 84. Surround                 	|                                 	|               	|
| 85. Tennis                   	|                                 	|               	|
| 86. Tetris                   	|                                 	|               	|
| 87. 3D Tic-Tac-Toe           	|                                 	|               	|
| 88. Time Pilot               	|                                 	|               	|
| 89. Turmoil                  	|                                 	|               	|
| 90. Tron: Deadly Discs       	|                                 	|               	|
| 91. Tutankham                	|                                 	|               	|
| 92. Up n' Down               	|                                 	|               	|
| 93. Venture                  	|                                 	|               	|
| 94. Video Checkers           	|                                 	|               	|
| 95. Video Chess              	|                                 	|               	|
| 96. Video Cube               	|                                 	|               	|
| 97. Video Pinball            	|                                 	|               	|
| 98. Wizard of Wor            	|                                 	|               	|
| 99. Word Zapper              	|                                 	|               	|
| 100. Yars' Revenge           	|                                 	|               	|
| 101. Zaxxon                  	|                                 	|               	|
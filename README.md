# pygame-RL
#use Rl play game made by pygame

##english





##中文

用Pygame做了一个小游戏，然后用不同的强化学习方法来玩。（model-free）
不同的方法，保存为不同的标题。

###Q-learning，最简单却效果最好，最快速度收敛。所以说简单的问题，最好用简单的方法。不过这里是为了给后面的王者荣耀RL做准备，所以Q-learning的方法仅作为对照组。80回合左右形成稳定的最优策略。

###DQN，一开始不调整replay顺序，很看脸，很容易完全跑不起来。随后加入了优先经验回放，训练变得稳定。
但是过估计的问题非常严重。在这个游戏中，我保留了撞墙的设定，因为后面做王者荣耀和暗黑的RL，都会有撞墙的情况。
结果过估计+撞墙，就会形成一个更加严重的过估计问题。
从数学上来看撞墙（或者原地不动）会让过估计多一个继承者，如果在角落就会多两个继承者。使得作为错误出现的过估计在角落割据成王了，不依靠随机选择的拯救，就很容易被墙角永远抓过去。所以轮次到后面，epsion加到0.95以上就经常卡死了。

###DOUBLE DQN，用这个方法来减弱过估计，确实好了一些。但是过估计同样会出现，最终还是有可能卡死在墙角。只是减弱了症状，但不治本。

###Dueling Double DQN，简称DDDQN。很明显他知道怎么不输，但他对怎么赢似乎不那么确定。后期老是来回冤枉路，但并不会卡死在角落。最终状态是每局徘徊上百步，却总能到达终点。胜率很高100%，但管这个叫最优策略很明显是在骗自己。
----
###Policy Gradient,最原始的PG收敛速度较慢，一般在500-600回合以后就能形成100%胜率。
注意学习率得低一点，然后要做一些reward shaping,不然这个难度很容易被负反馈统治。
现在我设置为1e-5的学习率，+10 -1的reward是比较稳定的。
有明显的退化问题，如果不在最优状态停住，胜率坚持不了一会就会掉头往下。
不过因为没有过估计，退化以后会重新收敛，形成一个治乱循环。




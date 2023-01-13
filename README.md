# FSAS_Big_Data_Bowl_2023

Evaluating Offensive Linemen Using OLIZ: Offensive Linemen Immediate Zone

The public Kaggle notebook can be found here: https://www.kaggle.com/code/petermajors/evaluating-offensive-linemen-using-oliz

Authors: Peter Majors, Chris Orlando, Jack Townsend.

Introduction

When a quarterback drops back in the pocket on a passing play, what is the role of the offensive lineman? Generally, it is to keep the pass rusher as far from the quarterback as possible. Doing so, he gives the quarterback enough time, physical space, and peace of mind to complete a pass to an eligible receiver.

Below we see a series of combinations between distances of various numbers of pass rushers from a quarterback on the final frame he is deemed to have possession of the football, along with the associated Expected Points Added (EPA) of the play. We see that as the distance decreases and and the number of rushers within that distance increases, offensive performance declines.

![image](https://user-images.githubusercontent.com/73561125/212229770-f89c2b8c-321f-4796-af13-6c6aed9d9aa6.png)

Even the mildest of football fans are aware of the relationship between pressure on the quarterback and offensive performance. We aren’t breaking any new ground here. However, what keeps these pass rushers from reaching the quarterback? Well, that would be a series of well fed offensive linemen, patrolling the center, tight end, and guard positions.

Classic approaches to offensive linemen performance concern themselves with binary outcomes such as pressures and sacks, as they are easy to understand, but these outcomes can be difficult to predict and subject to human biases. Among pass blockers with 100 snaps in weeks 1-4 and 5-8, hurries allowed and sacks allowed had a correlation of .32 and .25 , respectively, for the first and second four weeks of the 2021 season. So while sacks are hurries are high impact plays in terms of EPA, their predictive value is suspect.

With this in mind, we decided to investigate, not sacks nor hurries, but a something present in nearly every play: rusher distance from the quarterback at the end of posession, and its impact on EPA as well as predicitve value for sacks and hurries.

Our Proposal

For this year’s Big Data Bowl, we set out to determine the performance of offensive linemen as it pertains to their ability to keep the pass rusher as far as possible from the quarterback at the final moment of the quarterback’s possession of the football. Before proceeding, let’s lay the groundwork for our analysis. Below are the considerations used to determine which plays were selected for our analysis.

- All Passing Plays, First 8 Games Of The 2021 NFL Season
- First Block By Each Pass Blocker Against A Known Pass Rusher
 -Excluding Block Types “Backfield Help”, “Chip Block”, “No Block”, and “Set & Release”
- Excluding Non-Traditional Quarterback Drop Backs (Designed Rollouts, Scramble Rollouts, etc.)
- Blocks Performed By Left Tackles, Left Guards, Centers, Right Guards, and Right Tackles
- Time Between Ball Snap And End Of QB Posession (Ball Release, Run, Strip Sack, Sack)

To determine when an offensive lineman was engaged with their pass rusher, we created a orientation responsive “immediate zone” in front of each pass blocker, designated as their OLIZ , or “Offensive Lineman Immediate Zone” . The OLIZ shifts with the pass blocker’s shoulder orientation at each frame, reaches 1.5 yards in front of them, and spans 1 yard to their left and right. We found that 1.5 yards is the distance in front of a pass blocker where the momentum (speed and acceleration) of an oncoming pass rusher is lowest.

![OLIZ_demonstration_hd](https://user-images.githubusercontent.com/73561125/212230097-a70bd37b-0645-4469-88ca-b5bcdb193069.png)

OLIZ only considers the first rusher a pass blocker was designated as blocking in each play, as the provided data only specified the first block performed by each player in a play. It cannot consider double teams, that being the added benefit a pass blocker would receive from a teammate assiting them against a single pass rusher. Using the OLIZ, we calculated metrics relevant to the performance of an offensive lineman against a single pass rusher in keeping them as far away as possible from the quarterback.

In designing these questions, we wanted to isolate the interactions between blockers and rushers. Our goal was not to predict how close rushers would eventually be - but to determine how much influence offensive lineman have on that final figure under normal circumstances. Each question corresponds to one feature in our model.

Questions Considered When Designing Model Features

**<font size = "5" color = 'maroon'> Questions Considered When Designing Model Features**

- <font size = "4"> How Well Can The Blocker Hold Their Ground? 
    
- <font size = "4"> How Long Can The Blocker Stay Engaged With The Pass Rusher?
    
- <font size = "4"> How Long Can The Blocker Stay Between The QB Than The Pass Rusher?

- <font size = "4"> What Is The Direction Of The Rusher Relative To The Orientation Of The Blocker Coming Into The Block?

- <font size = "4"> How Well Can The Blocker Maintain Similar Shoulder Orientation To The Rusher? 
    
- <font size = "4"> How Well Can The Blocker Slow The Rusher As They're Leaving The Immediate Zone? 

- <font size = "4"> If The Blocker Loses Control of The Pass Rusher, How Well Can They Recover?

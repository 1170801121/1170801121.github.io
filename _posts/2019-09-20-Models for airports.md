---
title: Profit Optimization for Taxi Driver and Passengers Using Large Dataset 
layout: post
tags: 
img: taxi.jfif
---

Luckily, I was selected as a member of HIT Mathematical modeling Club to address a specific problem for airport projects.  My team members : **Jianyu Xiong, Rui Li**.

After most passengers get off the plane, they have to go to the city (or  surrounding) destination. Taxi is one of the main means of  transportation. Most domestic airports separate **the delivery (departure) and pickup (arrival) passages**. Taxi drivers who send passengers to the airport will face **two choices**:  entering the car storage pool to wait for passengers will need to pay  the corresponding time cost, while choosing to empty directly back to  the city will need to pay the no-load cost and potential loss of  passenger income. The number of flights arrived in a certain period of time and the  number of vehicles in the "car storage pool" are certain information that can be observed by the driver. How to **make a judgment based on the  known information to maximize the benefits** is very important. 

By analyzing and studying the influencing mechanism of factors related to taxi driver's decision-making, taking into account the changing law of airport passenger number and taxi driver's income, I set up a decision-making model for taxi driver's choice, and gave the driver's choice strategy: using the evaluation system of "**net income per unit time**", I calculated the net income per unit time of the two schemes respectively, and finally selected the scheme with a larger net income per unit time. When calculating the net income per unit time of scheme a, we focus on establishing **a queuing time model based on algorithm simulation**. The model carefully considers the impact of the arrival flight information list, the current number of taxi queuing L, the current number of passengers waiting for boarding 𝑝0 on the queuing time. The highlight of the model is to **simulate the flight arrival information one by one to ensure the accuracy of the output**.



By selecting **Shanghai Pudong International Airport and its taxis** as the  research objects, we use **Python crawler to collect in-depth relevant  information of Shanghai Pudong International Airport**, such as flight  information table, population density map of Shanghai, taxi pricing  formula of Shanghai, etc., give the taxi driver selection scheme of the  airport, and analyze the rationality of the model and the relevant  factors Element dependence. According to the population density map of Shanghai, we creatively  **establish the relationship model between the population density and the  probability density of taxi mileage, which makes the data closer to the  reality**. When analyzing the dependence of the model, we take a series of proper  passenger 𝑝0 values which are waiting to get on the train at present,  and then draw the decision scatter diagram under each 𝑝0 value, different arrival time t and the number of waiting taxis L. **Based on these scatter diagrams, we analyze the dependence of the model on the relevant input and the rationality of the model**. 

<center>
<img src="{{site.baseurl}}/assets/img/pydata1.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">information of Shanghai Pudong International Airport collected by Python crawler</div><br>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/shanghai.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">population density map of Shanghai</div><br>
</center>

<center>
<img src="{{site.baseurl}}/assets/img/sdot.png" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">decision scatter diagram </div><br>
</center>



By establishing a mathematical model that considers factors such as safety, ride efficiency, management cost and uncertainty of passengers' boarding time in real situation, **we help the management department to simulate how to set "boarding point" and arrange taxis and passengers reasonably**, so that the total ride efficiency is the highest under the condition of ensuring the safety of vehicles and passengers

First of all, we consider how to ensure the safety of vehicles and passengers. After analysis and demonstration, according to a rule, **we first get a scheme of taxi entry and exit**, and in the scheme, we can properly arrange the time for passengers to get on the bus, so that the safety of passengers can be guaranteed, and the waiting time of passengers can be reduced as soon as possible, and the service comfort of passengers can be improved.

<center>
<img src="{{site.baseurl}}/assets/img/442.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/443.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/444.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">a scheme of taxi entry and exit</div>
</center>

Under this scheme, we also discuss the influence of the number of taxis waiting for passengers at the same time in the parking area on the departure rate per unit time, and because of the instability of passengers' boarding time, the departure rate per unit time will also be affected. We have established **a mathematical model, considered the above factors, calculated the unit time drive out rate corresponding to different parking spaces, and comprehensively considered the actual factors such as management cost, and obtained an optimal scheme**, so that the driver's income will be increased, and the cost paid by the management department will not be wasted too much. In particular, we consider **the impact of uncertainty in the real situation**, which is a bright spot. At last, the load rate of each parking space and the feasible adjustment method are discussed.

$T$ is the time from the time when all vehicles of the k-th enter the departure area to the time when all vehicles of the K+1-th enter the departure area.  In the process of derivation, we compute $T$ differently when the amount of parking spaces $2i$ is varied as follows.

<center>
<img src="{{site.baseurl}}/assets/img/445.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/446.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/447.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">the computation of $T$</div>
</center>


For the random time of passengers' boarding, we can get the frequency  distribution chart in the following table from references, use the Monte Carlo method to process the data.
<center>
<img src="{{site.baseurl}}/assets/img/448.JPG"  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">frequency distribution chart</div>
</center>


Then use the linear interpolation method to get a random time m of passengers' boarding $M$ :  $M(rand) = y_1 + \frac {x-x_1}  {x_2-x_1}(y_2-y_1), rand \in (x_1,x_2)$


In order to eliminate the influence of the instability of the T calculation result caused by the random distribution of the passenger boarding time, we will simulate the situation that 8000 vehicles are waiting to pass through the parking area to carry passengers every time, simulate 1000 times, and the average $T$ obtained is of universal significance, and the results are as follows.

<center>
<img src="{{site.baseurl}}/assets/img/3q1.JPG"  /><br>
<img src="{{site.baseurl}}/assets/img/3q2.JPG"  /><br>
</center>


Based on the above model, **we also introduce "jump-queue  coefficient" $a$ as a measure to give certain priority to some short-distance taxi drivers who return again, ensuring that the  "net income per unit time" of short-distance taxi drivers is equal to  the "net income per unit time" of non short-distance taxi drivers**, so as to make the income of these taxis as balanced as possible. 

Therefore, the queue jumping coefficient is determined by the mileage of short  distance passengers $X'$, the current number of taxi queuing $L$, the  current number of passengers waiting for boarding $p0$, and the time when  the driver goes to the queue $T$. In the end, **we bring in a group of conventional data, and fit the  relationship between jump-queue  coefficient $a$ and short distance passenger mileage $X'$. The fitting curve shows good performance and the rationality of  the model. **
<center>
<img src="{{site.baseurl}}/assets/img/fitting4.png "   width="35%" height="35%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">fitting curve between jump-queue  coefficient and short distance passenger mileage</div>
</center>

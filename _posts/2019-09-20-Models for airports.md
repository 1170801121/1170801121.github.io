---
title: Profit Optimization for Taxi Drivers at Airports Using a Large Dataset 
layout: post
tags: 
img: taxi.jfif
---

To help taxi drivers at airports make the most proﬁtable decisions (whether to wait at the arrival gates, or drive downtown to seek passengers), I established a mathematical model, and used a Python crawler to collect data and optimize the model. My application achieved an approximately 100% increase in eﬃciency for drivers, and I am proud that it has been used at Harbin Taiping International Airport. 

## Background
After most passengers get off the plane, they have to go to the city (or surrounding) destination. Taxi is one of the main means of  transportation. Most domestic airports separate **the delivery (departure) and pickup (arrival) passages**. So taxi drivers who send passengers to the airport will face **two choices**:  the choice for entering the car waiting pool to pick up passengers need corresponding time cost, while choosing to drive directly back to the city without taking passengers need to pay the potential income loss from passengers in the airports. The number of flights arrived in a certain period and the number of taxis and passengers are the information that can be observed by taxi drivers. So how to **make a judgment based on the  known information to maximize the benefits of drivers** is very important. 

I analyzed the influencing mechanism of factors related to taxi driver's profits, then set up a taxi driver's decision-making model based on queuing theory, and gave the reasonable choice strategy. I used the evaluation system of "**net income per unit time**", and calculated the net income per unit time of the two choices respectively, and finally selected the choice with a larger net income per unit time. When calculating the net income per unit time of each choice, I established a model to simulate **the queuing time**. The model considers the impact of the arrival flight information, the number of taxi in the queue L, the number of passengers waiting for taxis 𝑝0. The highlight of the model is to **simulate the relevant information comprehensively to ensure the accuracy of the prediction**.



By selecting **Shanghai Pudong International Airport** as the research object, I used **a Python crawler to collect relevant information of Shanghai Pudong International Airport**, such as flight information, taxi information, population probability density of Shanghai, taxi mileage probability density, taxi pricing formula, etc. I  **modeled the relationship between the population probability density and the taxi mileage probability density**, which made the model closer to the reality. And I conducted many simulation experiments. More specifically, I took a series of 𝑝0, the number of passengers waiting for taxis,  and then draw the decision scatter diagram under each 𝑝0 value at different arrival time t and the number of taxis L. **Based on these scatter diagrams, I analyzed the model’s dependence on relevant factors and the model's rationality**. 

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



Besides, by considering factors such as safety, ride efficiency, management cost and uncertainty of passengers' boarding time, **I helped the management department at airports to make decision on how to set the boarding point for passengers and arrange taxi drivers and passengers** to make the total ride efficiency the highest when ensuring the safety of vehicles and passengers. 

To ensure the safety of vehicles and passengers, I **firstly established a scheme of taxi entry and exit**, and then properly arranged passengers to get on the taxis under the scheme to reduce the waiting time of passengers as soon as possible.

<center>
<img src="{{site.baseurl}}/assets/img/442.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/443.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/444.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">a scheme of taxi entry and exit</div>
</center>

Under this scheme, I also discussed the influence of the number of taxis waiting for passengers at the same time in the parking area on the departure rate per unit time, and because of the instability of passengers' boarding time, the departure rate per unit time will also be affected. We have established **a mathematical model, considered the above factors, calculated the unit time drive out rate corresponding to different parking spaces, and comprehensively considered the actual factors such as management cost, and obtained an optimal scheme**, so that the driver's income will be increased, and the cost paid by the management department will not be wasted too much. In particular, we consider **the impact of uncertainty in the real situation**, which is a bright spot. At last, the load rate of each parking space and the feasible adjustment method are discussed.

$T$ is the time from the time when all vehicles of the k-th enter the departure area to the time when all vehicles of the K+1-th enter the departure area.  In the process of derivation, I computed $T$ differently when the amount of parking spaces $2i$ is varied as follows.

<center>
<img src="{{site.baseurl}}/assets/img/445.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/446.JPG" width="55%" height="55%" /><br>
<img src="{{site.baseurl}}/assets/img/447.JPG" width="55%" height="55%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">the computation of $T$</div>
</center>


For the queuing theory–based models’ inherent uncertainties, such as  the random passenger boarding time, I firstly got the frequency  distribution chart as follows, using the Monte Carlo method to process the data.
<center>
<img src="{{site.baseurl}}/assets/img/448.JPG"  /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">frequency distribution chart</div>
</center>


Then I applied the linear interpolation method to estimate passengers' boarding time $M$ :  $M(rand) = y_1 + \frac {x-x_1}  {x_2-x_1}(y_2-y_1), rand \in (x_1,x_2)$


To reduce the negative influence from the variety of T's calculation caused by models’ inherent uncertainties, I established the situation that 8000 vehicles are waiting to carry passengers, and simulated for 1000 times. The average $T$ obtained is of universal significance, and the results are as follows.

<center>
<img src="{{site.baseurl}}/assets/img/3q1.JPG"  /><br>
<img src="{{site.baseurl}}/assets/img/3q2.JPG"  /><br>
</center>


Based on the above model, to make the income between drivers as balanced as possible, I also **introduced a priority factor  $a$ allowing drivers with lower profits to jump the queue**, ensuring that the short-distance taxi driver's profit is equal to that of long-distance taxi driver. 

The priority factor should be determined by short-distance passengers' mileage $X'$, the number of taxi $L$, the number of passengers  $p0$, and the time when the driver goes back to the queue at airports  $T$. I added this factor into above model. **The  relationship between priority factor $a$ and passenger's mileage $X'$ is as follows.** 

<center>
<img src="{{site.baseurl}}/assets/img/fitting4.png "   width="35%" height="35%" /><br>
<div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">The relationship between priority factor and passenger's mileage.</div>
</center>

Overall, these simulation experienments of the model showed effeciency and rationality. And I am very proud that it has been used at Harbin Taiping International Airport. 
---
title: Profit Optimization for Taxi Driver and Passengers Using Large Dataset 
layout: post
tags: 
img: taxi.jfif
---

Luckily, I was selected as a member of HIT Smart Car Innovational Club in Oct.2017 , a club that is aimed at the 13th National University NXP Cup of Smart Car Competition.  My team members : **Jianyu Xiong, Rui Li**.

大多数乘客下飞机后要去市区（或周边）的目的地，出租车是主要的交通工具之一。国内多数机场都是将送客（出发）与接客（到达）通道分开的。送客到机场的出租车司机都将会面临两个选择：进入蓄车池等待载客则需要付出相应的时间成本，而选择放空直接返回市区则需要付出空载费用和可能损失潜在的载客收益。在某时间段抵达的航班数量和“蓄车池”里已有的车辆数是司机可观测到的确定信息，如何根据已知信息去做出判断使得利益最大化就十分重要了。

After most passengers get off the plane, they have to go to the city (or  surrounding) destination. Taxi is one of the main means of  transportation. Most domestic airports separate **the delivery (departure) and pickup (arrival) passages**. Taxi drivers who send passengers to the airport will face **two choices**:  entering the car storage pool to wait for passengers will need to pay  the corresponding time cost, while choosing to empty directly back to  the city will need to pay the no-load cost and potential loss of  passenger income. The number of flights arrived in a certain period of time and the  number of vehicles in the "car storage pool" are certain information that can be observed by the driver. How to **make a judgment based on the  known information to maximize the benefits** is very important. 


我通过分析研究与出租车司机决策相关因素的影响机理，综合考虑机场乘客数量的变化规律和出租车司机的收益，建立出租车司机选择决策模型，并给出司机的选择策略：采用“单位时间净收益”的评价体系，分别计算上述两种方案的单位时间净收益，最后选取单位时间净收益更大的方案。在计算A方案的单位时间净收益时，我们着重建立了计算基于算法模拟的排队时间模型。该模型细致地考虑了一段时间内到达的航班信息list、当前排队出租车数L、当前等待上车的乘客数𝑝0对排队时间的影响。该模型的亮点为，对航班到达信息进行逐条模拟，保证了输出的精确度。

By analyzing and studying the influencing mechanism of factors related to taxi driver's decision-making, taking into account the changing law of airport passenger number and taxi driver's income, I set up a decision-making model for taxi driver's choice, and gave the driver's choice strategy: using the evaluation system of "**net income per unit time**", I calculated the net income per unit time of the two schemes respectively, and finally selected the scheme with a larger net income per unit time. When calculating the net income per unit time of scheme a, we focus on establishing **a queuing time model based on algorithm simulation**. The model carefully considers the impact of the arrival flight information list, the current number of taxi queuing L, the current number of passengers waiting for boarding 𝑝0 on the queuing time. The highlight of the model is to **simulate the flight arrival information one by one to ensure the accuracy of the output**.



我通过选取上海市浦东国际机场及该市的出租车为研究对象，我们使用python爬虫深入搜集了上海市浦东国际机场的相关信息，如全天的航班信息表、上海市人口密度地图、上海出租车计价公式等，给出该机场出租车司机的选择方案，并分析模型的合理性和对相关因素的依赖性。其中，我们依据上海市人口密度地图，创造性的建立了人口密度与打车里程概率密度的关系模型，使得数据更为贴近实际。在分析模型的依赖性时，我们取一系列的适当的当前等待上车的乘客𝑝0值，然后在每个𝑝0值下，在不同的到达时间t和排队出租车数L下，绘制决策散点图。基于这些散点图，我们分析了模型对相关输入的依赖性以及模型的合理性。



By selecting **Shanghai Pudong International Airport and its taxis** as the  research objects, we use **Python crawler to collect in-depth relevant  information of Shanghai Pudong International Airport**, such as flight  information table, population density map of Shanghai, taxi pricing  formula of Shanghai, etc., give the taxi driver selection scheme of the  airport, and analyze the rationality of the model and the relevant  factors Element dependence. According to the population density map of Shanghai, we creatively  **establish the relationship model between the population density and the  probability density of taxi mileage, which makes the data closer to the  reality**. When analyzing the dependence of the model, we take a series of proper  passenger 𝑝0 values which are waiting to get on the train at present,  and then draw the decision scatter diagram under each 𝑝0 value, different arrival time t and the number of waiting taxis L. **Based on these scatter diagrams, we analyze the dependence of the model on the relevant input and the rationality of the model**. 

<div align=center>![Our team]({{site.baseurl}}/assets/img/pydata1.png)  information of Shanghai Pudong International Airport collected by Python crawler </div>

<div align=center>![Our team]({{site.baseurl}}/assets/img/shanghai.png) {:height="50%" width="50%"} information of Shanghai Pudong International Airport collected by Python crawler </div>

<center>
<img src="{{site.baseurl}}/assets/img/sdot.png" width="55%" height="55%" />
Figure 1. Lena
</center>
<div align=center>![Our team]({{site.baseurl}}/assets/img/sdot.png){:height="50%" width="50%"}
<div align=center>![Our team]({{site.baseurl}}/assets/img/sdot.png)
我们通过建立考虑了安全、乘车效率、管理成本以及现实状况下乘客上车时间的不确定性等影响因素的数学模型，帮助管理部门模拟决策如何设置“上车点”，并合理安排出租车和乘客，在保证车辆和乘客安全的条件下，使得总的乘车效率最高：
我们首先考虑如何保证车辆和乘客安全，经过分析论证，按照一种规则，我们先得到了一种出租车驶入与驶出的方案，并且在方案中可以恰当地安排乘客上车的时机，使得既保证了乘客的安全，又能尽快地上车，减少乘客的等待时间，提高了乘客的服务舒适感。

By establishing a mathematical model that considers factors such as safety, ride efficiency, management cost and uncertainty of passengers' boarding time in real situation, **we help the management department to simulate how to set "boarding point" and arrange taxis and passengers reasonably**, so that the total ride efficiency is the highest under the condition of ensuring the safety of vehicles and passengers

First of all, we consider how to ensure the safety of vehicles and passengers. After analysis and demonstration, according to a rule, **we first get a scheme of taxi entry and exit**, and in the scheme, we can properly arrange the time for passengers to get on the bus, so that the safety of passengers can be guaranteed, and the waiting time of passengers can be reduced as soon as possible, and the service comfort of passengers can be improved.

<div align=center>![Our team]({{site.baseurl}}/assets/img/442.JPG)

<div align=center>![Our team]({{site.baseurl}}/assets/img/443.JPG)

<div align=center>![Our team]({{site.baseurl}}/assets/img/444.JPG)

在此方案下，我们又探讨了泊车区可同时等待载客的出租车的数量对于单位时间驶出率的影响，且由于乘客上车时间的不稳定性也会影响单位时间驶出率。我们建立了一个数学模型，考虑了前述影响因素，算得了不同的泊车位数量所对应的单位时间驶出率，又综合考虑了管理成本等实际因素，得出了一个最优方案，这样使得司机的收益也会得到提高，同时管理部门所付出的成本也不会浪费太多。在本题中，我们考虑到了现实状况下不确定性所带来的影响，是一个亮点。
最后还对于得到的最优方案的每个车位的负荷率及可行的调整方法进行了简单的讨论。
Under this scheme, we also discuss the influence of the number of taxis waiting for passengers at the same time in the parking area on the departure rate per unit time, and because of the instability of passengers' boarding time, the departure rate per unit time will also be affected. We have established **a mathematical model, considered the above factors, calculated the unit time drive out rate corresponding to different parking spaces, and comprehensively considered the actual factors such as management cost, and obtained an optimal scheme**, so that the driver's income will be increased, and the cost paid by the management department will not be wasted too much. In particular, we consider **the impact of uncertainty in the real situation**, which is a bright spot. At last, the load rate of each parking space and the feasible adjustment method are discussed.

$T$ is the time from the time when all vehicles of the k-th enter the departure area to the time when all vehicles of the K+1-th enter the departure area.  In the process of derivation, we compute $T$ differently when the amount of parking spaces $2i$ is varied.

<div align=center>![Our team]({{site.baseurl}}/assets/img/445.JPG)

<div align=center>![Our team]({{site.baseurl}}/assets/img/446.JPG)

<div align=center>![Our team]({{site.baseurl}}/assets/img/447.JPG)

对于乘客上车的随机时间，我们由参考文献 可得到下表中的频率分布图，应用蒙特卡罗方法将数据进行处理，再线性插值方式可得到一个随机的乘客上车时间M

For the random time of passengers' boarding, we can get the frequency  distribution chart in the following table from references, use the Monte Carlo method to process the data.

<div align=center>![Our team]({{site.baseurl}}/assets/img/448.JPG)

Then use the linear interpolation method to get a random time m of passengers' boarding $M$ :  $M(rand) = y_1 + \frac {x-x_1}  {x_2-x_1}(y_2-y_1), rand \in (x_1,x_2)$


为了消除由于乘客上车时长随机分布导致的T计算结果不稳定性的影响，我们将模拟每次有8000辆车待通过泊车区载客的情况，模拟1000次，得到的平均T就具有普适意义，得到的结果如下表

In order to eliminate the influence of the instability of the T calculation result caused by the random distribution of the passenger boarding time, we will simulate the situation that 8000 vehicles are waiting to pass through the parking area to carry passengers every time, simulate 1000 times, and the average $T$ obtained is of universal significance, and the results are as follows.


<div align=center>![Our team]({{site.baseurl}}/assets/img/3q1.JPG)

<div align=center>![Our team]({{site.baseurl}}/assets/img/3q2.JPG)

我们还基于上述的模型，引入“插队系数”a 作为“优先权”的衡量标准，对某些短途载客再次返回的出租车给予一定的“优先权”，保证了短途载客司机的“单位时间净收益”与非短途载客司机的“单位时间净收益”相等，使得这些出租车的收益尽量均衡。
因而，插队系数受短途客里程数 x’、当前排队出租车数L、当前等待上车的乘客数𝑝0、司机前往排队的时间决定。在最后，我们带入了一组常规的数据，对插队系数 a 与短途客里程数 x’的关系进行了拟合，拟合曲线表现良好，表现了模型的合理性。

Based on the above model, **we also introduce "jump-queue  coefficient" $a$ as a measure to give certain priority to some short-distance taxi drivers who return again, ensuring that the  "net income per unit time" of short-distance taxi drivers is equal to  the "net income per unit time" of non short-distance taxi drivers**, so as to make the income of these taxis as balanced as possible. 

Therefore, the queue jumping coefficient is determined by the mileage of short  distance passengers $X'$, the current number of taxi queuing $L$, the  current number of passengers waiting for boarding $p0$, and the time when  the driver goes to the queue $T$. In the end, **we bring in a group of conventional data, and fit the  relationship between jump-queue  coefficient $a$ and short distance passenger mileage $X'$. The fitting curve shows good performance and the rationality of  the model. **
![Our team]({{site.baseurl}}/assets/img/fitting4.png)
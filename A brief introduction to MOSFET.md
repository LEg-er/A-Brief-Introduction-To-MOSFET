# A brief introduction to MOSFET
================================
As the title shows, I'll give a brief introduction to a MOSFET, including basic principle and typical features.


This is my `FIRST` Blog, my writing proficiency needs to be improved and I still have a long way to go. So if there are mistakes, I beg for your critique and correction!

****
	
|Presented By|LEg-er|
|---|---
|Email|cairx_study@163.com
|Github|https://github.com/LEg-er


****
## Contents
* [Operational Principle](#Operational Principle)
* [Character Description](#Character Description)
	* [Uds](#Uds)
 	* [Qg](#Qg)
	* [Rds(on)](#Rds(on))
	* [Ugs(th)](#Ugs(th))
* [Other Tips](#Other Tips)
* [Summary](#Summary)


## Operational Principle


Before we talk about how the MOSFET operates, some of us may have a question: What is MOSFET? 

<div  align="center">    
 <img src="https://www.infineon.com/export/sites/default/media/products/irf/to-220ab.png_953229815.png" width = "200" alt="Fail to load image" align=center />
</div>

MOSFET is actually an abbreviation of Metal-Oxide-Semiconductor-Field-Effect-Transistor, it's obviously to find out the material but puzzling to get the point of field effect


Wikipedia describe field effect as this:

	the physical mechanism modulating the conductivity of a semiconductor
	using an applied voltage difference.

Okey, it's clear that Field effect means to control the conductivity with voltage. Now let's look into the specific structure of MOSFET to figure out its working mechanism. We use N channal enhancement mode MOSFET ,which is used most in real application, as an example.

<div  align="center">    
 <img src="http://users.cecs.anu.edu.au/~Matthew.James/engn2211-2002/notes/fetimg17.gif" width = "400" alt="Fail to load image" align=center />
</div>


There are four pins in the diagram above: source, gate, drain and B(base), we can find the gate pin isn't directly connected to semiconductor material but attach to a piece of silicon dioxide which is insulating, gate pin and the source pin is directly connected to two separated N-type semiconductors. The P-type base is a large one whose volume is the biggest. next picture shows the typical schematic symbol of MOSFET 


<div  align="center">    
 <img src="http://www.cmm.gov.mo/images/exhibits/2_10_4_3_chis.png" width = "200" alt="Fail to load image" align=center />
</div>


You may find source and drain is highly symmetric in the first picture, they are all alike in many ways. So we must know how it works before we figure out the name.


Now, we apply a positive voltage between the base(B) and gate, the holes in the P-type semiconductors are rejected and the eletrons in the N-type semiconductors are attracted, so the barrier made by P-type semiconductors between source and drain begin to collapse, and a conductive channel made up of N-type semiconductors is building up.

<div align="center">   
 <img src="https://www.hxymos.com/web/userfiles/1.png" width = "300" alt="Fail to load image" align=center />
</div>
 
Now you know the qualitative operation mode of MOSFET. In fact we always tie the base to the source pin, so we analyse MOSFET's behaviour by using the voltage between gate and source marked as Ugs, the diagram below explains the actual relationship between Ugs and the conductivity of the conductive channal represented by the current flows through drain to source(Id)when a specific voltage is applied between drain and source.  We can find there is a threshold before which the conductive channal is forming and the MOSFET is non-conductive, so the threshold mark the MOSFET is 'open' and under which a MOSFET is 'closed'. In power eletronic, we usually let a MOSFET works as a switch to control current flow's on-off, in this case voltage between drain and source is very small, so the character of MOSFET is in the left boundary of the diagram the relationship between current flows through MOSFET and voltage between drain and source is almost linear, our mosfet work as a voltage control resistor and if the Ugs is enough, the on resistance can be very small, maybe less than 1 milliohm. So if I apply a periodic switching signal to gate, we can control the MOSFET to quickly open and close.


In other application fields such as signal amplification or DC eletronic load, the MOSFET works in constant current region where the curve is parallel to Uds axis and the Id is controlled by Ugs only. We can discuss it lately in next blog.


<div align="center">    
 <img src="http://www.changjing2008.cn/uploadfile/image/20191122/20191122153147_1462430481.jpg" width = "400" alt="Fail to load image" align=center />
</div> 


## Character Description
When we talk about MOSFET, we usually juedge it's performance and choose appropriate materiel in four directions: maxium voltage tolerace between drain and source, the switching performance, the on-region characteristic and threshold voltage to open the MOSFET. I list it below and let's understand it individually.
	
|Character|Physical Quantity|
|---|---
|maxium voltage tolerace between drain and source|Uds
|the switching performance|Qg
|the on-region characteristic|Rds(on)
|threshold voltage to open the MOSFET|Ugs(th)


### Uds
Obviously, Uds shows the voltage level of a MOSFET, it well breakdown if you apply a high voltage. Also you need to becareful about voltage overshoot as it can easily destroy MOSFET and isn't easy to find it. You can make enough margin and design protect circuit to absorb voltage spikes. For example I want to design a 40V fly-back circuit, and the voltage overshot can reach over 60V in transformer primary coli. So when I choose primary switch FET, I should choose a MOSFET whose Uds is higher than 60V, maybe 70V or higher, then I also need to design a overshot absorbing circuit typically using a transient voltage suppressor diode(TVS diode). Next picture is TI's reference design of UCC28704, a tipical fly-back controller, I point out its portection circuit. 



<div align="center">    
 <img src="https://github.com/LEg-er/A-Brief-Introduction-To-MOSFET/blob/main/Images/UCC28704EVM-724%20Schematic.png?raw=true" width = "700" alt="Fail to load image" align=center />
</div> 
  

<div align="center">    
  Fig.1 UCC28704EVM-724 Schematic
</div>  


###Qg
Qg means total gate charge, you may wonder why gate neads charge as MOSFET is a voltage control device. In fact it a very complex process for a MOSFET to open in high speed, we can discuss it lately, now the only thing you need to know is that Qg exist because the parasitic capacitor between gate, source and drain. Qg always take nC as unit and smaller Qg means less loss in the hign speed switching process.


<div align="center">    
 <img src="https://www.rohm.com.tw/documents/11409/7486925/image01.jpg/999dfde1-a9fa-0d2e-c6b8-45444a35685a?t=1578278948473" width = "300" alt="Fail to load image" align=center />
</div> 
  

<div align="center">    
  Fig.1 Dynamic Character of Gate
</div>  
 


###Rds(on)
It's easy to understand Rds(on) since you have already had a clear understanding of the conductive channal and Rds(on) mean the resistance of the conductive channnal when it is completely open. It characterize the on-stage performance. Usually the on-stage peformance and the switching proformance can't make the best of both worlds, ideal low on-stage resistance always mean it's not very easy to open and the same to Qg. But if you have an ample budget or your target voltage level isn't very high you are more likely to find an ideal one.


<div align="center">    
 <img src="https://www.rohm.com.tw/documents/11409/6565466/tr_what9_img_01.gif/9e6275dc-f85f-fb25-c751-1e476ff021cb?t=1541393659113" width = "500" alt="Fail to load image" align=center />
</div> 
  

<div align="center">    
  Fig.1 Relationship between Rds(on) and Ugs and Temperature
</div>


###Ugs(th)
This indicator has been explained in pervious content, I think there is an another thing to highlight that wen you want to drive a MOSFET as a switch using a micro controller directilly, you need to choose a low Ugs(th) one. Also you should care about it when you don't have enough drive voltage. 




##Other Tips 
Now we should think about a question, since we tie the base to the source pin, is the conductive channel form by Ugs the only way for current to flow from drain to source? The answer is no, because the base is consist of P-type semiconductors so it can form PN junction with the N-type semiconductor in the drain, so there is a body diode from the source to the drain. So we usually use symbol like Fig.2 to mark the body diode and help us to distinguish drain and source.


<table width="100%" border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td align="center"><img src="http://www.kiaic.com/include/upload/kind/image/20190125/20190125091527_9687.jpg" width="300" /> </td>
    <td align="center"><img src="https://file2.dzsc.com/data/17/03/01/9207_161831641.jpg" width="350" /></td>
  </tr>
  <tr>
    <td align="center">Fig.1 body diode formation </td>
    <td align="center">Fig.2 symbol of MOSFET highlight body diode </td>
  </tr>
<table>


We have described NMOS above and symmetrically there is PMOS, but in fact we seldom use PMOS due to worse feature and higher price. It can be a giant gap between PMOS and NMOS even they use same technics craft and have same voltage level, the table below show a contrast between PMOS and NMOS both using TI 20-V NexFET™ craft, we can see PMOS is worse in on-region characteristic and switching characteristic. You may wonder why, now we look back to the core of MOSFET's principle: conductive channnal. PMOS's channal is formed by P-type semiconductors whose carrier is holes meanwhile NMOS use eletrons as its carrier. Due to the craft and physical characteristic, the holes have a weaker ability to carry current flow and more expensive to be made.


<table width="100%" border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td align="center"><img src="https://github.com/LEg-er/A-Brief-Introduction-To-MOSFET/blob/main/Images/20-V%20N-Channel%20NexFET%E2%84%A2%20Power%20MOSFET.png?raw=true" width="400" /> </td>
    <td align="center"><img src="https://github.com/LEg-er/A-Brief-Introduction-To-MOSFET/blob/main/Images/20-V%20P-Channel%20NexFET%E2%84%A2%20Power%20MOSFET.png?raw=true" width="400" /></td>
  </tr>
  <tr>
    <td align="center">Fig.1 TI 20-V N-Channel NexFET™ Power MOSFET </td>
    <td align="center">Fig.2 TI 20-V P-Channel NexFET™ Power MOSFET </td>
  </tr>
<table>


##Summary
Now you have a general image on MOSFET. I'll share more eletronic knowledge in my bolg and next time I'll introduce BUCK circuit and other application of MOSFET. You'll have to wait and see!


See you next time!




# Telescopic_Amplifier

In this project we will show the design of a single ended "Telescopic Amplifier". 
we will use CMOS general pdk 90nm (gpdk90) technology by Cadence. 

**Specifications**
* $Gain = 1000 = 60dB$
* $I_{ref} = 10uA$
* $V_{AA} = 2V$
* $V_{out,CM}$ range $(0.6,1.2)V$
* $C_{L} = 10[pF]$ 

Spec will hold cross corners - TT, SS, FF and temperatures = [-40, 25, 125]

## Circuit Architecture, Gain, and Biasing
Taken from Razavi's book - Design of analog CMOS integrated circuits - 

<img src="https://github.com/dsapir4422/Telescopic_Amplifier/assets/87266625/001ee7db-3a02-4f9c-8273-290d1a07ac05" alt="Image Alt Text" width="250" height="250" />

We will use the below circuit but with some changes - 
* PMOS stage, where M4 is the input (Vin), M3 is added for a cascode amplifier stage and M2,M1 are the cascode current source.
* Short Vout to Vin for introducing a buffer single ended stage

**Gain** - 
Looking from Vout to either PMOS or NMOS side, we have a cascode structure and therefore - $R_{out,p}$ = $g_{m,p}*r_{o,p}^2$ in parallel to $R_{out,n}$ = $g_{m,n}*r_{o,n}^2$

Assuming M1,M2 and M3,M4 are identical - $A_v$ = $\frac{-(g_m*r_o)^2}{2}$

otherwise - $A_v$ = $g_{m4}*(g_{m4}r_{o4}r_{o3})||(g_{m1}r_{o1}r_{o2})$

**Biasing** - 
Simulating gpdk90, we saw that $V_{th} = 0.5[V]$ roughly for PMOS, NMOS. Assuming $V_{ov} = 0.2[V]$ for a good current mirror - 
* **Vb1** : We will use a current mirror to copy the 10uA current to M1 gate, therefore $V_{b1} = V_{gs,cm} \approx 0.8[V]$
* **Vb2** : $V_{b2,min} = V_{ov1} + V_{gs2} = V_{ov1} + V_{ov2} + V{th,n} \approx 0.9 $
* **Vb3** : $V_{b3,max} = V_{AA} - (V_{ov4} + V_{gs3}) = V_{AA} - (V_{ov4} + V_{ov3} + V_{th,p}) \approx 1.1[V]$
* **Vb4** : $V_{b4,max} = V_{AA} - V_{sg4} = V_{out} \approx 1.2[V]$

Although, we will add 100-150mV margin for corners

## Circuit Design
Initial design will be with ideal power supply at TT corner - 
![image](https://github.com/dsapir4422/Telescopic_Amplifier/assets/87266625/f3032124-efb5-4037-84df-04f290def9d7)

For supporting corners we will add a biasing network based on $I_{ref}$ current copying, where we will use NMOS for biasing the NMOS transistors (M1,M2) and PMOS for biasing the PMOS transistors (M3,M4) - 
![image](https://github.com/dsapir4422/Telescopic_Amplifier/assets/87266625/ceb766c7-cdc8-4ee5-9310-c01b1dae064c)

Telescopic amplifier with biasing network NET's - 
![image](https://github.com/dsapir4422/Telescopic_Amplifier/assets/87266625/062d10b3-4447-46f9-b0c9-1ec5356aaf7d)

Full circuit - 
![image](https://github.com/dsapir4422/Telescopic_Amplifier/assets/87266625/15d7d6a4-e809-438f-bf8d-56204ec8100e)


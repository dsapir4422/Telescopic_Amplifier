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
* PMOS stage, so M4 is the input (Vin), M3 is added for a cascode amplifier stage and M2,M1 are the cascode current source.
* Short Vout to Vin to introduce a buffer single ended stage

**Gain** - 

Looking from Vout to either PMOS or NMOS side, we have a cascode structure and therefore - $R_{out,p}$ = $g_{m,p}*r_{o,p}^2$ in parallel to 

$R_{out,n}$ = $g_{m,n}*r_{o,n}^2$

assuming M1,M2 and M3,M4 are identical - $A_v$ = $\frac{-(g_m*r_o)^2}{2}$

otherwise - $A_v$ = $g_{m4}*(g_{m4}r_{o4}r_{o3})||(g_{m1}r_{o1}r_{o2})$

**Biasing** - 

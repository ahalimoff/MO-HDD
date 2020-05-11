# -*- coding: utf-8 -*-
"""
Created on Sat Jun 15 18:38:50 2019

@author: ahl
"""

import numpy as np
import matplotlib.pyplot as plt


from gekko import GEKKO

m= GEKKO()


######Costs
C_fuel=0.004 #USD $/kWh fuel cost
C_ins=26 #USD $/m3 insulation
C_floor=26 #USD $/m3 insulation
C_roof=26  #USD $/m3 insulation
C_hp=600 #USD $/kW heat pump cost per kW
C_sc=200 #USD $/m2 flat-plate solar collector 
C_sc_DHW=300 #USD $/m2 flat-plate solar collector 
C_pv=340 #USD $/m2 PV panels
C_win=70 #USD $/(W/(m2*K)) windows cost per U value
C_el=0.029 #USD $/kWh cost of electricity
C_ung_sc=80 #USD $/m2 unglazed flat-plate solar collector
C_ceiling=26

##### Parameters of heating systems
etta_fuel=0.8 # efficiency of boiler
etta_hs=0.8 # heat transmittance systems
##############################################

#### Surface of envelopes ############
A_win=17.6 #m2
A_wall=172.8 #m2
A_r=151.2 #m2
A_c=131.7 #m2
A_rs=30 #m2
A_f=131.7 #m2
A=A_f+A_c+A_wall+A_win # surface of external envelopes
################################################################

##### Height ############################################
P_h=3.2 #m
###########################################################

#### Air changes per hour ##############################
ACH=0.5 #h-1
########################################################
#################################################################


####################

##### Heat pump system #############
COP=3.0 # COP of Heat Pump
####################################


hdd=np.array([1802,	2084,	2385,	2536,	2545,	2559,	2566,	2571,	2604,	2639,	2698,	3009,	3550])
pv=np.array([1582, 1572, 1589, 1404, 1442, 1577, 1455, 1496, 1320, 1559, 1329, 1544, 1473])
ghi=np.array([1789, 1782, 1766, 1610, 1644, 1752, 1604, 1666, 1510, 1685, 1507, 1679, 1581])

RR=0 #region from 0 to 12 in total 13 region
Level=1 #Level of insulation 
##### Solar radiation ########
H_0=ghi[RR] #kWh/m2 #Global horizontal radiation
####### HDD ##########
HDD=hdd[RR]  # degree-days
##### PV panel performance ########
P_0=pv[RR] #kWh/m2/year #Global horizontal radiation
#PV 1582, 1572, 1589, 1404, 1442, 1577, 1455, 1496, 1320, 1559, 1329, 1544, 1473
#GHI 1789, 1782, 1766, 1610, 1644, 1752, 1604, 1666, 1510, 1685, 1507, 1679, 1581

#####R-value of envelopes#####################################
n=1

walls=[[0.75, 0.94, 0.94],[1.4, 1.8, 2.2],[2.2, 2.6, 3.0]]
ceiling=[[1.2*n, 1.4*n, 1.6*n], [2.1*n, 2.6*n, 3.2*n], [3.2*n, 3.7*n, 4.2*n]]
floor=[[1.7*n, 2.0*n, 2.4*n],[1.8*n, 2.3*n, 2.8*n],[2.8*n, 3.2*n, 3.6*n]]
roof=[[0.19, 0.19, 0.19], [0.19, 0.19, 0.19], [0.19, 0.19, 0.19]]
windows=[[0.39,0.39,0.39],[0.39,0.39,0.42],[0.42,0.42,0.53]]
attic_sides=[[0.75, 0.94, 0.94],[1.4, 1.8, 2.2],[2.2, 2.6, 3.0]]

if Level==1 and HDD<2000:
    R_win0=windows[0][0] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[0][0] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[0][0] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[0][0] #m2*K/W  
    R_wall0=walls[0][0] #m2*K/W
    R_rs0=attic_sides[0][0] #m2*K/W
if Level==1 and 2000<HDD<3000:
    R_win0=windows[0][1] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[0][1] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[0][1] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[0][1] #m2*K/W  
    R_wall0=walls[0][1] #m2*K/W
    R_rs0=attic_sides[0][1] #m2*K/W
if Level==1 and HDD>3000:
    R_win0=windows[0][2] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[0][2] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[0][2] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[0][2] #m2*K/W  
    R_wall0=walls[0][2] #m2*K/W
    R_rs0=attic_sides[0][2] #m2*K/W
    
if Level==2 and HDD<2000:
    R_win0=windows[1][0] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[1][0] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[1][0] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[1][0] #m2*K/W  
    R_wall0=walls[1][0] #m2*K/W
    R_rs0=attic_sides[1][0] #m2*K/W
if Level==2 and 2000<HDD<3000:
    R_win0=windows[1][1] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[1][1] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[1][1] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[1][1] #m2*K/W  
    R_wall0=walls[1][1] #m2*K/W
    R_rs0=attic_sides[1][1] #m2*K/W
if Level==2 and HDD>3000:
    R_win0=windows[1][2] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[1][2] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[1][2] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[1][2] #m2*K/W  
    R_wall0=walls[1][2] #m2*K/W
    R_rs0=attic_sides[1][2] #m2*K/

if Level==3 and HDD<2000:
    R_win0=windows[2][0] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[2][0] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[2][0] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[2][0] #m2*K/W  
    R_wall0=walls[2][0] #m2*K/W
    R_rs0=attic_sides[2][0] #m2*K/W
if Level==3 and 2000<HDD<3000:
    R_win0=windows[2][1] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[2][1] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[2][1] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[2][1] #m2*K/W  
    R_wall0=walls[2][1] #m2*K/W
    R_rs0=attic_sides[2][1] #m2*K/W
if Level==3 and HDD>3000:
    R_win0=windows[2][2] #m2*K/W Level I and II 0.39 Level III 0.43 2000<HDD<3000 
    R_c0=ceiling[2][2] #m2*K/W  Level I = 1.2n, Level II =2.1n, Level III=3.2n 
    R_floor0=floor[2][2] #m2*K/W Level I 1.7n Level II 1.8n Level III 2.8n 
    R_r0=roof[2][2] #m2*K/W  
    R_wall0=walls[2][2] #m2*K/W
    R_rs0=attic_sides[2][2] #m2*K/W
    

k_ce=0.04
k_fl=0.04
k_r=0.035
k_wall=0.04


###### Economic factors
g=0.17 #% infliation
i=0.16 # % interest rate
N=30 # years
if i>g:
    r=(i-g)/(1+g)
    PVF=((1+r)**N-1)/(r*(1+r)**N) # present value factor
if i<g:         
    r=(g-i)/(1+i)
    PVF=((1+r)**N-1)/(r*(1+r)**N) # present value factor
else:         
    r=(g-i)/(1+i)
    PVF=N/(1+i) # present value factor

print(PVF)
#########################################################

#####Annual DHW heating 50 degC
V=40 #liter/day
n_d=350 #days
n_p=5 #persons
Q_water= 3000 #0.98*V*n_d*n_p #kWh/year

#####Electricity consumption ##########

E_el=12*n_p*100 # kWh/year 


#### Surface ratio
f_w=A_win/(A_win+A_wall) # ratio of surface of windows to the total surface of external walls and windows
f_rs=A_rs/(A_r+A_rs) #ratio of sides of the attic to the total surface of the attic
f_c=A_c/(A_r+A_rs) # ratio of ceiling surface to the total attic area


########### Parameters #######
########### Parameters #######

E_PV= m.FV(value=0)
E_PV.STATUS=1
#U_t.DCOST=0

R_win= m.FV(value=0)
R_win.STATUS=1
#U_t.DCOST=0

R_wall= m.FV(value=0)
R_wall.STATUS=1
#dE_h.DCOST=0

R_c= m.FV(value=0)
R_c.STATUS=1
#dE_E.DCOST=0

R_floor= m.FV(value=0)
R_floor.STATUS=1
#dE_E.DCOST=0

R_r= m.FV(value=0)
R_r.STATUS=1
#dE_E.DCOST=0

R_rs= m.FV(value=0)
R_rs.STATUS=1
#dE_E.DCOST=0

R_rs= m.FV(value=0)
R_rs.STATUS=1
#dE_E.DCOST=0

U_ew= m.FV(value=0)
U_ew.STATUS=1
#dE_E.DCOST=0

U_f= m.FV(value=0)
U_f.STATUS=1
#dE_E.DCOST=0

U_r= m.FV(value=0)
U_r.STATUS=1
#dE_E.DCOST=0

U= m.FV(value=0)
U.STATUS=1
#dE_E.DCOST=0

Q_DHW= m.FV(value=0)
Q_DHW.STATUS=1
#dE_E.DCOST=0

Q_combi= m.FV(value=0)
Q_combi.STATUS=1
#dE_E.DCOST=0

Q_heat= m.FV(value=0)
Q_heat.STATUS=1
#dE_E.DCOST=0

Q_ther= m.FV(value=0)
Q_ther.STATUS=1
#dE_E.DCOST=0

C_h= m.FV(value=0)
C_h.STATUS=1
#dE_E.DCOST=0

C_ae= m.FV(value=0)
C_ae.STATUS=1
#dE_E.DCOST=0

C_t= m.FV(value=0)
C_t.STATUS=1
#dE_E.DCOST=0

M_CO2= m.FV(value=0)
M_CO2.STATUS=1
#dE_E.DCOST=0

M_CO2_el= m.FV(value=0)
M_CO2_el.STATUS=1
#dE_E.DCOST=0

C_M= m.FV(value=0)
C_M.STATUS=1
#C_M.DCOST=0

tau_d= m.FV(value=0)
tau_d.STATUS=1
#C_M.DCOST=0

q= m.FV(value=0)
q.STATUS=1
#C_M.DCOST=0


LCC= m.FV(value=0)
LCC.STATUS=1
#C_M.DCOST=0

m_co2= m.FV(value=0)
m_co2.STATUS=1
#C_M.DCOST=0

c_t= m.FV(value=0)
c_t.STATUS=1
#C_M.DCOST=0

U_win= m.FV(value=0)
U_win.STATUS=1
#C_M.DCOST=0

x1=m.Var(value=0.0,lb=0.0) #Insulation thickness, m
#x1.STATUS=1
#x1.DCOST=0

x2= m.Var(value=0.0,lb=0.00) #Surface area of unglazed flat-plate solar collectors m2
#x2.STATUS=1
#x2.DCOST=0

x3=m.Var(value=0.0,lb=0.00) #Surface area of unglazed flat-plate solar collectors m2
#x3.STATUS=1
#x3.DCOST=0

x5=m.Var(value=0.0,lb=0.00) #Surface area of PV panels m2
#x4.STATUS=1
#x4.DCOST=0

x7=m.Var(value=0.0,lb=0.0) #Surface area of PV panels m2
#x4.STATUS=1
#x4.DCOST=0

x8=m.Var(value=0.0,lb=0.0) #Surface area of PV panels m2
#x4.STATUS=1
#x4.DCOST=0

x9=m.Var(value=0.0,lb=0.0) #Surface area of PV panels m2
#x4.STATUS=1
#x4.DCOST=0
#x5=m.Var(value=0,lb=0,ub=4) #Electrical power consumption of HP kW


#R-value after retrofitting
R_win=R_wall0+x1 #
R_c=R_c0+x2/k_ce #
R_floor=R_floor0+x3/k_fl #
#R_r=R_r0+x4/k_r #
R_wall=R_wall0+x5/k_wall #
#R_rs=R_rs0+x6/k_wall #



####Before retrofitting
U_ew0=1/R_wall0
U_win0=1/R_win0
U_f0=1/R_floor0
U_r0=1/R_c0
#U_ew0=(R_win0*(1-f_w)+f_w*R_wall0)/(R_win0*R_wall0)
#U_f0=1/R_floor0
#U_r0=((R_rs0*A_r+R_r0*A_rs)/(R_r0*R_rs0*A_c+R_c0*(R_rs0*A_r+R_r0*A_rs)))
#U_r0=(R_rs0*(1-f_rs)+f_rs*R_r0)/(R_r0*R_rs0*f_c+2*R_c0*(R_rs0*(1-f_rs)+f_rs*R_r0))
U0=(U_ew0*A_wall+R_win0*A_win+U_f0*A_f+U_r0*(A_c))/A # U-value of the building

###Heat load
Q_heat0=(0.34*ACH*A_f*P_h+U0*A)*0.024*HDD		#kWh/year


###Total thermal energy load
Q_ther0=(Q_heat0/etta_hs+Q_water)/(etta_hs) # kWh/year

#####Cost of heating
C_h0=Q_ther0*C_fuel/(etta_fuel) #USD $/year

#####Cost of electricity
C_ae0=E_el*C_el #USD $/year

#####Total cost
C_t0=C_h0+C_ae0 #USD $/year
c_t0=C_t0/A_f # $/m2/year

#### CO2-emission
myu_f=0.369 #kg/kWh
myu_el=0.489 #kg/kWh

M_CO20=myu_f*Q_ther0/etta_fuel+myu_el*E_el  #kg/year
m_co20=M_CO20/A_f # kg/m2*year

####After retrofitting################################

m.Equation(U_ew==1/R_wall)
m.Equation(U_win==1/R_win)
m.Equation(U_f==1/R_floor)
m.Equation(U_r==1/R_c)            #(R_rs*(1-f_rs)+f_rs*R_r)/(R_r*R_rs*f_c+2*R_c*(R_rs*(1-f_rs)+f_rs*R_r)))
           #((R_rs*A_r+R_r*A_rs))/(R_r*R_rs*A_c+R_c*(R_rs*A_r+R_r*A_rs)))
m.Equation(U==(U_ew*A_wall+U_win*A_win+U_f*A_f+U_r*(A_c))/A) # U-value of the building()

###Heat load
m.Equation(Q_heat==(0.34*ACH*A_f*P_h+U*A)*0.024*HDD)		#kWh/year

####DHW and combi-system
m.Equation(Q_DHW==0.44*H_0*x7) #kWh/year
m.Equation(Q_combi==0.33*H_0*x8) #kWh/year

#####PV panel
r=0.15 # efficiency
P_r=0.75 # ratio

m.Equation(E_PV==x9*r*P_0*P_r) # kWh/year

###Total thermal energy load
m.Equation(Q_ther==((Q_heat-Q_combi)/etta_hs+Q_water-Q_DHW)/(etta_hs)) # kWh/year

#####Cost of heating
m.Equation(C_h==Q_ther*C_fuel/(etta_fuel)) # USD $/year

#####Cost of electricity
m.Equation(C_ae==(E_el-E_PV)*C_el) # USD $/year

#####Total cost of energy
m.Equation(C_t==C_h+C_ae) # USD $/year

m.Equation(c_t==(C_h+C_ae)/A_f) #USD $/year
#### CO2-emission
m.Equation(M_CO2==myu_f*Q_ther/etta_fuel)  #kg/year
m.Equation(M_CO2_el==myu_el*(E_el-E_PV))  #kg/year
m.Equation(m_co2==(M_CO2_el+M_CO2)/A_f)  #kg/year
#####Material cost
m.Equation(C_M==x1*C_win*A_win+x2*C_ceiling*A_c+x3*C_floor*A_f+x5*C_ins*A_wall+x7*C_sc_DHW+x8*C_sc+x9*C_pv)

m.Equation(x7+x8+x9<=A_r/2)

#m.Equation(tau_d==math.log(abs(1-r*C_M/(-C_t0+C_t)))/math.log(abs(1-r))) #years
m.Equation(tau_d==C_M/(C_t0-C_t)) #years
m.Equation(q==((Q_heat-Q_combi)/etta_hs)/A_f)
m.Equation(M_CO2>=0)
m.Equation(M_CO2_el>=0)
m.Equation(Q_heat-Q_combi>=0)
m.Equation(Q_water-Q_DHW>=0)
m.Equation(E_el-E_PV>=0)
m.Equation(Q_ther>=0)
m.Equation(LCC==0.001*(C_t*PVF+C_M))
#m.Obj(C_t*PVF+C_M)
#m.Obj(C_M/(C_t0-C_t))
m.Obj(C_M)
m.Obj(-(Q_heat0-Q_heat))
m.Obj(-Q_DHW)
#m.Obj(Q_ther)
m.Obj(-(E_el-E_PV))
m.Obj(-(Q_combi))
m.Obj(M_CO2)
m.Obj(M_CO2_el)

m.options.IMODE = 3
m.solve()          
#print('')
print(HDD)
print(Level)
print(str(LCC.value))
print(str(x1.value))
print(str(x2.value))
print(str(x3.value))
#print(0)
print(str(x5.value))
#print(0)
print(str(x7.value))
print(str(x8.value))
print(str(x9.value))
print(str(U.value))   
print(U0)  
print(str(q.value))   
print(Q_heat0/(etta_hs*A_f))
print(str(c_t.value))   
print(c_t0)
print(str(m_co2.value))
print(m_co20)
print(str(C_M.value))   
print(str(tau_d.value))

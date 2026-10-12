# 660 	 Diesel fuel

A unit injector operated by the engine camshaft meters and injects the fuel into the combustion chamber at high pressure at the proper time.

In addition to a noticeable odor, the exhaust from the diesel engine contains gaseous and particulate emissions which contribute to air pollution. The particles, or soot, may be removed by a trap oxidizer that consists of a filter and a regeneration system, which burns the trapped particles and cleans the filter. Gaseous emissions of unburned hydrocarbons (HC), carbon monoxide (CO), and oxides of nitrogen (NO$_{x}$) may be controlled through the use of electronically controlled fuel injection, exhaust-gas recirculation, and charge-air cooling. Operating the engine on low-sulfur fuel reduces sulfur and particulate emissions. SEE AIR POLLUTION; DIESEL FUEL; FUEL INJECTION. [D.A.M.]

# Diesel fuel

A broad mixture of hydrocarbons produced as distillates, as residual materials, or as blends of the two during the refining of crude petroleum. Diesel fuel usually has a distillation range of 390–715 $^{\circ}$F (200–380 $^{\circ}$C) and a specific gravity range of 0.760–0.935 [equivalent to 61.2–19.8 on the American Petroleum Institute (API) scale]. In addition to these properties, diesel fuel must have <1 wt % sulfur, <0.1 wt % ash, <0.5 vol % water and sediment, and a high flash point (greater than 131 $^{\circ}$F or 55 $^{\circ}$C).

Diesel fuel quality is defined by the cetane number, which usually falls into the range 30–50. A high cetane number indicates the potential for easy starting and smooth operation of the engine. The cetane number is the analog of the automobile engine octane number, with cetane (n-hexadecane, C$_{16}$H$_{34}$) having the arbitrarily assigned value of 100. At the other end of the scale, heptamethylnonane, an isomer of cetane, has the assigned cetane number of 0. The cetane number of a diesel fuel is determined by comparison with blends of cetane and heptamethylnonane. It corresponds to the number of parts by volume of cetane in a cetane–heptamethylnonane blend which has the same ignition quality as the fuel. SEE CETANE NUMBER.

The American Society for Testing and Materials (ASTM) has categorized diesel fuels into three general groups. The need to categorize these fuels results from the varied uses of diesel engines, which are designed to operate efficiently on one of the standard diesel fuels. SEE DIESEL ENGINE.

No. 1-D is a light distillate, similar to kerosine, for engines where frequent load changes and speed changes (truck, tractor engines) are essential. This fuel has a flash point greater than 100 $^{\circ}$F (38 $^{\circ}$C), with a minimum cetane number of 40. This fuel is believed to be particularly suitable for cold-weather operation. SEE KEROSENE.

No. 2-D is a medium distillate fuel with a lower volatility and higher density than No. 1-D. This fuel finds use in heavier-duty engines, for example, railroad engines, which operate at uniform speeds but with heavier loads than encountered during the use of No. 1-D. The flash point is greater than 125 $^{\circ}$F (52 $^{\circ}$C) and the minimum cetane number is 40.

No. 3-D is a heavy distillate fuel with the highest density and lowest volatility of the three diesel fuels. It finds use in low- and medium-speed engines such as marine engines and electric power generator engines, which operate under sustained loads. The flash point is greater than 130 $^{\circ}$F (54 $^{\circ}$C) and the minimum cetane rating is 30. [J.G.S.]

# Difference equation

A relationship between one or more independent variables, one or more dependent variables, and differences of those variables. Difference equations arise in the analysis of discrete systems (for example, a string loaded along its length with small masses), in the solution of differential equations by means of digital computers, in the implementation of digital filters, and in the discrete-time control of systems. An ordinary difference equation expresses a relationship between an independent variable *t* and one or more dependent vari-ables, *y*(*t*), *u*(*t*), and so forth, and any successive differences of *y*, *u*, . . . . The first forward difference of *y*$_{i}$, relative to the increment *h*, is defined by Eq. (1). The second forward difference can be obtained by applying the above definition to itself, as in Eq. (2).

```
$$
\Delta y(t) = y(t+h)-y(t) \tag{1}
\Delta^2 y(t) = \Delta[\Delta y(t)]
= \Delta y(t+h)-\Delta y(t)
= [y(t+2h)-y(t+h)]
-[y(t+h)-y(t)]
= y(t+2h)-2y(t+h)+y(t) \tag{2}
$$
```

A difference equation is linear if it is of the first degree with respect to all the quantities $\Delta y(t)$, $\Delta^2 y(t)$, $\Delta^3 y(t)$, . . . . The general solution of difference equations is possible only for the case where they are linear with constant coefficients. However, non-linear difference equations arise naturally in the solution of non-linear differential equations. Likewise, the numerical solution of a partial differential equation leads to a partial difference equation. Methods exist for approximating governing equations for linear continuous-time systems by difference equations.

# Linear constant-coefficient equations

The independent variable of a difference equation will usually have discrete values. Then the notation can be simplified by making the substitution in Eq. (3). In this case, the arguments of the independent variables, if more than one, can be replaced by the subscript *k*. Then, the forward difference operators given by Eqs. (1) and (2) can be written as Eqs. (4), where the shifting operator *E* has been defined, incrementing the index on the dependent variable by 1. Each time *E* is applied.

```
$$
 t_k = t_0 + kh \tag{3}
 k = 0, 1, 2, \dots
$$
```

```
$$
 \Delta y_k = y_{k+1} - y_k = E y_k - y_k
 \Delta^2 y_k = E^2 y_k - 2Ey_k + y_k \tag{4}
$$
```

The general homogeneous, linear, constant-coefficient difference equation of order *n* can be written in terms of the shifting operator as Eq. (5). From the solution of linear, constant-coefficient differential equations, the solution is assumed to be of the form $e^k = \beta^k$, where *r* is a suitably chosen constant and $\beta = e^r$. From the definition of the shifting operator, Eqs. (6)

```
$$
 E^n y_k + A_1 E^{n-1} y_k + \cdots + A_{n-1} E y_k + A_0 y_k = 0 \tag{5}
 k \geq 0
$$
```

```
$$
 E\beta^k = \beta^{k+1} = \beta(\beta^k)
 E^2\beta^k = \beta^{k+2} = \beta^2(\beta^k) \tag{6}
$$
```

follow, as well as similar equations for higher powers of *E*. When these equations are substituted into Eq. (5), the result is Eq. (7).

```
$$
 \beta^n + A_1\beta^{n-1} + \cdots + A_{n-1}\beta + A_0 = 0 \tag{7}
$$
```

Hence, *y*_k = $\beta^k$ will satisfy Eq. (5) if $\beta$ is a root of Eq. (7). When all roots are real and distinct, the most general expression satisfying Eq. (5) is Eq. (8), where $\beta_1$, $\beta_2$, . . . , $\beta_n$ are the roots to Eq. (7) and *y*_k = $c_1\beta_1^k + c_2\beta_2^k + \cdots + c_n\beta_n^k$. *c*$_1$, *c*$_2$, . . . , *c*$_n$ are constants to be determined by the initial conditions. SEE ALGEBRA.

```
$$
 k \geq 0 \tag{8}
$$
```
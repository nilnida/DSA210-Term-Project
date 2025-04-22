# DSA210-Term-Project

In this project, I will work on the effect of temperature on battery efficiency and try to predict remaining useful lifetime behavior. By doing so, I aim to use my conclusions to create solutions to achieve effective usage of batteries in daily life. The plan is to use the main dataset that shows the relation of different operation type variables and the ambient temperature as the main source and support it with a different dataset that shows the battery chemistry relation with the changing temperature. Also, during the analysis, some other indicators will be derived from the existing data for further exploration.

---

## Table of Contents
- [Motivation](#motivation)
- [Data Sources](#data-sources)
- [Hypotheses](#hypotheses)
- [Data Analysis Techniques and Stages](#data-analysis-techniques-and-stages)

---

## Motivation

In the rapid revolutions occuring in technology today, the adoption of lithium-ion batteries stands as an important building block especially when we think of electrically powered devices, electric vehicles and renewable energy storage systems. Since the reliance on battery technologies increases more and more, understanding the behavior becomes more of an interest area. The widespread use of the lithium-ion batteries raises both safety and economic concerns. To be able to offer accurate solutions, it is important to analyze data. Hence, it becomes possible to optimize the battery performance and predict the lifespan of a functioning battery.

Battery efficiency, reliability, lifespan and safety relies on multiple factors but one of the critical ones is the temperature stemming from the chemical nature of lithium-ion batteries. In general, it is known that when batteries are exposed to high temperatures, their capacity and performance consistency decreases while safety risks increases. However, the infuence of the temperature is still an ongoing research area since there is no concrete explanation showing the effect of variations in temperature on battery performance metrics.

This project will systematically reveal the relations between temperature, battery chemistry, and performance providing a general understanding. Hence, it is going to be possible to offer practical real-life solutions regarding battery management and optimization.

---

## Data Sources

### 1)  **Batteries Data Set Provided by PCoE:**

The main data set of this project is the publicly available lithium-ion battery data set provided by NASA Prognostics Center of Excellence (PCoE). This data set consists of several different batteries tested under controlled laboratory conditions. There are 3 operational modes that the data set consists of. I downloaded the data set as a Matlab file and here is the data set structure:

```
cycle: Top level structure array containing the charge, discharge and impedance operations

  type: Operation type
  ambient_temperature: Ambient temperature (°C)
  time: The date and time of the start of the cycle, in MATLAB date vector format
  data: Data structure containing the measurements

    For charge, the fields are:
      Voltage_measured: Battery terminal voltage (Volts)
      Current_measured: Battery output current (Amps)
      Temperature_measured: Battery temperature (°C)
      Current_charge: Current measured at charger (Amps)
      Voltage_charge: Voltage measured at charger (Volts)
      Time: Time vector for the cycle (secs)
  
    For discharge, the fields are:
      Voltage_measured: Battery terminal voltage (Volts)
      Current_measured: Battery output current (Amps)
      Temperature_measured: Battery temperature (°C)
      Current_charge: Current measured at load (Amps)
      Voltage_charge: Voltage measured at load (Volts)
      Time: Time vector for the cycle (secs)
      Capacity: Battery capacity (Ahr) for discharge till 2.7V

    For impedance, the fields are:
      Sense_current: Current in sense branch (Amps)
      Battery_current: Current in battery branch (Amps)
      Current_ratio: Ratio of the above currents
      Battery_impedance: Battery impedance (Ohms) computed from raw data
      Rectified_impedance: Calibrated and smoothed battery impedance (Ohms)
      Re: Estimated electrolyte resistance (Ohms)
      Rct: Estimated charge transfer resistance (Ohms)
```

### 2)  **Battery Data Set Provided by The Hawaii Natural Energy Institute:**

I plan to integrate the data set provided by the The Hawaii Natural Energy Institute to the analysis. This data set consists of comprehensive lithium-ion battery data, including parameters such as internal resistance, energy density, and degradation rates that may be integrated to the main data set to improve the accuracy of the analysis of the remaining useful life of batteries.

In addition to these two data sets, supplementary indicators will be derived from the existing data such as impedance evolution, rate of voltage drop, cumulative capacity loss, and many others that may enrich the analysis further.

---

## Hypotheses

In order to define the project's research framework, the following null and alternative hypotheses will be tested statistically:

- **Null Hypothesis (H₀)**: Temperature has no relation with the efficiency and remaining useful life of lithium-ion batteries.

- **Alternative Hypothesis (H₁)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

Testing these hypotheses will be the main objective of the analysis phase, with the aim of accepting or rejecting them based on quantitative data analysis and predictive modeling.

---

## Data Analysis Techniques and Stages

The data analysis process will begin with exploratory data analysis (EDA). Initially, statistical techniques and visualizations will identify trends and relationships within the combined datasets. With correlation and regression analysis, relationships between temperature, and battery performance parameters will be established. Subsequently, advanced machine learning methodologies such as regression models, random forest algorithms, and support vector regression will be employed to model and predict battery efficiency and remaining useful life. To derive the already stated supplementary indicators, feature engineering will be used.

The final predictive models will be evaluated based on their accuracy in predicting the remaining useful life and battery efficiency across varying temperature conditions and chemical characteristics.

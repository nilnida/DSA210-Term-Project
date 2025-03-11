# DSA210-Term-Project

In this project, I will work on the effect of temperature on battery efficiency and try to predict remaining useful lifetime behavior. By doing so, I aim to use my conclusions to create solutions to achieve effective usage of batteries in daily life. The plan is to use the main dataset that shows the relation of different operation type variables and the ambient temperature as the main source and support it with a different dataset that shows the battery chemistry relation with the changing temperature. Also, during the analysis, some other indicators will be derived from the existing data for further exploration.

---

## Table of Contents
- [Motivation](#motivation)
- [Data Sources](#data-sources)
- [Data Analysis](#data-analysis)
- [Expected Findings](#expected-findings)
- [Limitations and Future Work](#limitations-and-future-work)

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

### 2)  **Battery Data Set Provided by CALCE:**

To enrich the analysis, additional scientifically credible data from the Battery Materials Property Database, published by reputable sources such as *Scientific Data* and the Center for Advanced Life Cycle Engineering (CALCE), will be integrated. These supplementary datasets include extensive data on various Li-ion battery chemistries and properties, including internal resistance, energy density, voltage profiles, coulombic efficiency, and degradation rates. The combination of these two credible datasets will allow for deeper, more insightful analyses into how battery chemistry and temperature jointly influence battery performance and RUL.

Moreover, additional derived supplementary indicators, such as temperature gradients during charging/discharging cycles, impedance evolution, rate of voltage drop, and cumulative capacity loss, will also be computed from these data to enrich the analysis further.

## Data Analysis
The data analysis process will follow a structured pipeline, beginning with thorough exploratory data analysis (EDA). Initially, statistical techniques and visualizations will identify meaningful trends, relationships, and anomalies within the combined datasets. Correlation and regression analysis will establish baseline relationships between temperature, chemical properties, and battery performance parameters.

Subsequently, advanced machine learning methodologies—including regression models, random forest algorithms, gradient boosting models, and support vector regression—will be employed to model and predict battery efficiency and remaining useful life. Feature engineering will be used to derive supplementary indicators, such as average charge/discharge temperatures, internal impedance variation across battery life cycles, temperature gradients, capacity fade rates, and overall battery aging indicators. These indicators will provide deeper predictive insights into the degradation mechanisms of Li-ion batteries.

Cross-validation methods will ensure model robustness, accuracy, and generalizability. The final predictive models will be evaluated based on their accuracy in predicting RUL and battery efficiency across varying temperature conditions and chemical characteristics.

## Expected Findings
The anticipated findings of this project will deliver detailed and quantitatively supported insights regarding the relationships between temperature, battery chemistry, and battery efficiency metrics. Specifically, it is expected that the analysis will clarify how variations in ambient temperature influence battery degradation (capacity fading and impedance increase) and lifespan, with chemical properties acting as significant moderators.

Additionally, this project aims to produce reliable predictive models that can estimate remaining useful life (RUL) and battery efficiency under different temperature conditions and battery chemistries. These insights and models could directly assist battery manufacturers and system designers in optimizing battery systems, prolonging battery life, enhancing reliability, and reducing both economic and environmental impacts.

## Limitations and Future Work
Despite the comprehensive nature of the datasets utilized, certain limitations exist. The primary data from NASA was collected in controlled laboratory environments, potentially limiting the applicability of the predictive insights to real-world scenarios where environmental conditions are more dynamic and unpredictable. Another limitation lies in potential differences between laboratory battery conditions and real-life battery usage patterns, such as fluctuating loads and irregular charge cycles.

Future extensions of this research may include integrating datasets from real-world scenarios or field experiments (e.g., batteries from electric vehicles or renewable energy storage systems). Moreover, further studies could explore emerging battery chemistries (like lithium-sulfur or solid-state batteries) under extreme operating conditions, thus significantly extending the project's applicability and relevance to future battery technology advancements.

---  

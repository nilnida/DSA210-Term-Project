# DSA210-Term-Project

In this project, I will work on the effect of temperature on battery efficiency and try to predict remaining useful lifetime behavior. By doing so, I aim to use my conclusions to create solutions to achieve effective usage of batteries in daily life. The plan is to use the main dataset that shows the relation of different operation type variables and the ambient temperature as the main source and support it with a different dataset that shows the battery chemistry relation with the changing temperature. Also, during the analysis, some other indicators will be derived from the existing data for further exploration.

---

## Table of Contents
- [Motivation](#motivation)
- [Data Sources](#data-sources)
- [Hypotheses](#hypotheses)
- [Methodology](#methodology)
- [Findings](#findings)
- [Hypotesis Testing](#hypothesis-testing)

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

## Methodology

The methodology of this project consists of three core phases: data processing, data visualization, and hypothesis testing. Each step was carried out in dedicated Jupyter notebooks to ensure modularity and clarity.

### 1) Data Processing

The data processing phase begins with the extraction of structured battery datasets from MATLAB .mat files, specifically B0005.mat. Using scipy.io, the nested cycle structure is accessed, containing detailed measurements for charge, discharge, and impedance phases. Each sub-structure is parsed and reshaped into Python dictionaries and subsequently converted into data frames. After loading each data frame, based on cycle indices, the data is merged to end up with a data frame consisting of useful variables for data analysis.

### 2) Data Visualization

The visualization stage explores patterns and correlations across the operational and environmental variables of the battery. This includes plotting trends over cycles using line and scatter plots to observe metrics such as discharging time, discharge capacity, and battery temperature changes. Lineplots are employed to compare distributions of battery capacity and RUL across temperature bins.  These visualizations are instrumental in guiding the formation of hypotheses and identifying relationships worth statistically validating.

### 3) Hypothesis Testing

This stage involves statistically testing the relationships between temperature and key performance indicators of the battery. This begins with performing correlation tests, two-tailed and one-tailed t-tests, and one-way ANOVA on discharging time over temperature bins. These techniques are used for both battery capacity and remaining useful life as well, in order. Several hypotesis tests are done on each variable to determine teh significancy of the observed effects.

---

## Findings

### 1. Average Charging Time across Charging Cycle Bins

Following graphs investigate how the average charging time evolves throughout the battery’s usage cycles. Charging time is a key indicator of a battery’s health and performance, which may change due to internal resistance buildup or degradation.

![image](https://github.com/user-attachments/assets/e3523cff-4459-4b25-b805-00225cc01049)

![image](https://github.com/user-attachments/assets/90d40245-aa44-459e-94f7-202639b30d99)

There is an increasing trend in general but it does not seem as a good indicator to examine for average charging time since there is no consistency.

### 2. Average Temperature across Charging Cycle Bins

Following graphz highlight how temperature changes during the battery charging process over its lifespan. Since temperature affects chemical reactions, it’s crucial to see if operating temperature increases with wear.

![image](https://github.com/user-attachments/assets/ad3ff0b6-316a-43d4-bd84-f46a5ce6601b)

![image](https://github.com/user-attachments/assets/1a72a5ce-334a-49ee-b65e-086323026f29)

Again, since there is not a strong relation that can be seen in general, examining the relation statistically is not necessary.

### 3. Average Discharging Time across Discharging Cycle Bins

The graphs below evaluate how long it takes to discharge the battery over different usage phases. Discharging time directly relates to how long the battery can hold and deliver energy.

![image](https://github.com/user-attachments/assets/160daeac-40f4-4fe5-a7ff-033a70cc2347)

![image](https://github.com/user-attachments/assets/6faa5b26-5a21-4a09-9ad9-be2de387790a)

Since the trend is consistent with the cycle numbers, this relation is important for the hypotesis testing stage.

### 4. Average Temperature across Discharging Cycle Bins

Following graphs are important to explore thermal behavior during discharge and how it varies over time. Understanding discharging temperature trends helps assess safety and energy efficiency.

![image](https://github.com/user-attachments/assets/43a38956-efe8-4b7a-ac25-626abd322c03)

![image](https://github.com/user-attachments/assets/5b3ea88b-223f-44f1-8b16-6da4975c66e3)

Since the trend is almost consistent, one can find examining the relation between average temperature and average discharge time, evaluated in the previous step, necessary. Discharging time vs battery temperature is the first relation examined in the hypotesis testing part of this project.

### 5. Battery Capacity over Discharging Cycles

Battery capacity is the fundamental efficiency metric to monitor. The following raphs explicitly shows that over the discharging cycles, the battery capacity reduces, which indicates a degraadation in battery efficiency. This is critical for quantifying the effect of aging on battery performance.

![image](https://github.com/user-attachments/assets/b9e9a69b-5154-4397-aa66-a5bb2e85328d)

![image](https://github.com/user-attachments/assets/e65c4477-07db-476f-ba73-c421433ba923)

### 6. Average Battery Capacity across Temperature Bins

To assess how the battery temperature influences the discharge capacity of the battery. Since high temperatures can accelerate chemical reactions and degradation, it's important to understand the thermal impact on energy output.

![image](https://github.com/user-attachments/assets/a12ab9c8-64bc-433e-b605-78b42f4b2f5d)

![image](https://github.com/user-attachments/assets/5f5adf79-0681-4269-8dee-1344a92f5a27)

This relation is the second one to be examined in the hypothesis testing part since there is a visually consistent trend between both variables highlighting the importance of battery capacity in order to decide on the battery efficiency trend.

### 7. RUL across Temperature Bins

To see whether RUL varies significantly with respect to operating temperature, the following graphs are used. Since the null hypothesis examines if there is a relation between battery temperature and remaining useful life (RUL), this graphs are important for the hypothesis testing part as well.

![image](https://github.com/user-attachments/assets/a84b53af-986d-444f-8cc8-2ad49570a138)

![image](https://github.com/user-attachments/assets/2c902fc7-1200-497d-a3e4-f3571d503442)

The relation between battery temperature and remaining useful life (RUL) is the third and the last relation that will be studied in the hypothesis testing part.

### 8. Correlation Analysis on Discharge Results

The ones that are highlighted as key metrics before is examined in a correlation heat map, showing a strong relation between the chosen metrics, opposing the temperature. This evaluation is important since after the hypothesis testing, the outcomes will be consistent with this visualization.

![image](https://github.com/user-attachments/assets/f021c0eb-5b21-4ea7-bd4d-db14162126f5)

---

## Hypotesis Testing







# DSA210-Term-Project

In this project, I will work on the effect of temperature on battery efficiency and try to predict remaining useful lifetime behavior. By doing so, I aim to use my conclusions to create solutions to achieve effective usage of batteries in daily life. The plan is to use the main dataset that shows the relation of different operation type variables and the ambient temperature as the main source and support it with a different dataset that shows the battery chemistry relation with the changing temperature. Also, during the analysis, some other indicators will be derived from the existing data for further exploration.

---

## Table of Contents
- [Motivation](#motivation)
- [Data Sources](#data-sources)
- [Hypotheses](#hypotheses)
- [Methodology](#methodology)
- [Visualization Findings](#visualization-findings)
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

- **Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

- **Alternative Hypothesis (H₁)**: Temperature has no relation with the efficiency and remaining useful life of lithium-ion batteries.

Testing these hypotheses will be the main objective of the analysis phase, with the aim of accepting or rejecting them based on quantitative data analysis and predictive modeling.

---

## Methodology

The methodology of this project consists of three core phases: data processing, data visualization, and hypothesis testing. Each step was carried out in dedicated Jupyter notebooks to ensure modularity and clarity.

### 1) Data Processing

The data processing phase begins with the extraction of structured battery datasets from MATLAB .mat files, specifically B0005.mat. Using scipy.io, the nested cycle structure is accessed, containing detailed measurements for charge, discharge, and impedance phases. Each sub-structure is parsed and reshaped into Python dictionaries and subsequently converted into data frames. After loading each data frame, based on cycle indices, the data is merged to end up with a data frame consisting of useful variables for data analysis.

### 2) Data Visualization

The visualization stage explores patterns and correlations across the operational and environmental variables of the battery. This includes plotting trends over cycles using line and scatter plots to observe metrics such as discharging time, discharge capacity, and battery temperature changes. Lineplots are employed to compare distributions of battery capacity and RUL across temperature bins.  These visualizations are instrumental in guiding the formation of hypotheses and identifying relationships worth statistically validating.

### 3) Hypothesis Testing

This stage involves statistically testing the relationships between temperature and key performance indicators of the battery. This begins with performing correlation tests, two-tailed and one-tailed t-tests, and one-way ANOVA on discharging time over temperature bins. These techniques are used for both battery capacity and remaining useful life as well, in order. Several hypotesis tests are done on each variable to determine the significancy of the observed effects.

---

## Visualization Findings

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

### 1. Relation of Battery Efficinecy with Battery Temperature

Since in the data, there exists two metrics that shows the battery efficiency, there will be two parts that hypotesis tests are conducted on. At the end, the results will be evaluated to make a conclusion.

#### a. Relation of Discharge Duration with Battery Temperature

#### Pearson Correlation Test for Discharge Duration in Relation with Temperature

**Null Hypothesis:** No linear correlation between battery temperature and discharge duration.

**Alternative Hypothesis:** There is a significant linear correlation.

###### Findings

- Correlation Coefficient (r): -0.7586681656065123
- P-Value: 1.0388933158394018e-32
- Reject the null hypothesis, proving that there is a significant linear correlation between battery temperature and discharge duration.

![image](https://github.com/user-attachments/assets/175fad49-ffd3-45cf-87ff-6760dd4ad28e)

#### Spearman Correlation Test for Discharge Duration in Relation with Temperature

**Null Hypothesis:** No monotonic relationship between battery temperature and discharge duration.

**Alternative Hypothesis:** There is a significant monotonic correlation.

###### Findings

- Correlation Coefficient (ρ): -0.765188979606299
- P-Value: 1.4419679611288852e-33
- Reject the null hypothesis, proving that there is a strong monotonic relation between battery temperature and discharge duration.

![image](https://github.com/user-attachments/assets/aa7f40e6-108d-4250-aeeb-a8e5e547fee4)

#### Two-Tailed T-Test for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis:** The mean discharge duration is the same in both groups.

**Alternative Hypothesis:** The mean discharge duration is different between the groups.

###### Findings

- T-Statistic: 19.345736701918707
- P-Value: 1.1254142603243133e-42
- Reject the null hypothesis, proving that the mean discharge duration is different between the groups.

#### One-Tailed T-Test for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis:** The mean discharge duration in the low temperature group is less than or equal to the high temperature group.s.

**Alternative Hypothesis:** The mean discharge duration is greater in the low temperature group.

###### Findings

- T-Statistic: 19.345736701918707
- One-Tailed P-Value: 5.627071301621567e-43
- Reject the null hypothesis, proving that the mean discharge duration is greater in the low temperature group.

![image](https://github.com/user-attachments/assets/1c740229-a5d3-4092-8647-e6ba42a3e27b)

![image](https://github.com/user-attachments/assets/506ff738-1fbd-4957-adb5-4cedd0808181)

#### One-Way ANOVA for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis:** Mean discharge duration is equal across all temperature bins.

**Alternative Hypothesis:** At least one group differs.

###### Findings

- F-Statistic = 68.22562456047194
- P-Value = 2.552793322562453e-22
- Reject the null hypothesis, proving that at least one group mean discharge duration is different than the others.

![image](https://github.com/user-attachments/assets/e9304850-f407-486c-bcba-cebd34c01ddb)

![image](https://github.com/user-attachments/assets/deb82f12-d562-4f6a-a06e-c1357070cf67)

When all of the steps in the analysis of the battery discharge duration relation with battery temperature are examined, one can say that there is a strong negative relation that shows in the lower temperatures, the battery discharge duration is higher and while the temperature rises, the battery discharge duration lowers. This conclusion strenghtens out null hypothesis which is:

**Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

To make sure, one must continue with the other steps of the hypothesis testing.

#### b. Relation of Battery Capacity with Battery Temperature

#### Pearson Correlation Test for Capacity in Relation with Temperature

**Null Hypothesis:** No linear correlation between battery temperature and battery capacity.

**Alternative Hypothesis:** There is a significant linear correlation.

###### Findings

- Correlation Coefficient (r): -0.8097441885175425
- P-Value: 2.8106843882059685e-40
- Reject the null hypothesis, proving that there is a significant linear correlation between battery temperature and battery capacity.

![image](https://github.com/user-attachments/assets/4a70c6d7-a2b5-48a8-945a-4094cfbe5ce1)

#### Spearman Correlation Test for Capacity in Relation with Temperature

**Null Hypothesis:** No monotonic relationship between battery temperature and battery capacity.

**Alternative Hypothesis:** There is a significant monotonic correlation.

###### Findings

- Correlation Coefficient (ρ): -0.7657508313887864
- P-Value: 1.2127188259834856e-33
- Reject the null hypothesis, proving that there is a strong monotonic relation between battery temperature and battery capacity.

![image](https://github.com/user-attachments/assets/a9da9746-28a7-4df7-8a16-b1d23ee08a75)

#### Two-Tailed T-Test for Capacity in Relation with Temperature

**Null Hypothesis:** The mean battery capacity is the same in both groups.

**Alternative Hypothesis:** The mean battery capacity is different between the groups.

###### Findings

- T-Statistic: 21.839623575172133
- P-Value: 1.11288621468798e-50
- Reject the null hypothesis, proving that the mean battery capacity is different between the groups.

#### One-Tailed T-Test for Capacity in Relation with Temperature Groups

**Null Hypothesis:** The mean battery capacity in the low temperature group is less than or equal to the high temperature group.

**Alternative Hypothesis:** The mean battery capacity is greater in the low temperature group.

###### Findings

- T-Statistic: 21.839623575172133
- One-Tailed P-Value: 5.5644310734399e-51
- Reject the null hypothesis, proving that the mean battery capacity is greater in the low temperature group.

![image](https://github.com/user-attachments/assets/3c76ac41-5c73-47e7-898b-1717ad3b433d)

![image](https://github.com/user-attachments/assets/d916b3b6-a26a-463a-aa0a-1e59e304337b)

#### One-Way ANOVA for Capacity in Relation with Temperature

**Null Hypothesis:** Mean battery capacity is equal across all temperature bins.

**Alternative Hypothesis:** At least one group differs.

###### Findings

- F-Statistic = 93.62187835584314
- P-Value = 6.727485891787589e-28
- Reject the null hypothesis, proving that at least one group mean charge capacity is different than the others.

![image](https://github.com/user-attachments/assets/617644aa-e5fd-4df3-9902-6ee8c182de7c)

![image](https://github.com/user-attachments/assets/f1e80217-ddd7-4232-9d2f-8451a7a13618)

When all the steps in this part are evaluated, it is obvious that in the lower temoeratures, the battery capacity is higher, while the temperature rises, the battery capacity starts to degrade resulting in a lower battery efficiency. Combined with the discharge duration tests, it is possible that there is a negative relation between battery temperature and battery efficiency, concluding the first part of the null hypothesis.

**Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

Only remaining part to complete the tests is to examine the relation of the remaining useful life (RUL) with battery temperature.

### 2. Relation of Remaining Useful Life (RUL) with Battery Temperature

##### Pearson Correlation Test for RUL in Relation with Temperature

**Null Hypothesis:** No linear correlation between battery temperature and remaining useful life (RUL).

**Alternative Hypothesis:** There is a significant linear correlation.

###### Findings

- Correlation Coefficient (r): -0.7918862831172826
- P-Value: 5.831299114433377e-37
- Reject the null hypothesis, proving that there is a significant linear correlation between battery temperature and remaining useful life (RUL).

![image](https://github.com/user-attachments/assets/1696c3e7-ae6b-4a46-8467-c06fa8632c11)

##### Spearman Correlation Test for RUL in Relation with Temperature

**Null Hypothesis:** No monotonic relationship between battery temperature and remaining useful life (RUL).

**Alternative Hypothesis:** There is a significant monotonic correlation.

###### Findings

- Correlation Coefficient (ρ): -0.7830223452328641
- P-Value: 1.2004211657701526e-35
- Reject the null hypothesis, proving that there is a strong monotonic relation between battery temperature and remaining useful life (RUL).

![image](https://github.com/user-attachments/assets/35fda465-c367-45a1-9120-302a47dabea9)

##### Two-Tailed T-Test for Remaining useful Life (RUL) in Relation with Temperature

**Null Hypothesis:** The mean remaining useful life (RUL) is the same in both groups.

**Alternative Hypothesis:** The mean remaining useful life (RUL) is different between the groups.

###### Findings

- T-Statistic: 20.57740189874722
- P-Value: 5.621172405518512e-47
- Reject the null hypothesis, proving that the mean remaining useful life (RUL) is different between the groups.

##### One-Tailed T-Test for Remaining useful Life (RUL) in Relation with Temperature

**Null Hypothesis:** The mean RUL in the low temperature group is less than or equal to the high temperature group.

**Alternative Hypothesis:** The mean RUL is greater in the low temperature group.

###### Findings

- T-Statistic: 20.57740189874722
- One-Tailed P-Value: 2.810586202759256e-47
- Reject the null hypothesis, proving that the mean RUL is greater in the low temperature group.

![image](https://github.com/user-attachments/assets/d57461d4-61dd-4687-b557-02f5f84f6556)

![image](https://github.com/user-attachments/assets/18491943-7964-44c7-992a-1885ebfdbc6b)

##### One-Way ANOVA for RUL in Relation with Temperature

**Null Hypothesis:** Mean RUL is equal across all temperature bins.

**Alternative Hypothesis:** At least one group differs.

###### Findings

- -Statistic = 81.73646437193544
- P-Value = 2.598633162882089e-25
- Reject the null hypothesis, proving that at least one group mean RUL is different than the others.

![image](https://github.com/user-attachments/assets/2ba6414f-4c34-4757-ba0b-854c38554975)

![image](https://github.com/user-attachments/assets/9cb8abbc-a271-4b55-8d61-a939f4968535)

Based on the analysis done in this step, in low temperatures, the remaining useful life is higher. In the meantime, in high temperatures, the remaining useful life is lower proving that there is a negative relationship between the two variables. This step concludes our hypoteses test stage.

**Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

**Alternative Hypothesis (H₁)**: Temperature has no relation with the efficiency and remaining useful life of lithium-ion batteries.

We do not have enough evidence to reject the null hypothesis since in each step, the relation between temperature and battery efficiency and remaining useful life. 

**Null Hypothesis (H₀)**: Temperature has no relation with the efficiency and remaining useful life of lithium-ion batteries.

**Alternative Hypothesis (H₁)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

If the hypotheses were constructed like this, one could reject the null hypothesis, since the relation is proved for all the variables.

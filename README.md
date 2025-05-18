# DSA210-Term-Project

In this project, I will investigate the effect of temperature on battery efficiency and aim to model the remaining useful life (RUL) behavior of lithium-ion batteries. By doing so, I intend to derive meaningful conclusions that can be translated into practical solutions to enhance battery usage efficiency in daily life applications. The core of the study relies on analyzing a comprehensive dataset that captures the interplay between operational parameters and ambient temperature. This main dataset is complemented by another that includes battery chemistry characteristics across temperature ranges. Additionally, throughout the analysis, supplementary indicators will be engineered from the existing data to further enrich the insights and modeling accuracy.

---

## Table of Contents
- [Motivation](#motivation)
- [Data Sources](#data-sources)
- [Hypotheses](#hypotheses)
- [Methodology](#methodology)
- [Visualization Findings](#visualization-findings)
- [Hypothesis Testing](#hypothesis-testing)
- [ML Model Implementation](#ml-model-implementation)
- [Limitations and Future Work](#limitations-and-future-work)

---

## Motivation

In the rapid revolutions occuring in technology today, the adoption of lithium-ion batteries stands as an important building block especially when we think of electrically powered devices, electric vehicles and renewable energy storage systems. Since the reliance on battery technologies increases more and more, understanding the behavior becomes more of an interest area. The widespread use of the lithium-ion batteries raises both safety and economic concerns. To be able to offer accurate solutions, it is important to analyze data. Hence, it becomes possible to optimize the battery performance and predict the lifespan of a functioning battery.

Battery efficiency, reliability, lifespan and safety relies on multiple factors but one of the critical ones is the temperature stemming from the chemical nature of lithium-ion batteries. In general, it is known that when batteries are exposed to high temperatures, their capacity and performance consistency decreases while safety risks increases. However, the infuence of the temperature is still an ongoing research area since there is no concrete explanation showing the effect of variations in temperature on battery performance metrics.

This project seeks to explore and quantify the relationship between battery temperature and key efficiency indicators such as discharge time, capacity, and remaining useful life (RUL). By doing so, it aims to contribute to the development of real-world battery management strategies that are grounded in data-driven insights.

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

These hypotheses will be tested using statistical methods, including correlation analysis, hypothesis testing, and regression modeling. The goal is to determine whether temperature is a statistically significant factor affecting battery performance metrics.

---

## Methodology

The methodology of this project consists of four core phases: data processing, data visualization, hypothesis testing and machine leraning model implementation. Each step was carried out in dedicated Jupyter notebooks to ensure modularity and clarity.

### 1) Data Processing

The data processing phase begins with the extraction of structured battery datasets from MATLAB .mat files, specifically B0005.mat. Using scipy.io, the nested cycle structure is accessed, containing detailed measurements for charge, discharge, and impedance phases. Each sub-structure is parsed and reshaped into Python dictionaries and subsequently converted into data frames. After loading each data frame, based on cycle indices, the data is merged to end up with a data frame consisting of useful variables for data analysis.

### 2) Data Visualization

The visualization stage explores patterns and correlations across the operational and environmental variables of the battery. This includes plotting trends over cycles using line and scatter plots to observe metrics such as discharging time, discharge capacity, and battery temperature changes. Lineplots are employed to compare distributions of battery capacity and RUL across temperature bins.  These visualizations are instrumental in guiding the formation of hypotheses and identifying relationships worth statistically validating.

### 3) Hypothesis Testing

This stage involves statistically testing the relationships between temperature and key performance indicators of the battery. This begins with performing correlation tests, two-tailed and one-tailed t-tests, and one-way ANOVA on discharging time over temperature bins. These techniques are used for both battery capacity and remaining useful life as well, in order. Several hypothesis tests are done on each variable to determine the significancy of the observed effects.

### 4) Machine Learning Model Implementation

The final phase involves implementing a machine learning model to investigate whether operational variables such as battery capacity, discharge time, and remaining useful life could be used to predict battery temperature. A linear regression model is selected due to its interpretability and effectiveness in identifying linear trends. The dataset is first cleaned and preprocessed to remove missing values, and then split into training and testing sets. Model performance is evaluated using RMSE and R² metrics. Additional evaluation includes a scatter plot comparing actual vs. predicted temperature values and a confusion matrix generated by binning temperature predictions. This phase provides a predictive perspective that supported and extends the conclusions drawn from hypothesis testing.

---

## Visualization Findings

### 1. Average Charging Time across Charging Cycle Bins

The following graphs explore how the average charging time evolves across different phases of the battery’s lifecycle. Charging time is an essential metric for evaluating a battery’s operational health, as it can be affected by internal resistance buildup, aging effects, and chemical degradation over time. Understanding how this variable changes across cycles can provide insights into the underlying electrochemical structure.

![image](https://github.com/user-attachments/assets/e3523cff-4459-4b25-b805-00225cc01049)

![image](https://github.com/user-attachments/assets/90d40245-aa44-459e-94f7-202639b30d99)

The visualizations reveal a generally increasing trend in charging time as the cycle number increases, indicating that the battery begins to require more time to reach full charge. This is expected as internal resistance typically increases with age, slowing down the charging process. However, despite the overall trend, the graphs also display a degree of inconsistency and fluctuation from cycle to cycle, suggesting that charging time may be influenced by other factors or may not serve as a stable indicator of battery health.

Given this variability, average charging time was not selected as a key variable for hypothesis testing. While the upward trend is visible, its lack of consistency across cycles makes it less reliable for drawing statistically meaningful conclusions compared to other indicators like discharge time, capacity, or remaining useful life.

### 2. Average Temperature across Charging Cycle Bins

The following graphs illustrate how the battery's internal temperature changes throughout the charging cycles. Since temperature directly influences the rate of chemical reactions and degradation processes within lithium-ion cells, monitoring its variation over time is critical for assessing both performance and safety. Ideally, an increase in temperature over time could indicate rising internal resistance or abnormal cell behavior, which are early signs of aging or inefficiency.

![image](https://github.com/user-attachments/assets/ad3ff0b6-316a-43d4-bd84-f46a5ce6601b)

![image](https://github.com/user-attachments/assets/1a72a5ce-334a-49ee-b65e-086323026f29)

In this case, the visualizations show that temperature values remain relatively stable across the charging cycle bins, with only slight fluctuations. There is no clear upward or downward trend that consistently correlates with cycle progression. This suggests that during charging, the battery's thermal profile remains largely controlled and does not display significant thermal degradation patterns.

Due to the lack of a consistent or statistically visible relationship, this metric was not selected for detailed hypothesis testing. While temperature is an important safety and performance factor, its stability during charging indicates that any thermal effects are likely being managed well under the tested conditions and do not strongly reflect changes in battery efficiency over time.

### 3. Average Discharging Time across Discharging Cycle Bins

The graphs below examine how discharging time evolves across different battery usage phases. Discharging time is a key efficiency indicator, reflecting how long the battery is capable of supplying energy during each cycle. As the battery ages, a decrease in discharging time typically indicates capacity degradation or increased internal resistance, both of which impair the battery’s ability to maintain energy output over time.

![image](https://github.com/user-attachments/assets/160daeac-40f4-4fe5-a7ff-033a70cc2347)

![image](https://github.com/user-attachments/assets/6faa5b26-5a21-4a09-9ad9-be2de387790a)

In this case, the visualizations show a clear and consistent downward trend in discharging time as the cycle number increases. This suggests that the battery's ability to hold and deliver charge diminishes progressively with continued usage which is a behavior that aligns well with expected degradation patterns in lithium-ion batteries.

Because the trend is directionally coherent, this variable is highly relevant for further statistical analysis. Its strong cycle-based pattern makes it suitable for hypothesis testing against temperature data, to explore whether thermal effects influence how long the battery retains functional energy output. Therefore, discharging time is used as one of the core efficiency metrics in the hypothesis testing stage of this project.

### 4. Average Temperature across Discharging Cycle Bins

The following graphs investigate how battery temperature evolves specifically during the discharge cycles across the battery’s lifespan. Monitoring temperature during discharge is essential because it reflects real-time thermal stress on the battery while it actively delivers energy. Excessive heating during discharge may signal inefficiencies, internal resistance buildup, or safety risks associated with degradation.

![image](https://github.com/user-attachments/assets/43a38956-efe8-4b7a-ac25-626abd322c03)

![image](https://github.com/user-attachments/assets/5b3ea88b-223f-44f1-8b16-6da4975c66e3)

The visualizations reveal a relatively stable but slightly increasing trend in average temperature as the cycle number advances. This suggests a mild thermal accumulation effect, which could be due to chemical aging or reduced heat dissipation efficiency as the battery wears. While the changes are not dramatic, the consistency of this trend is noteworthy.

Given that both discharge duration (explored in the previous section) and temperature show predictable behavior across cycles, it becomes relevant to examine whether they are statistically correlated. The relationship between discharging time and battery temperature forms the first analytical focus in the hypothesis testing phase. By investigating how increased temperature may shorten discharge duration, the analysis aims to determine if thermal effects contribute to diminished battery efficiency over time.

### 5. Battery Capacity over Discharging Cycles

Battery capacity is one of the most fundamental indicators of performance and degradation in lithium-ion cells. It directly reflects how much charge the battery can store and deliver during each discharge cycle. As the battery ages, the active materials degrade, leading to a gradual and irreversible decline in usable capacity.

![image](https://github.com/user-attachments/assets/b9e9a69b-5154-4397-aa66-a5bb2e85328d)

![image](https://github.com/user-attachments/assets/e65c4477-07db-476f-ba73-c421433ba923)

The graphs clearly demonstrate a consistent and progressive decrease in battery capacity across successive discharge cycles. This declining trend strongly indicates the expected degradation process, where the battery’s ability to hold charge diminishes as a function of use. Such a pattern confirms that the battery is undergoing normal aging, which is a key factor to track for predictive maintenance and life estimation.

Given its steady and interpretable behavior, capacity is an ideal candidate for hypothesis testing in relation to temperature. Since thermal conditions can accelerate chemical degradation, investigating whether higher temperatures correlate with lower capacities is critical. This relationship serves as the second focal point in the hypothesis testing phase, complementing the analysis of discharge time and reinforcing the broader goal of understanding battery efficiency dynamics.

### 6. Average Battery Capacity across Temperature Bins

This section examines how discharge capacity varies across different temperature bins, offering insights into the effect of thermal conditions on the battery's ability to store and deliver energy. Since elevated temperatures are known to accelerate degradation in lithium-ion cells, understanding whether capacity consistently drops in higher thermal environments is essential for assessing battery efficiency and lifespan under different operating conditions.

![image](https://github.com/user-attachments/assets/a12ab9c8-64bc-433e-b605-78b42f4b2f5d)

![image](https://github.com/user-attachments/assets/5f5adf79-0681-4269-8dee-1344a92f5a27)

The graphs display a clear and consistent inverse relationship between battery temperature and discharge capacity. As the average operating temperature increases, the corresponding battery capacity decreases. This trend supports the theoretical expectation that higher thermal stress degrades the internal structure of the battery, thereby reducing the amount of charge it can hold over time.

Given this visually coherent trend, the relationship between temperature and battery capacity is selected as the second focal point in the hypothesis testing stage. Establishing a statistically significant connection between these variables helps confirm that thermal conditions play a measurable role in influencing efficiency metrics, further validating the role of temperature as a key factor in battery health diagnostics.

### 7. RUL across Temperature Bins

This section investigates how the Remaining Useful Life (RUL) of the battery changes across different temperature bins. RUL is a critical metric in battery prognostics, as it reflects the number of future cycles the battery is expected to perform effectively before its capacity falls below a usable threshold. Because temperature can influence chemical stability, aging rate, and degradation patterns, understanding its relationship with RUL is essential for predictive maintenance and reliability analysis.

![image](https://github.com/user-attachments/assets/a84b53af-986d-444f-8cc8-2ad49570a138)

![image](https://github.com/user-attachments/assets/2c902fc7-1200-497d-a3e4-f3571d503442)

The visualizations show a clear trend: RUL tends to decrease as battery temperature increases. Batteries operating in lower temperature ranges exhibit longer projected lifespans, while those subjected to higher thermal conditions show reduced RUL values. This behavior aligns with the known impact of temperature on accelerating degradation mechanisms such as electrode breakdown and electrolyte decomposition.

Given the strength and clarity of this relationship, the connection between battery temperature and RUL is chosen as the third and final relationship to be statistically tested in the hypothesis testing stage. This analysis complements the findings from discharge time and capacity trends, providing a holistic view of how temperature affects not just immediate performance, but also long-term battery sustainability.

### 8. Correlation Analysis on Discharge Results

To complement the individual analyses of discharge-related variables, a correlation heatmap was generated to examine the pairwise relationships between the key battery performance metrics: discharge time, discharge capacity, remaining useful life (RUL), and temperature. Correlation analysis provides a high-level overview of how variables co-vary, enabling quick identification of strong linear associations that may warrant further investigation.

![image](https://github.com/user-attachments/assets/f021c0eb-5b21-4ea7-bd4d-db14162126f5)

The heatmap reveals that discharge time, capacity, and RUL are all strongly positively correlated with one another, indicating that as one degrades, the others tend to follow a similar downward trend. In contrast, temperature shows strong negative correlations with each of these efficiency metrics. This inverse relationship visually reinforces the hypothesis that elevated temperature is associated with accelerated degradation and reduced performance across multiple dimensions.

---

## Hypothesis Testing

### 1. Relation of Battery Efficinecy with Battery Temperature

Since in the data, there exists two metrics that shows the battery efficiency, there will be two parts that hypothesis tests are conducted on. At the end, the results will be evaluated to make a conclusion.

### a. Relation of Discharge Duration with Battery Temperature

#### Pearson Correlation Test for Discharge Duration in Relation with Temperature

**Null Hypothesis (H₀):** No linear correlation between battery temperature and discharge duration.

**Alternative Hypothesis (H₁):** There is a significant linear correlation.

**Findings:**

- Correlation Coefficient (r): -0.7586681656065123
- P-Value: 1.0388933158394018e-32
- **Reject the null hypothesis**, proving that there is a significant linear correlation between battery temperature and discharge duration.

The negative correlation coefficient of approximately -0.76 indicates a strong inverse linear relationship between battery temperature and discharge duration. In practical terms, this means that as the battery operates at higher temperatures, the time it takes to discharge tends to decrease significantly. This trend is consistent with the understanding that elevated temperatures accelerate degradation processes, leading to a faster loss of usable charge. The extremely low p-value (< 0.001) confirms that this result is statistically significant, providing strong evidence against the null hypothesis. Therefore, this analysis supports the broader hypothesis that temperature adversely affects battery efficiency, beginning with its impact on discharge duration.

![image](https://github.com/user-attachments/assets/175fad49-ffd3-45cf-87ff-6760dd4ad28e)

#### Spearman Correlation Test for Discharge Duration in Relation with Temperature

**Null Hypothesis (H₀):** No monotonic relationship between battery temperature and discharge duration.

**Alternative Hypothesis (H₁):** There is a significant monotonic correlation.

**Findings:**

- Correlation Coefficient (ρ): -0.765188979606299
- P-Value: 1.4419679611288852e-33
- **Reject the null hypothesis**, proving that there is a strong monotonic relation between battery temperature and discharge duration.

The Spearman correlation coefficient of approximately -0.77 indicates a strong negative monotonic relationship between battery temperature and discharge duration. This means that as temperature increases, discharge duration consistently decreases, even if the relationship is not strictly linear. The very small p-value confirms that this result is statistically significant and highly unlikely to have occurred by chance. Unlike Pearson correlation, which captures only linear relationships, Spearman’s method validates that the overall trend between temperature and discharge time is both strong and directionally consistent. This further reinforces the conclusion that higher operating temperatures are associated with decreased battery efficiency, making discharge duration a reliable metric for examining thermal effects on battery performance.

![image](https://github.com/user-attachments/assets/aa7f40e6-108d-4250-aeeb-a8e5e547fee4)

#### Two-Tailed T-Test for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis (H₀):** The mean discharge duration is the same in both groups.

**Alternative Hypothesis (H₁):** The mean discharge duration is different between the groups.

**Findings:**

- T-Statistic: 19.345736701918707
- P-Value: 1.1254142603243133e-42
- **Reject the null hypothesis**, proving that the mean discharge duration is different between the groups.

The two-tailed t-test evaluates whether there is a statistically significant difference in the mean discharge duration between low-temperature and high-temperature groups. The extremely high t-statistic (19.35) and the correspondingly low p-value (close to zero) provide strong evidence that the means are not equal. This result leads to the rejection of the null hypothesis and confirms that temperature has a substantial impact on how long the battery can sustain discharge. In particular, the significant difference in means implies that battery performance, measured through discharge duration, varies meaningfully with thermal conditions. This supports the hypothesis that temperature is a key factor influencing battery efficiency.

#### One-Tailed T-Test for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis (H₀):** The mean discharge duration in the low temperature group is less than or equal to the high temperature group.s.

**Alternative Hypothesis (H₁):** The mean discharge duration is greater in the low temperature group.

**Findings:**

- T-Statistic: 19.345736701918707
- One-Tailed P-Value: 5.627071301621567e-43
- **Reject the null hypothesis**, proving that the mean discharge duration is greater in the low temperature group.

The one-tailed t-test was conducted to specifically test whether batteries operating at lower temperatures have longer discharge durations compared to those at higher temperatures. The very large t-statistic (19.35) and the extremely small one-tailed p-value (< 0.001) provide strong statistical evidence to reject the null hypothesis. This confirms that the mean discharge duration in the low temperature group is significantly greater than in the high temperature group. This result aligns with theoretical expectations, as batteries tend to perform more efficiently and retain energy longer under cooler operating conditions. The finding further strengthens the argument that higher temperatures negatively impact battery efficiency by shortening discharge time.

![image](https://github.com/user-attachments/assets/1c740229-a5d3-4092-8647-e6ba42a3e27b)

![image](https://github.com/user-attachments/assets/506ff738-1fbd-4957-adb5-4cedd0808181)

#### One-Way ANOVA for Discharge Duration in Relation with Temperature Groups

**Null Hypothesis (H₀):** Mean discharge duration is equal across all temperature bins.

**Alternative Hypothesis (H₁):** At least one group differs.

**Findings:**

- F-Statistic = 68.22562456047194
- P-Value = 2.552793322562453e-22
- **Reject the null hypothesis**, proving that at least one group mean discharge duration is different than the others.

The one-way ANOVA test was used to assess whether the mean discharge durations differ significantly across multiple temperature bins. The resulting F-statistic of approximately 68.23, combined with an extremely small p-value, provides strong evidence to reject the null hypothesis. This indicates that at least one temperature group exhibits a statistically different mean discharge duration compared to the others. In other words, the battery’s ability to sustain discharge varies depending on the temperature range. This result reinforces the conclusions drawn from the previous correlation and t-test analyses, confirming that temperature is a significant factor affecting discharge efficiency and validating its inclusion in the broader hypothesis framework of this project.

![image](https://github.com/user-attachments/assets/e9304850-f407-486c-bcba-cebd34c01ddb)

![image](https://github.com/user-attachments/assets/deb82f12-d562-4f6a-a06e-c1357070cf67)

Considering all the results from the analysis of the relationship between battery discharge duration and temperature, there is strong evidence of a significant negative correlation. The findings consistently show that at lower temperatures, the battery exhibits longer discharge durations, whereas higher temperatures lead to shorter discharge periods. This outcome supports the null hypothesis, which states:

**Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

To fully validate this hypothesis, the analysis must proceed with the remaining steps of hypothesis testing, particularly focusing on battery capacity and RUL in relation to temperature.

### b. Relation of Battery Capacity with Battery Temperature

#### Pearson Correlation Test for Capacity in Relation with Temperature

**Null Hypothesis (H₀):** No linear correlation between battery temperature and battery capacity.

**Alternative Hypothesis (H₁):** There is a significant linear correlation.

**Findings:**

- Correlation Coefficient (r): -0.8097441885175425
- P-Value: 2.8106843882059685e-40
- **Reject the null hypothesis**, proving that there is a significant linear correlation between battery temperature and battery capacity.

The Pearson correlation coefficient of approximately -0.81 indicates a strong negative linear relationship between battery temperature and discharge capacity. This means that as temperature increases, the battery’s ability to store and deliver charge decreases significantly. The extremely low p-value confirms the statistical significance of this result, providing clear evidence to reject the null hypothesis. These findings suggest that higher operating temperatures contribute to faster capacity degradation, reinforcing the understanding that thermal stress negatively impacts battery efficiency. This result also strengthens the case for temperature being a critical factor in evaluating overall battery performance and longevity.

![image](https://github.com/user-attachments/assets/4a70c6d7-a2b5-48a8-945a-4094cfbe5ce1)

#### Spearman Correlation Test for Capacity in Relation with Temperature

**Null Hypothesis (H₀):** No monotonic relationship between battery temperature and battery capacity.

**Alternative Hypothesis (H₁):** There is a significant monotonic correlation.

**Findings:**

- Correlation Coefficient (ρ): -0.7657508313887864
- P-Value: 1.2127188259834856e-33
- **Reject the null hypothesis**, proving that there is a strong monotonic relation between battery temperature and battery capacity.

The Spearman correlation coefficient of approximately -0.77 indicates a strong negative monotonic relationship between battery temperature and capacity. This means that as temperature increases, battery capacity consistently declines, even if the rate of change is not strictly linear. The extremely low p-value confirms that this result is statistically significant. This test provides further evidence that thermal conditions have a considerable impact on battery efficiency, supporting the hypothesis that capacity diminishes with rising temperature levels.

![image](https://github.com/user-attachments/assets/a9da9746-28a7-4df7-8a16-b1d23ee08a75)

#### Two-Tailed T-Test for Capacity in Relation with Temperature

**Null Hypothesis (H₀):** The mean battery capacity is the same in both groups.

**Alternative Hypothesis (H₁):** The mean battery capacity is different between the groups.

**Findings:**

- T-Statistic: 21.839623575172133
- P-Value: 1.11288621468798e-50
- **Reject the null hypothesis**, proving that the mean battery capacity is different between the groups.

The two-tailed t-test evaluates whether there is a statistically significant difference in the mean battery capacity between low-temperature and high-temperature groups. The extremely high t-statistic (21.84) and the near-zero p-value provide strong evidence that the group means differ significantly. This result leads to the rejection of the null hypothesis and confirms that battery capacity is affected by temperature variations. Specifically, the significant drop in capacity under higher temperatures indicates that thermal conditions play a meaningful role in accelerating capacity degradation. This finding supports the hypothesis that temperature is a critical factor in determining battery efficiency and health.

#### One-Tailed T-Test for Capacity in Relation with Temperature Groups

**Null Hypothesis (H₀):** The mean battery capacity in the low temperature group is less than or equal to the high temperature group.

**Alternative Hypothesis (H₁):** The mean battery capacity is greater in the low temperature group.

**Findings:**

- T-Statistic: 21.839623575172133
- One-Tailed P-Value: 5.5644310734399e-51
- **Reject the null hypothesis**, proving that the mean battery capacity is greater in the low temperature group.

The one-tailed t-test assesses whether the mean battery capacity is significantly greater in the low-temperature group compared to the high-temperature group. The extremely high t-statistic (21.84) and the exceptionally small p-value provide compelling evidence to reject the null hypothesis. This result confirms that batteries operating under cooler conditions retain significantly more capacity than those exposed to higher temperatures. The finding reinforces the understanding that elevated temperatures accelerate degradation, leading to a measurable reduction in capacity. It further supports the hypothesis that thermal conditions are a major determinant of battery performance and longevity.

![image](https://github.com/user-attachments/assets/3c76ac41-5c73-47e7-898b-1717ad3b433d)

![image](https://github.com/user-attachments/assets/d916b3b6-a26a-463a-aa0a-1e59e304337b)

#### One-Way ANOVA for Capacity in Relation with Temperature

**Null Hypothesis (H₀):** Mean battery capacity is equal across all temperature bins.

**Alternative Hypothesis (H₁):** At least one group differs.

**Findings:**

- F-Statistic = 93.62187835584314
- P-Value = 6.727485891787589e-28
- **Reject the null hypothesis**, proving that at least one group mean charge capacity is different than the others.

The one-way ANOVA test determines whether the mean battery capacity differs significantly across multiple temperature bins. The very high F-statistic (93.62) and the extremely small p-value provide strong statistical evidence to reject the null hypothesis. This confirms that at least one of the temperature groups has a mean capacity that differs from the others. The result highlights that battery capacity is not uniformly distributed across temperature ranges, indicating that temperature plays a significant role in shaping how effectively the battery retains and delivers energy. This finding aligns with previous results and further supports the hypothesis that thermal conditions impact battery efficiency.

![image](https://github.com/user-attachments/assets/617644aa-e5fd-4df3-9902-6ee8c182de7c)

![image](https://github.com/user-attachments/assets/f1e80217-ddd7-4232-9d2f-8451a7a13618)

When all the findings in this section are considered, it becomes clear that battery capacity is significantly higher at lower temperatures, while increasing temperatures lead to noticeable capacity degradation. This decline directly contributes to reduced battery efficiency. When combined with the earlier discharge duration results, the evidence points toward a consistent negative relationship between battery temperature and overall efficiency. These outcomes collectively support the first component of the null hypothesis:

**Null Hypothesis (H₀)**: Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

Only remaining part to complete the tests is to examine the relation of the remaining useful life (RUL) with battery temperature.

### 2. Relation of Remaining Useful Life (RUL) with Battery Temperature

#### Pearson Correlation Test for RUL in Relation with Temperature

**Null Hypothesis (H₀):** No linear correlation between battery temperature and remaining useful life (RUL).

**Alternative Hypothesis (H₁):** There is a significant linear correlation.

**Findings:**

- Correlation Coefficient (r): -0.7918862831172826
- P-Value: 5.831299114433377e-37
- **Reject the null hypothesis**, proving that there is a significant linear correlation between battery temperature and remaining useful life (RUL).

The Pearson correlation test reveals a strong negative linear relationship between battery temperature and remaining useful life (RUL), as indicated by a correlation coefficient of approximately -0.79. The extremely low p-value confirms that this correlation is statistically significant, allowing us to confidently reject the null hypothesis. This result demonstrates that as temperature increases, RUL tends to decrease, suggesting that batteries exposed to higher thermal conditions experience faster degradation and shortened operational lifespan. This finding is consistent with previous efficiency metrics and reinforces the broader hypothesis that temperature significantly influences both performance and durability of lithium-ion batteries.

![image](https://github.com/user-attachments/assets/1696c3e7-ae6b-4a46-8467-c06fa8632c11)

#### Spearman Correlation Test for RUL in Relation with Temperature

**Null Hypothesis (H₀):** No monotonic relationship between battery temperature and remaining useful life (RUL).

**Alternative Hypothesis (H₁):** There is a significant monotonic correlation.

**Findings:**

- Correlation Coefficient (ρ): -0.7830223452328641
- P-Value: 1.2004211657701526e-35
- **Reject the null hypothesis**, proving that there is a strong monotonic relation between battery temperature and remaining useful life (RUL).

The Spearman correlation test confirms a strong negative monotonic relationship between battery temperature and remaining useful life (RUL), with a coefficient of approximately -0.78. This result indicates that RUL consistently decreases as temperature increases, regardless of whether the relationship is strictly linear. The extremely low p-value further supports the statistical significance of this finding, allowing us to reject the null hypothesis. This reinforces the conclusion that thermal stress plays a critical role in accelerating battery aging and reducing its usable lifespan.

![image](https://github.com/user-attachments/assets/35fda465-c367-45a1-9120-302a47dabea9)

#### Two-Tailed T-Test for Remaining useful Life (RUL) in Relation with Temperature

**Null Hypothesis (H₀):** The mean remaining useful life (RUL) is the same in both groups.

**Alternative Hypothesis (H₁):** The mean remaining useful life (RUL) is different between the groups.

**Findings:**

- T-Statistic: 20.57740189874722
- P-Value: 5.621172405518512e-47
- **Reject the null hypothesis**, proving that the mean remaining useful life (RUL) is different between the groups.

The two-tailed t-test assesses whether there is a statistically significant difference in the mean remaining useful life (RUL) between batteries operating in low and high temperature conditions. The very high t-statistic (20.58) and the near-zero p-value provide strong evidence to reject the null hypothesis. This confirms that RUL varies significantly across temperature groups. Specifically, the result suggests that batteries subjected to higher temperatures tend to have a reduced lifespan compared to those operating at lower temperatures. This finding further supports the hypothesis that thermal conditions are a key driver of battery aging and durability.

#### One-Tailed T-Test for Remaining useful Life (RUL) in Relation with Temperature

**Null Hypothesis (H₀):** The mean RUL in the low temperature group is less than or equal to the high temperature group.

**Alternative Hypothesis (H₁):** The mean RUL is greater in the low temperature group.

**Findings:**

- T-Statistic: 20.57740189874722
- One-Tailed P-Value: 2.810586202759256e-47
- **Reject the null hypothesis**, proving that the mean RUL is greater in the low temperature group.

The one-tailed t-test was conducted to determine whether the mean remaining useful life (RUL) is significantly greater in the low-temperature group compared to the high-temperature group. The large t-statistic (20.58) and extremely small one-tailed p-value provide strong statistical evidence to reject the null hypothesis. This result confirms that batteries operating under lower temperature conditions retain a significantly longer remaining lifespan. It further emphasizes the detrimental impact of higher temperatures on battery longevity and aligns with the overall conclusion that cooler thermal environments are more favorable for extending battery life.

![image](https://github.com/user-attachments/assets/d57461d4-61dd-4687-b557-02f5f84f6556)

![image](https://github.com/user-attachments/assets/18491943-7964-44c7-992a-1885ebfdbc6b)

#### One-Way ANOVA for RUL in Relation with Temperature

**Null Hypothesis (H₀):** Mean RUL is equal across all temperature bins.

**Alternative Hypothesis (H₁):** At least one group differs.

**Findings:**

- -Statistic = 81.73646437193544
- P-Value = 2.598633162882089e-25
- **Reject the null hypothesis**, proving that at least one group mean RUL is different than the others.

The one-way ANOVA test evaluates whether the mean remaining useful life (RUL) differs significantly across multiple temperature bins. The high F-statistic (81.74) and the extremely low p-value provide strong evidence to reject the null hypothesis. This result indicates that at least one temperature group exhibits a significantly different mean RUL, confirming that RUL is not uniformly distributed across thermal conditions. These findings reinforce the conclusion that temperature has a measurable impact on battery longevity and further validate the inclusion of RUL as a critical efficiency metric in evaluating thermal effects on battery performance.

![image](https://github.com/user-attachments/assets/2ba6414f-4c34-4757-ba0b-854c38554975)

![image](https://github.com/user-attachments/assets/9cb8abbc-a271-4b55-8d61-a939f4968535)

Based on the results obtained in this step, it is evident that batteries operating at lower temperatures exhibit a higher remaining useful life (RUL), while those subjected to higher temperatures show a marked decrease in RUL. This confirms the presence of a strong negative relationship between temperature and battery longevity. The consistency across all statistical tests reinforces the reliability of this finding. With this final analysis, the hypothesis testing stage is concluded, having demonstrated that temperature significantly influences both efficiency and lifespan-related metrics of lithium-ion batteries.

**Null Hypothesis (H₀):** Temperature has a relation with the efficiency and remaining useful life of lithium-ion batteries.

**Alternative Hypothesis (H₁):** Temperature has no relation with the efficiency and remaining useful life of lithium-ion batteries.

We do not have sufficient evidence to reject the null hypothesis. Statistical analyses conducted throughout the study consistently revealed a meaningful relationship between temperature and both efficiency indicators (discharge time and battery capacity) as well as remaining useful life (RUL). The presence of statistically significant correlations suggests that variations in temperature are associated with changes in battery performance metrics. As a result, we retain the null hypothesis that temperature has a relationship with the efficiency and remaining useful life of lithium-ion batteries. These findings support the theoretical expectation that thermal conditions influence battery degradation behavior.

---

## ML Model Implementation

### Linear Regression Model to Predict Remaining Useful Life (RUL)

**Objective:**

The objective of the machine learning implementation in this study is to evaluate whether battery performance indicators, specifically battery capacity, discharge time, and remaining useful life (RUL), can be used to accurately estimate battery temperature. A Linear Regression model was employed for this purpose, serving as a simple yet interpretable baseline to test the strength of this relationship.

**Results:**

**RMSE (Root Mean Squared Error):** 0.25, indicating a very low average deviation of the predicted temperature values from the actual temperature readings, measured in degrees Celsius.

**R² Score:** 0.88, which suggests that 88% of the variance in the actual battery temperature can be explained by the linear relationship with discharge capacity, discharge time, and RUL.

These metrics indicate that the linear regression model performs strongly, capturing the underlying patterns between battery efficiency indicators and thermal behavior with high accuracy. The low RMSE and high R² demonstrate that the model provides reliable temperature estimates across the observed range.

#### Scatter Plot of Actual vs. Predicted Battery Temperature

The scatter plot illustrates the relationship between the actual and predicted battery temperature values produced by the linear regression model. Each point represents a test observation, with the horizontal axis corresponding to the true temperature and the vertical axis indicating the model’s prediction. Most points are closely clustered around the red dashed diagonal line, which represents perfect predictions where actual and predicted values are equal. This visual alignment confirms a strong positive correlation between the predicted and true temperatures, supporting the numerical R² score of 0.88. Only a few minor deviations from the diagonal suggest small prediction errors, but overall, the plot demonstrates that the model performs well in capturing the thermal behavior of the battery based on battery capacity, discharge duration, and remaining useful life.

![image](https://github.com/user-attachments/assets/2442ced3-4009-4fa3-8aa3-fe71a14b3f68)

#### Confusion Matrix for Binned Temperature Prediction

The confusion matrix provides a categorical evaluation of the model’s temperature prediction performance by grouping both actual and predicted values into temperature bins: 31.5–32 °C, 32–32.5 °C, 32.5–33 °C, 33–33.5 °C, and 33.5+ °C. The majority of predictions are concentrated along the diagonal, indicating that the model generally predicts the correct temperature range. For instance, the bins 32–32.5 °C and 33.5+ °C show relatively strong alignment between actual and predicted values, with 7 and 6 correct predictions, respectively. However, some off-diagonal values reveal instances where the model slightly overestimated or underestimated the temperature range—most notably in the 32–32.5 °C actual bin, where 4 predictions were made in the adjacent 32.5–33 °C range. These misclassifications are minor and occur primarily between neighboring bins, suggesting the model captures the general trend well but exhibits small deviations in boundary regions. Overall, the confusion matrix supports the conclusion that the model provides a reasonable approximation of temperature when interpreted in a discretized context.

![image](https://github.com/user-attachments/assets/58b5dc68-9af5-4ed4-85dd-2685405f8b38)

---

## Limitations and Future Work

### Limitations

While this project provides a thorough analysis of the relationship between temperature and key performance indicators of lithium-ion batteries, several limitations should be acknowledged:

**Single Dataset Focus:** Although supported by supplementary datasets, the analysis primarily relied on a single battery dataset (B0005.mat). Broader generalizability would benefit from applying the same methodology across diverse datasets, chemistries, and operational scenarios.

**Simplified Feature Set:** The machine learning model used only three predictor variables (battery capacity, discharge time, and remaining useful life). Including more detailed electrochemical or impedance-related features could enhance the predictive power.

**Model Complexity:** A linear regression model was selected for its interpretability, but more complex models such as neural networks could uncover nonlinear interactions and improve prediction accuracy.

**No Real-Time or Deployed Validation:** The study did not include real-world battery deployments or real-time sensor validation. Results are based solely on offline historical datasets.

**Temperature Binning Assumptions:** In classification evaluations, temperature bins were chosen using fixed or quantile-based intervals. This approach may oversimplify the continuous nature of thermal influence.

### Future Work

- Extend the analysis to a broader set of lithium-ion battery datasets to validate the consistency of the findings across different chemistries and usage patterns. This would help ensure that the observed temperature-performance relationships are not specific to a particular dataset or battery configuration.

- Explore advanced machine learning models, including tree-based regressors or deep learning approaches, to better capture nonlinearities in battery behavior. These models may uncover complex interactions between variables and improve predictive accuracy, especially in edge cases or under extreme thermal conditions.

- Incorporate additional operational features (internal resistance, impedance evolution etc.) for more robust predictive modeling. Expanding the feature space could provide deeper insights into battery health and enable more comprehensive assessments of temperature influence.

- Develop a real-time battery monitoring framework that applies the statistical and ML methods in an online setting for predictive maintenance. Implementing live diagnostics would make these techniques applicable in practical battery management systems and support proactive decision-making.

- Conduct a sensitivity analysis to understand how changes in bin definitions or feature engineering choices impact model outputs and statistical conclusions. This would help quantify the robustness of the results and guide best practices for preprocessing and model interpretation in future studies.

- Apply uncertainty quantification methods, such as Bayesian regression or dropout-based uncertainty estimation, to better understand the confidence level of model predictions and support risk-aware decision-making.

- Explore the integration of these models into real-world Battery Management Systems (BMS) to enable continuous health monitoring, anomaly detection, and predictive control in live environments.

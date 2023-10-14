# Simulation-of-Emergency-Responses-to-Cardiac-Arrests-in-an-Urban-Setting

## Overview

This project delves into optimizing emergency responses to Out-of-Hospital Cardiac Arrests (OHCAs) in an urban environment. Through data analysis, simulation, and policy evaluation, our aim is to enhance patient survival rates while making efficient use of available resources.

## Files

- **ProjectData-OHCAs.csv:** Dataset containing OHCA-related information, including Dispatch Time, Latitude (Lat), Longitude (Lon), and Ambulance Arrival Time.

- **ProjectData-VolunteerResponses.csv:** Dataset with data related to volunteer responses, including Response and Response Delay.
- **Data Cleansing and Transformation** 
- **Policies Analysis**

## Data Cleansing and Transformation

We initiated the project by refining the dataset through the removal of outliers. Additionally, we explored the distribution of OHCA cases across geographical and temporal dimensions. We map distributions to response delays from both volunteers and ambulance arrival times. Simulation and testing handle outlier cases, and we map distributions to address gaps in our data. This step ensures data quality and reliability for further analysis.


## Modeling Approach

Our model addresses the following problem:

1. An OHCA is reported to 911.
2. An ambulance officer activates the volunteer-alert system and dispatches an ambulance.
3. The volunteer-alert system identifies nearby volunteers (within 1 km) and alerts a subset of them based on the chosen policy.
4. Over time, volunteers accept, decline, or don't respond to the alert. Accepting volunteers head to the OHCA. Additional volunteers may be dispatched based on responses.
5. The first arriving volunteer administers CPR, and the ambulance provides defibrillation once it arrives, also providing CPR if no volunteers are at the OHCA when it arrives.

The model considers three input parameters: number of replications, volunteer count, and dispatch policy. It runs 100 replications for each simulation, independently treating each OHCA incident due to their rarity. The simulations cover various volunteer network sizes, ranging from 9,000 to 12,000 in increments of 500.

For each simulation, the model:

- Generates OHCA locations via resampling.
- Models the time from OHCA to alert using a triangular distribution.
- Simulates ambulance arrival time with a log-normal distribution.
- Determines volunteer locations using a thinning method with a nonhomogeneous Poisson point process.

The model alerts volunteers based on the chosen policy, response probabilities, and response times (gamma distribution for acceptances). If volunteers don't respond, there's a 15% chance they arrive anyway, prompting further time calculations. The first arriving volunteer initiates CPR, while the ambulance handles defibrillation if required.

The model tracks four performance measures for each replication:

- Survival Rate (SR) - patient survival rate.
- Alerted Volunteers (AV) - number of alerted volunteers.
- Nearby Fraction (NF) - presence of a volunteer within 200 meters.
- Volunteer-First Fraction (VF) - volunteer arriving before the ambulance.

These measures provide insights into the effectiveness of each policy for varying volunteer network sizes.

Lastly we can use estimate the patient's survival probability by using the formula: 
<div style="text-align: center;">
  <img width="500" alt="Screenshot 2023-10-11 at 5 37 41 PM" src="https://github.com/yusef-rahimzada/Simulation-of-Emergency-Responses-to-Cardiac-Arrests-in-an-Urban-Setting/assets/66438099/54a5c6cb-cd0e-469e-8bc1-de9ceb27ee3f">
</div>
where T1 represents the time until the initiation of CPR, administered by both volunteers and ambulances, and T2 represents the time until defibrillation initiation, an action solely performed by ambulances.


## Policies Analysis

In our simulations, we analyzed four dispatch policies at different volunteer network sizes, ranging from 9,000 to 12,000 with 500-person increments. After extensive consultation with software developers, paramedics, and volunteers, we explored the following dispatch policies:

#### Policy 1: Safe Bet
This policy suggests alerting the closest 20 volunteers to ensure a higher response rate of around 7 volunteers. It achieved survival rates between 11.7% and 12.8%, peaking at 11,000 volunteers.

#### Policy 2: Efficiency Focus
This policy alerts volunteers one at a time with a 1-minute response time. It reduces the average number of alerted volunteers to about 3 but lowers the survival rate to 10%.

#### Policy 3: Full Volunteer Alert
This policy alerts all available volunteers who can reach the scene before the ambulance. It increased alerted volunteers to a range of 64 to 116 but raised the survival rate to approximately 12%.

#### Policy 4: Two-Batch Policy
This policy aims to improve Policy 2 by increasing the batch size to 2 while providing a 1-minute response time before moving on to the next set of alerts. Surprisingly, it resulted in a decrease in the survival rate and other metrics.

## Conclusion

In conclusion, we recommend adopting any of the first three policies as they balance good survival rates with efficient utilization of the volunteer network for handling severe OHCA cases.

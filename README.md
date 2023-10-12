# Simulation-of-Emergency-Responses-to-Cardiac-Arrests-in-an-Urban-Setting
Simulation of Emergency Responses to Cardiac Arrests in an Urban Setting

Overveiw: Led exploratory data analysis, with a focus on removing outliers and comprehending case distribution across geographical and temporal dimensions. Applied maximum likelihood estimation and method of moments estimation to derive distribution parameters, utilizing Q-Q plots to pinpoint the best-fit distribution. Identified variations in cases by day of the week and time across all sectors, strategically leveraging these insights to optimize ambulance placement, refine shift assignments, and adhere to budget constraints, resulting in a 21% increase in theoretical survival rates.

Attached files: 
- ProjectData-OHCAs.csv: Dataset containing Dispatch_Time, Lat (Latitude), Lon (Longitude), Amb_Arrival_Time
- ProjectData-VolunteerResponses.csv:  Dataset containing Response, Response_Delay
- Data Cleansing and Transformation: 

Background: 

OHCA is an Out-of-Hospital Cardiac Arrest incidents. To improve patient survival rates we will optimizing the volunteer dispatch policies. The patient's survival probability can be expressed using the following formula, as shown in the image below. In this formula, 

<div style="text-align: center;">
  <img width="300" alt="Screenshot 2023-10-11 at 5 37 41 PM" src="https://github.com/yusef-rahimzada/Simulation-of-Emergency-Responses-to-Cardiac-Arrests-in-an-Urban-Setting/assets/66438099/54a5c6cb-cd0e-469e-8bc1-de9ceb27ee3f">
</div>

T_1  represents the time in minutes until the initiation of CPR, which can be administered by both volunteers and ambulances.
T_2 represents the time in minutes until the initiation of defibrillation, which is an action exclusively carried out by ambulances.

The performance measures of interest include: 
- The average survival rate of patients (SR)
- The average number of alerted volunteers per OHCA (AV)
- The fraction of OHCAs with at least one volunteer within 200 meters (Nearby Fraction - NF)
- The fraction of OHCAs where a volunteer reaches the patient before the ambulance (Volunteer-first Fraction - VF).

The goal is to identify efficient dispatch policies with high survival rates while maintaining an acceptable number of alerted volunteers.

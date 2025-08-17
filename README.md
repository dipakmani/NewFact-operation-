import pandas as pd
import numpy as np
import random

# Number of records
n = 500000  

# ----------------------------
# Predefined lookup tables for IDs and their attributes
# ----------------------------

# Procedure
procedures = {
    1: ["Appendectomy", "General Surgery", "CPT44950"],
    2: ["Angioplasty", "Cardiology", "CPT92928"],
    3: ["Cataract Surgery", "Ophthalmology", "CPT66984"],
    4: ["Hip Replacement", "Orthopedics", "CPT27130"],
    5: ["Cesarean Section", "Gynecology", "CPT59510"]
}

# Anesthesia
anesthesia = {
    1: ["General Anesthesia", "IV", "Dr. Smith", "High"],
    2: ["Local Anesthesia", "Injection", "Dr. Adams", "Low"],
    3: ["Spinal Anesthesia", "Spinal", "Dr. Lee", "Medium"]
}

# Equipment
equipment = {
    1: ["Scalpel", "Surgical Tool", "MedTech", "MTX-101"],
    2: ["Heart Monitor", "Monitoring", "Philips", "PHL-200"],
    3: ["X-Ray Machine", "Imaging", "Siemens", "SIE-500"]
}

# Nurse
nurses = {
    1: ["Alice Brown", "Day", 5, "BSc Nursing"],
    2: ["John Davis", "Night", 8, "MSc Nursing"],
    3: ["Sophia Miller", "Day", 3, "Diploma Nursing"]
}

# Room
rooms = {
    1: ["ICU"],
    2: ["General Ward"],
    3: ["Operation Theater"]
}

# Blood Transfusion
blood = {
    1: ["A+", 2, "DON1001", "N"],
    2: ["B-", 1, "DON1002", "Y"],
    3: ["O+", 3, "DON1003", "N"]
}

# Billing
billing = {
    1: [50000, 45000, "Credit Card", 5000],
    2: [75000, 75000, "Insurance", 0],
    3: [30000, 20000, "Cash", 10000]
}

# Recovery
recovery = {
    1: ["ICU", 48, "N", "Y"],
    2: ["General", 24, "Y", "N"],
    3: ["Ward", 12, "N", "N"]
}

# Follow Up
followup = {
    1: ["2025-08-20", "Dr. Smith", "Physical", "2025-09-15"],
    2: ["2025-08-22", "Dr. Adams", "Virtual", "2025-09-05"],
    3: ["2025-08-25", "Dr. Lee", "Physical", "2025-09-10"]
}

# ----------------------------
# Generate fact table
# ----------------------------

data = []

for i in range(n):
    # Select random IDs
    proc_id = random.choice(list(procedures.keys()))
    anes_id = random.choice(list(anesthesia.keys()))
    equip_id = random.choice(list(equipment.keys()))
    nurse_id = random.choice(list(nurses.keys()))
    room_id = random.choice(list(rooms.keys()))
    blood_id = random.choice(list(blood.keys()))
    bill_id = random.choice(list(billing.keys()))
    rec_id = random.choice(list(recovery.keys()))
    foll_id = random.choice(list(followup.keys()))

    # Build row with attributes expanded
    row = [
        i+1,  # OperationID (Primary Key)

        proc_id, *procedures[proc_id],
        anes_id, *anesthesia[anes_id],
        equip_id, *equipment[equip_id],
        nurse_id, *nurses[nurse_id],
        room_id, *rooms[room_id],
        blood_id, *blood[blood_id],
        bill_id, *billing[bill_id],
        rec_id, *recovery[rec_id],
        foll_id, *followup[foll_id],

        # Measures
        random.randint(30, 300),  # Operation_DurationMinutes
        random.randint(20000, 100000),  # Operation_Cost
        random.choice(["Y", "N"]),  # Complications_Flag
        round(random.uniform(80, 99), 2),  # Success_Rate
        random.choice(["Y", "N"])   # Mortality_Flag
    ]

    data.append(row)

# ----------------------------
# Column Names
# ----------------------------
columns = [
    "OperationID",
    
    "ProcedureID", "Procedure_Type", "Procedure_Category", "Procedure_CPT_Code",
    "AnesthesiaID", "Anesthesia_Type", "Method", "Anesthetist", "Anesthesia_RiskLevel",
    "EquipmentID", "Equipment_Name", "Equipment_Type", "Equipment_Manufacturer", "Equipment_Model",
    "NurseID", "Nurse_FullName", "Nurse_Shift", "Nurse_ExperienceYears", "Nurse_Education",
    "RoomID", "Room_Type",
    "BloodTransfusionID", "Blood_Type", "Units_Transfused", "Donor_ID", "Transfusion_Complications",
    "BillingID", "Total_Charges", "Amount_Paid", "Payment_Method", "Outstanding_Balance",
    "RecoveryID", "Recovery_Room_Type", "Recovery_DurationHours", "Recovery_Complications", "Physiotherapy_Required",
    "FollowUpID", "FollowUp_Date", "FollowUp_Doctor", "FollowUp_Type", "Next_Appointment_Date",
    
    # Measures
    "Operation_DurationMinutes", "Operation_Cost", "Complications_Flag", "Success_Rate", "Mortality_Flag"
]

# ----------------------------
# Save to CSV
# ----------------------------
df = pd.DataFrame(data, columns=columns)
df.to_csv("fact_operations.csv", index=False)

print("✅ fact_operations.csv generated with", n, "records")
print(df.head(2))

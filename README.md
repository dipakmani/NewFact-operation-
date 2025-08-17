import pandas as pd
import random
import numpy as np

# Number of records
num_records = 500000

# -------------------------
# Helper functions
# -------------------------
def random_date():
    return pd.to_datetime("2020-01-01") + pd.to_timedelta(random.randint(0, 1825), unit="D")

def random_choice(options):
    return random.choice(options)

# -------------------------
# Generate Fact_Operations Dataset
# -------------------------
data = {
    # Operation IDs
    "OperationID": range(1, num_records + 1),

    # ProcedureID & Attributes
    "ProcedureID": np.random.randint(1000, 2000, num_records),
    "Procedure_Type": np.random.choice(["Surgery", "Biopsy", "Transplant", "Endoscopy"], num_records),
    "Procedure_Category": np.random.choice(["Cardiac", "Neuro", "Ortho", "General"], num_records),
    "Procedure_CPT_Code": np.random.randint(10000, 99999, num_records),

    # AnesthesiaID & Attributes
    "AnesthesiaID": np.random.randint(2000, 3000, num_records),
    "Anesthesia_Type": np.random.choice(["General", "Local", "Regional", "Sedation"], num_records),
    "Anesthesia_Dosage": np.random.randint(50, 300, num_records),
    "Anesthesia_Complications": np.random.choice(["Y", "N"], num_records),

    # EquipmentID & Attributes
    "EquipmentID": np.random.randint(3000, 4000, num_records),
    "Equipment_Name": np.random.choice(["Scalpel", "Monitor", "Ventilator", "ECG", "X-Ray Machine"], num_records),
    "Equipment_Type": np.random.choice(["Surgical", "Diagnostic", "Support"], num_records),
    "Equipment_Manufacturer": np.random.choice(["GE", "Philips", "Siemens", "Medtronic"], num_records),
    "Equipment_Model": np.random.choice(["X100", "M200", "S300", "V400"], num_records),

    # NurseID & Attributes
    "NurseID": np.random.randint(4000, 5000, num_records),
    "Nurse_FullName": np.random.choice(["Alice Brown", "John Smith", "Mary Johnson", "Robert Wilson"], num_records),
    "Nurse_Shift": np.random.choice(["Day", "Night"], num_records),
    "Nurse_ExperienceYears": np.random.randint(1, 30, num_records),
    "Nurse_Education": np.random.choice(["BSc Nursing", "MSc Nursing", "Diploma"], num_records),

    # RoomID & Attributes
    "RoomID": np.random.randint(5000, 6000, num_records),
    "Room_Type": np.random.choice(["ICU", "General", "Operation Theater"], num_records),

    # BloodTransfusionID & Attributes
    "BloodTransfusionID": np.random.randint(6000, 7000, num_records),
    "Blood_Type": np.random.choice(["A+", "A-", "B+", "B-", "O+", "O-", "AB+", "AB-"], num_records),
    "Units_Transfused": np.random.randint(1, 5, num_records),
    "Donor_ID": np.random.randint(7000, 8000, num_records),
    "Transfusion_Complications": np.random.choice(["Y", "N"], num_records),

    # BillingID & Attributes
    "BillingID": np.random.randint(8000, 9000, num_records),
    "Total_Charges": np.random.randint(10000, 500000, num_records),
    "Amount_Paid": np.random.randint(5000, 500000, num_records),
    "Payment_Method": np.random.choice(["Cash", "Card", "Insurance"], num_records),
    "Outstanding_Balance": np.random.randint(0, 20000, num_records),

    # RecoveryID & Attributes
    "RecoveryID": np.random.randint(9000, 10000, num_records),
    "Recovery_Room_Type": np.random.choice(["ICU", "Ward", "Private"], num_records),
    "Recovery_DurationHours": np.random.randint(1, 240, num_records),
    "Recovery_Complications": np.random.choice(["Y", "N"], num_records),
    "Physiotherapy_Required": np.random.choice(["Y", "N"], num_records),

    # FollowUpID & Attributes
    "FollowUpID": np.random.randint(10000, 11000, num_records),
    "FollowUp_Date": [random_date() for _ in range(num_records)],
    "FollowUp_Doctor": np.random.choice(["Dr. Adams", "Dr. Lee", "Dr. Patel", "Dr. Gomez"], num_records),
    "FollowUp_Type": np.random.choice(["Physical", "Virtual"], num_records),
    "Next_Appointment_Date": [random_date() for _ in range(num_records)],

    # Measures
    "Operation_DurationMinutes": np.random.randint(30, 600, num_records),
    "Operation_Cost": np.random.randint(5000, 200000, num_records),
    "Complications_Flag": np.random.choice(["Y", "N"], num_records),
    "Success_Rate": np.random.randint(70, 100, num_records),
    "Mortality_Flag": np.random.choice(["Y", "N"], num_records),
}

# Convert to DataFrame
df = pd.DataFrame(data)

# Save to CSV
df.to_csv("Fact_Operations.csv", index=False)

print("✅ Fact_Operations.csv generated successfully with", num_records, "records")

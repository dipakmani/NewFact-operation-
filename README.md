import pandas as pd
import numpy as np
from faker import Faker
import random

fake = Faker()

# Number of records
n = 500000  

# Generate IDs
operation_ids = [f"OP{100000+i}" for i in range(n)]
patient_ids = [f"P{random.randint(1000,9999)}" for _ in range(n)]
doctor_ids = [f"D{random.randint(100,999)}" for _ in range(n)]
procedure_ids = [f"PR{random.randint(100,999)}" for _ in range(n)]
anesthesia_ids = [f"A{random.randint(10,99)}" for _ in range(n)]
equipment_ids = [f"E{random.randint(200,400)}" for _ in range(n)]
nurse_ids = [f"N{random.randint(50,200)}" for _ in range(n)]
room_ids = [f"R{random.randint(1,50)}" for _ in range(n)]
bloodtransfusion_ids = [f"BT{random.randint(1,1000)}" for _ in range(n)]
billing_ids = [f"B{random.randint(10000,99999)}" for _ in range(n)]
recovery_ids = [f"RC{random.randint(1,500)}" for _ in range(n)]
followup_ids = [f"FU{random.randint(1,1000)}" for _ in range(n)]

# Procedure attributes
procedure_types = ["Bypass Surgery", "Appendectomy", "Hip Replacement", "Angioplasty", "Cataract Surgery"]
procedure_categories = ["Cardiac", "General Surgery", "Orthopedic", "Neuro", "Ophthalmology"]
procedure_cpt_codes = [f"CPT{random.randint(1000,9999)}" for _ in range(n)]

# Anesthesia attributes
anesthesia_types = ["General", "Local", "Regional", "Sedation"]
anesthesia_durations = np.random.randint(30, 240, n)  # minutes
anesthetist_names = [fake.name() for _ in range(n)]

# Equipment attributes
equipment_names = ["Scalpel", "ECG Monitor", "Defibrillator", "Endoscope", "Ventilator"]
equipment_types = ["Surgical", "Monitoring", "Support", "Diagnostic"]
equipment_manufacturers = ["Medtronic", "GE Healthcare", "Siemens", "Philips", "Johnson & Johnson"]
equipment_models = [f"Model-{random.randint(100,999)}" for _ in range(n)]

# Nurse attributes
nurse_names = [fake.name() for _ in range(n)]
nurse_shifts = ["Morning", "Evening", "Night"]
nurse_experience = np.random.randint(1, 30, n)
nurse_education = ["B.Sc Nursing", "GNM", "M.Sc Nursing"]

# Room attributes
room_types = ["ICU", "General", "Operation Theater"]

# Blood Transfusion attributes
blood_types = ["A+", "A-", "B+", "B-", "AB+", "AB-", "O+", "O-"]
transfusion_complications = ["Y", "N"]

# Billing attributes
payment_methods = ["Cash", "Credit Card", "Insurance", "Online Transfer"]

# Recovery attributes
recovery_room_types = ["ICU", "Step-Down Unit", "General Ward"]
recovery_complications = ["Y", "N"]
physiotherapy_required = ["Y", "N"]

# FollowUp attributes
followup_types = ["Physical", "Virtual"]

# Build dataset
data = {
    "OperationID": operation_ids,
    "PatientID": patient_ids,
    "DoctorID": doctor_ids,
    "ProcedureID": procedure_ids,
    "Procedure_Type": np.random.choice(procedure_types, n),
    "Procedure_Category": np.random.choice(procedure_categories, n),
    "Procedure_CPT_Code": procedure_cpt_codes,
    "AnesthesiaID": anesthesia_ids,
    "Anesthesia_Type": np.random.choice(anesthesia_types, n),
    "Anesthesia_DurationMinutes": anesthesia_durations,
    "Anesthetist_Name": anesthetist_names,
    "EquipmentID": equipment_ids,
    "Equipment_Name": np.random.choice(equipment_names, n),
    "Equipment_Type": np.random.choice(equipment_types, n),
    "Equipment_Manufacturer": np.random.choice(equipment_manufacturers, n),
    "Equipment_Model": equipment_models,
    "NurseID": nurse_ids,
    "Nurse_FullName": nurse_names,
    "Nurse_Shift": np.random.choice(nurse_shifts, n),
    "Nurse_ExperienceYears": nurse_experience,
    "Nurse_Education": np.random.choice(nurse_education, n),
    "RoomID": room_ids,
    "Room_Type": np.random.choice(room_types, n),
    "BloodTransfusionID": bloodtransfusion_ids,
    "Blood_Type": np.random.choice(blood_types, n),
    "Units_Transfused": np.random.randint(1, 5, n),
    "Donor_ID": [f"DNR{random.randint(1000,9999)}" for _ in range(n)],
    "Transfusion_Complications": np.random.choice(transfusion_complications, n),
    "BillingID": billing_ids,
    "Total_Charges": np.random.randint(5000, 200000, n),
    "Amount_Paid": np.random.randint(3000, 200000, n),
    "Payment_Method": np.random.choice(payment_methods, n),
    "Outstanding_Balance": np.random.randint(0, 50000, n),
    "RecoveryID": recovery_ids,
    "Recovery_Room_Type": np.random.choice(recovery_room_types, n),
    "Recovery_DurationHours": np.random.randint(1, 48, n),
    "Recovery_Complications": np.random.choice(recovery_complications, n),
    "Physiotherapy_Required": np.random.choice(physiotherapy_required, n),
    "FollowUpID": followup_ids,
    "FollowUp_Date": [fake.date_between(start_date="-1y", end_date="today") for _ in range(n)],
    "FollowUp_Doctor": [fake.name() for _ in range(n)],
    "FollowUp_Type": np.random.choice(followup_types, n),
    "Next_Appointment_Date": [fake.date_between(start_date="today", end_date="+6m") for _ in range(n)],
    # Fact Measures
    "Operation_DurationMinutes": np.random.randint(30, 600, n),
    "Operation_Cost": np.random.randint(10000, 500000, n),
    "Complications_Flag": np.random.choice(["Y", "N"], n),
    "Success_Rate(%)": np.random.randint(70, 100, n),
    "Mortality_Flag": np.random.choice(["Y", "N"], n),
}

# Create DataFrame
df = pd.DataFrame(data)

# Save to CSV
df.to_csv("Fact_Operations.csv", index=False)

print("✅ Fact_Operations dataset with 5 lakh records generated successfully!")

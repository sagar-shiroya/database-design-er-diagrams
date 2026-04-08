# Clinic Appointment and Diagnostics Platform

## Understanding

<img width="3161" height="2495" alt="image" src="https://github.com/user-attachments/assets/701df093-cb1f-420d-95a9-184b7df60c8d" />

<img width="2931" height="3540" alt="image" src="https://github.com/user-attachments/assets/5d702bf2-e070-47e3-846e-4a2d8d0b2acd" />

## ER Diagram

<img width="4732" height="3537" alt="image" src="https://github.com/user-attachments/assets/df15b3fc-c2b4-4d89-be38-fbbc1a0434e2" />



## ER Diagram Code

```markdown
notation crows-foot
patients [color: Yellow] {
  id SERIAL PK
  patient_name string
  mobile_numer string
  email string null
  age int
  height int //in cms
  weight int //in kgs
  blood_group string
}

doctors [color: Red] {
  id SERIAL PK
  doctor_name string
  email string
  birthday date null
  degree string
  experience int // in months
  salary int // in rupees
}

departments [color: Orange] {
  id SERIAL PK
  department_name  string
  floor_address string
  time_start datetime
  time_end datetime
  emergency_available boolean default false
}

doctor_departments {
  id SERIAL PK
  doctor_id FK
  department_id FK
  doctor_visit_start_time time
  duration int //in hours
  joined_at datetime
  created_at
  updated_at
}
doctor_departments.doctor_id > doctors.id: [color: red]
doctor_departments.department_id > departments.id: [color: orange]

appointments [color: Purple] {
  id SERIAL PK
  patient_id FK
  doctor_id FK
  appointed_time datetime
  created_at datetime
  updated_at datetime
}
appointments..patient_id > patients.id
appointments.doctor_id > doctors.id: [color: red]

visits [color: Green] {
  id SERIAL PK
  appointment_id FK
  doctor_id FK // this doc might change at patient visit time
  patient_weight INT // in kgs
  doctor_notes text
  created_at datetime
  updated_at datetime₹
}

visits.appointment_id > appointments.id: [color: purple]
visits.doctor_id > doctors.id: [color: red]

tests [color: Blue] {
  id SERIAL PK
  patient_id FK
  visit_id FK
  test_name string
  sample_collected boolean default false
  created_at datetime
  updated_at datetime
}
tests.patient_id > patients.id: [color: yellow]
tests.visit_id >visits.id: [color: green]

reports {
  id SERIAL PK
  test_id FK
  report_generated_at datetime
  generated_by FK
  created_at
  updated_at
}

reports.test_id > tests.id: [color: blue]
reports.generated_by > doctors.id: [color: red]

payments {
  id SERIAL PK
  patient_id FK
  transaction_id string
  payment_method enum(card|cash|UPI)
  total_charges double
  status enum(pending|in_progress|completed)
  visit_id FK null
  test_id FK null
  created_at datettime
  updated_at datetime
}
payments.patient_id >patients.id: [color: yellow]
payments.visit_id - visits.id: [color: green]
payments.test_id - tests.id: [color: blue]
```


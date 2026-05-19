# End-to-End Data Engineering Pipeline: Student AI Impact & Global Education Analytics

Proyek ini membangun pipa data (ETL Pipeline) otomatis secara *end-to-end* untuk mengolah dua dataset sektor pendidikan: dampak GenAI pada mahasiswa (50.000 baris) dan metrik edukasi global. Data diekstraksi dari sumber mentah, ditransformasikan ke dalam model skema bintang (*Star Schema*), dan dimuat ke dalam *Cloud Data Warehouse* PostgreSQL via Supabase.

## 🛠️ Tech Stack
- **Language:** Python 3.x
- **Data Manipulation:** Pandas, Jupyter Notebook
- **Database Connector:** SQLAlchemy, Psycopg2-binary
- **Data Warehouse:** PostgreSQL (Supabase Cloud Infrastructure)
- **Security & Ops:** Python-dotenv (Environment Variables), Connection Pooler (Session Mode)

## 📐 Arsitektur Data (Dimensional Modeling)

Untuk mengoptimalkan performa kueri analitik, tabel melebar (*wide table*) dari sumber mentah dipecah menjadi beberapa **Tabel Dimensi** (Konteks) dan **Tabel Fakta** (Metrik Numerik).

### 1. Dataset Impact AI Siswa (Star Schema)
- **`dim_student`**: `Student_ID` (PK), `Major_Category`, `Year_of_Study`
- **`dim_ai_profile`**: `ai_profile_id` (PK), `Primary_Use_Case`, `Prompt_Engineering_Skill`, `Paid_Subscription`
- **`dim_policy`**: `policy_id` (PK), `Institutional_Policy`
- **`dim_risk`**: `risk_id` (PK), `Burnout_Risk_Level`
- **`fact_student_ai_impact`**: `fact_id` (PK), Foreign Keys (`student_id`, `ai_profile_id`, `policy_id`, `risk_id`), dan 8 metrik numerik (IPK, Jam Belajar, Tingkat Stres, dll).

### 2. Dataset Global Education Metrics
- **`dim_country`**: `country_id` (PK), `Countries_and_areas`, `Latitude`, `Longitude`
- **`fact_global_education_metrics`**: `fact_id` (PK), `country_id` (FK), serta 20+ metrik kuantitatif (OOSR, Completion Rate, Unemployment Rate, Birth Rate).

## 🚀 Fitur Utama & Penyelesaian Masalah (Engineering Highlights)
- **IPv4 Connection Workaround:** Mengatasi limitasi jaringan lokal dengan mengimplementasikan **Supabase Connection Pooler** (port 5432) berbasis IPv6-to-IPv4 proxy agar transaksi data ke *cloud* tetap stabil tanpa *timeout*.
- **Data Integrity & Constraints:** Menangani urutan eksekusi *Load* secara ketat—memasukkan tabel dimensi terlebih dahulu sebelum tabel fakta untuk mencegah kegagalan *Foreign Key Constraint Violation*.
- **Security Best Practices:** Mengisolasi kredensial database sensitif menggunakan variabel lingkungan (`.env`) agar terhindar dari kebocoran data di repositori publik.

## 📁 Struktur Direktori
```text
├── .env                  # Kredensial Database (Disembunyikan)
├── .gitignore            # Daftar file yang diabaikan oleh Git
├── README.md             # Dokumentasi Proyek
├── pipeline_ai.ipynb     # Script ETL Dataset AI Student
├── pipeline_edu.ipynb    # Script ETL Dataset Global Education
├── Global_Education.csv  # Dataset Mentah Global Education
└── ai_student_impact.csv # Dataset Mentah AI Student Impact

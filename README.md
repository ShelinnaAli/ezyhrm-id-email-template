# Panduan Integrasi Template Email - EzyHRM
## Email Notification Templates

Dokumen ini adalah referensi kontrak data (*data contract*) untuk tim backend (NestJS) dalam memasang template email notifikasi sistem **EzyHRM**.

Semua template telah dirancang dengan standar baku **Email Client Best Practice** (menggunakan *table-based layout*, *inline CSS*, font **Inter**, *Outlook VML bulletproof button*, serta *mobile-responsive styling*).

---

## 📁 Struktur File & Aset

```text
├── onboarding-to-employee-email.html   # Template 1: Email Selamat Datang & Kredensial (ke Karyawan)
├── onboarding-to-hr-email.html         # Template 2: Email Onboarding Selesai (ke Tim HR)
├── change-password-to-employee.html    # Template 3: Email Permintaan Perubahan Kata Sandi (ke Karyawan)
├── leave-request-to-approver.html      # Template 4: Email Permintaan Persetujuan Cuti (ke Approver / Atasan)
├── leave-request-to-hr.html            # Template 5: Email Pemberitahuan Pengajuan Cuti Dibuat (ke Tim HR)
├── claim-request-to-approver.html      # Template 6: Email Permintaan Persetujuan Klaim (ke Approver / Atasan)
├── claim-request-to-hr.html            # Template 7: Email Pemberitahuan Pengajuan Klaim Dibuat (ke Tim HR)
├── submission-status-update.html       # Template 8: Master Status Update (Approve / Reject ke Employee & HR)
├── payslip-published-to-employee.html  # Template 9: Notifikasi Slip Gaji Diterbitkan (ke Karyawan)
├── contract-end-notification.html      # Template 10: Master Notifikasi Berakhir Kontrak (Manager, Approver & HR)
├── assets/
│   ├── ezyhrmLogo.png                  # Logo EzyHRM (PNG Transparan High-Res)
│   ├── union1.png                      # Icon Dekoratif Aksen Hijau Atas (Semua Template)
│   ├── union2.png                      # Icon Dekoratif Aksen Hijau Bawah (Semua Template)
│   ├── magicWandIcon.png               # Ilustrasi Tongkat Sihir (untuk onboarding-to-employee)
│   ├── jobProfileIcon.png              # Ilustrasi Profil Pekerjaan (untuk onboarding, payslip & contract)
│   ├── laptopLockIcon.png              # Ilustrasi Kunci Laptop (untuk change-password-to-employee)
│   └── formEditionIcon.png             # Ilustrasi Form Cuti, Klaim & Submission Status
└── README.md                           # Panduan integrasi & daftar binding data ini
```

---

## 🗺️ Matriks Pemetaan 23 Email Notification EzyHRM

Sesuai *best practice* arsitektur email enterprise, seluruh **23 skenario email notifikasi** di EzyHRM didukung secara efisien oleh **10 master template** modular di atas:

| No | Nama Notifikasi Email (Skenario Bisnis) | Penerima | Template HTML yang Digunakan |
| :---: | :--- | :--- | :--- |
| 1 | Onboarding Welcome & Account Credential | Karyawan Baru | `onboarding-to-employee-email.html` |
| 2 | Onboarding Completion Notification | Tim HR | `onboarding-to-hr-email.html` |
| 3 | Password Reset Request | Karyawan | `change-password-to-employee.html` |
| 4 | Leave - Request Submission Notification | Approver / Atasan | `leave-request-to-approver.html` |
| 5 | Leave - Request Submission Notification | Tim HR | `leave-request-to-hr.html` |
| 6 | Claim - Request Submission Notification | Approver / Atasan | `claim-request-to-approver.html` |
| 7 | Claim - Request Submission Notification | Tim HR & Finance | `claim-request-to-hr.html` |
| 8 | Overtime - Request Submission Notification | Approver / Atasan | `leave-request-to-approver.html` *(atau blueprint klaim)* |
| 9 | Overtime - Request Submission Notification | Tim HR | `leave-request-to-hr.html` *(atau blueprint klaim)* |
| 10 | Attendance - Request Submission Notification | Approver / Atasan | `leave-request-to-approver.html` *(atau blueprint klaim)* |
| 11 | Attendance - Request Submission Notification | Tim HR | `leave-request-to-hr.html` *(atau blueprint klaim)* |
| 12 | Data Profile - Request Submission Notification | Approver / Atasan | `leave-request-to-approver.html` *(atau blueprint klaim)* |
| 13 | Data Profile - Request Submission Notification | Tim HR | `leave-request-to-hr.html` *(atau blueprint klaim)* |
| 14 | Submission Status Update: Approve | Karyawan | `submission-status-update.html` *(status_badge: DISETUJUI)* |
| 15 | Submission Status Update: Approve | Tim HR | `submission-status-update.html` *(status_badge: DISETUJUI)* |
| 16 | Submission Status Update: Reject | Karyawan | `submission-status-update.html` *(status_badge: DITOLAK)* |
| 17 | Submission Status Update: Reject | Tim HR | `submission-status-update.html` *(status_badge: DITOLAK)* |
| 18 | Payslip Published Notification | Karyawan | `payslip-published-to-employee.html` |
| 19 | Contract end - New notification | Manager | `contract-end-notification.html` |
| 20 | Contract end - New notification | Approver & HR | `contract-end-notification.html` |
| 21 | Contract end - Reminder | Approver | `contract-end-notification.html` |
| 22 | Contract end - Reminder | Tim HR | `contract-end-notification.html` |
| 23 | Contract end - Expired | Tim HR | `contract-end-notification.html` |

> **Tips untuk NestJS:**  
> File `.html` dapat langsung digunakan atau di-rename menjadi `.hbs` sesuai konfigurasi folder `templates` di modul mailer NestJS Anda.

---

## 🎨 Aset Gambar Bersama (Global Brand Assets)

Setiap template email memiliki elemen visual identitas brand EzyHRM yang seragam:

| Nama Variabel | Tipe Data | Wajib? | File Sumber | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | `assets/ezyhrmLogo.png` | URL publik HTTPS logo EzyHRM di header. |
| `union1_url` | `string` | **Ya** | `assets/union1.png` | Icon dekoratif transparan bagian atas pada aksen hijau banner. |
| `union2_url` | `string` | **Ya** | `assets/union2.png` | Icon dekoratif transparan bagian bawah pada aksen hijau banner. |
| `support_url` | `string` | **Ya** | Portal Web | URL web portal Jira Service Desk: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Sistem | Tahun hak cipta di footer. Contoh: `2026` |

---

## 📋 1. Template: `onboarding-to-employee-email.html`
> **Penerima:** Karyawan Baru (`employee_email`)  
> **Tujuan:** Notifikasi pembuatan akun karyawan baru, memberikan kredensial sementara, dan instruksi aktivasi.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `banner_wand_url` | `string` | **Ya** | URL ilustrasi banner tongkat sihir (`assets/magicWandIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan baru. Contoh: `Alexander Christian` |
| `employee_email` | `string` | **Ya** | Alamat email login akun karyawan. Contoh: `alexander@company.com` |
| `temporary_password` | `string` | **Ya** | Kata sandi sementara yang di-generate sistem. Contoh: `Welcome2026!` |
| `login_url` | `string` | **Ya** | URL tujuan tombol CTA "Masuk Sekarang" & fallback link. Contoh: `https://ezyhrm.id/login` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

---

## 📋 2. Template: `onboarding-to-hr-email.html`
> **Penerima:** Tim HR (Email HR / PIC Onboarding)  
> **Tujuan:** Memberitahukan Tim HR bahwa seorang karyawan telah resmi menyelesaikan seluruh tugas onboarding.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `job_profile_url` | `string` | **Ya** | URL ilustrasi banner onboarding (`assets/jobProfileIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan yang telah selesai onboarding. Contoh: `Alexander Christian` |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Tipe kepegawaian. Contoh: `Full-time (PKWTT)` atau `Kontrak (PKWT)` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

> **Catatan Salam Pembuka:**  
> Pada template ini, salam pembuka dibuat statis **`Halo Tim HR,`** karena ditujukan khusus untuk internal tim HR.

---

## 📋 3. Template: `change-password-to-employee.html`
> **Penerima:** Karyawan (`employee_email`)  
> **Tujuan:** Notifikasi permintaan pembaruan / perubahan kata sandi akun karyawan lengkap dengan panduan tahapan keamanan.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `laptop_lock_url` | `string` | **Ya** | URL ilustrasi banner kunci laptop (`assets/laptopLockIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan yang meminta reset kata sandi. Contoh: `Alexander Christian` |
| `reset_password_url` | `string` | **Ya** | URL tautan reset kata sandi dengan token aman (pada tombol "Atur Ulang Kata Sandi"). Contoh: `https://ezyhrm.id/reset-password?token=xyz...` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

> **Catatan Validitas Link:**  
> Link reset kata sandi pada template ini diinformasikan hanya berlaku selama **60 menit**.

---

## 📋 4. Template: `leave-request-to-approver.html`
> **Penerima:** Approver / Manajer / Atasan (`approver_email`)  
> **Tujuan:** Notifikasi pengajuan cuti dari anggota tim yang membutuhkan peninjauan dan persetujuan.

### Struktur Card 1:
1. **Header Top (3 Kolom Horizontal, Background White):** Berisi profil karyawan pemohon (Nama Karyawan, Posisi/Jabatan, dan Tipe Karyawan).
2. **Detail Pengajuan Cuti (2 Kolom Grid, Background Card `#F4F4F4`):**
   * **Kolom Kiri:** Jenis Cuti, Tanggal Mulai, Tanggal Selesai, dan Durasi Jam Kerja.
   * **Kolom Kanan:** Total Hari Cuti dan Deskripsi Cuti.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `form_edition_url` | `string` | **Ya** | URL ilustrasi banner pengajuan cuti (`assets/formEditionIcon.png`). |
| `approver_name` | `string` | **Ya** | Nama atasan / approver penerima email pada salam pembuka. Contoh: `Budi Santoso` |
| `employee_name` | `string` | **Ya** | Nama karyawan yang mengajukan cuti. Contoh: `Alexander Christian` |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan pemohon. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Status kepegawaian karyawan pemohon. Contoh: `Full-time (PKWTT)` |
| `leave_type` | `string` | **Ya** | Jenis cuti yang diajukan. Contoh: `Cuti Tahunan` atau `Cuti Khusus` |
| `start_date` | `string` | **Ya** | Tanggal awal cuti. Contoh: `20 Okt 2026` |
| `end_date` | `string` | **Ya** | Tanggal akhir cuti. Contoh: `22 Okt 2026` |
| `working_hours` | `string` | **Ya** | Durasi jam kerja per hari. Contoh: `08:00 - 17:00 (8 Jam)` |
| `total_leave_days` | `string` | **Ya** | Total hari cuti yang diambil. Contoh: `3 Hari Kerja` |
| `leave_description` | `string` | **Ya** | Keterangan / alasan pengajuan cuti. Contoh: `Keperluan keluarga di luar kota` |
| `approve_leave_url` | `string` | **Ya** | URL tujuan tombol CTA "Tinjau & Setujui Cuti". Contoh: `https://ezyhrm.id/leaves/approvals/123` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

> 💡 **Panduan Penggunaan Kembali (*Reusability*) untuk Modul Lain ke Approver:**  
> Template ini dirancang sebagai **Master Blueprint untuk seluruh pengajuan yang membutuhkan persetujuan atasan**. Backend NestJS dapat langsung menggunakannya untuk:
> * **Overtime (Pengajuan Lembur):** Ganti teks banner menjadi *"Permintaan Persetujuan Lembur"*, isi kolom dengan tanggal lembur, jam mulai, jam selesai, total jam lembur, dan alasan lembur.
> * **Attendance (Koreksi Absensi):** Ganti teks banner menjadi *"Persetujuan Koreksi Kehadiran"*, isi kolom dengan tanggal absensi, jam masuk/pulang baru, dan alasan koreksi.
> * **Data Profile Change (Perubahan Data Karyawan):** Ganti teks banner menjadi *"Persetujuan Pembaruan Data Profil"*, isi kolom dengan jenis data yang diubah, nilai lama, dan nilai baru.

---

## 📋 5. Template: `leave-request-to-hr.html`
> **Penerima:** Tim HR (Email HR / PIC Personalia)  
> **Tujuan:** Pemberitahuan informatif kepada HR bahwa terdapat pengajuan cuti baru yang telah dibuat dalam sistem dan sedang dalam proses peninjauan oleh approver terkait.

### Struktur Card 1:
1. **Header Top (3 Kolom Horizontal, Background White):** Berisi profil karyawan pemohon (Nama Karyawan, Posisi/Jabatan, dan Tipe Karyawan).
2. **Detail Pengajuan Cuti (2 Kolom Grid, Background Card `#F4F4F4`):**
   * **Kolom Kiri:** Jenis Cuti, Tanggal Mulai, Tanggal Selesai, dan Durasi Jam Kerja.
   * **Kolom Kanan:** Total Hari Cuti dan Deskripsi Cuti.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `form_edition_url` | `string` | **Ya** | URL ilustrasi banner pengajuan cuti (`assets/formEditionIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama karyawan yang mengajukan cuti. Contoh: `Alexander Christian` |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan pemohon. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Status kepegawaian karyawan pemohon. Contoh: `Full-time (PKWTT)` |
| `leave_type` | `string` | **Ya** | Jenis cuti yang diajukan. Contoh: `Cuti Tahunan` atau `Cuti Khusus` |
| `start_date` | `string` | **Ya** | Tanggal awal cuti. Contoh: `20 Okt 2026` |
| `end_date` | `string` | **Ya** | Tanggal akhir cuti. Contoh: `22 Okt 2026` |
| `working_hours` | `string` | **Ya** | Durasi jam kerja per hari. Contoh: `08:00 - 17:00 (8 Jam)` |
| `total_leave_days` | `string` | **Ya** | Total hari cuti yang diambil. Contoh: `3 Hari Kerja` |
| `leave_description` | `string` | **Ya** | Keterangan / alasan pengajuan cuti. Contoh: `Keperluan keluarga di luar kota` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

> **Catatan Teknis Template HR:**  
> * Salam pembuka dibuat statis **`Halo Tim HR,`**.
> * Template ini bersifat **informatif** (*FYI* / update status), sehingga **tidak memiliki tombol CTA persetujuan** (tindakan persetujuan dilakukan oleh Approver melalui Template 4).
> 
> 💡 **Panduan Penggunaan Kembali (*Reusability*) untuk Modul Lain ke HR:**  
> Template ini juga berfungsi sebagai **Master Blueprint untuk seluruh pemberitahuan pengajuan baru ke Tim HR** (format informatif tanpa tombol aksi), termasuk:
> * **Overtime Notification ke Tim HR:** Pemberitahuan bahwa ada pengajuan lembur yang telah dikirim ke atasan.
> * **Attendance Notification ke Tim HR:** Pemberitahuan bahwa ada pengajuan koreksi absensi yang masuk.
> * **Data Profile Notification ke Tim HR:** Pemberitahuan bahwa ada permintaan pembaruan data profil karyawan.

---

## 📋 6. Template: `claim-request-to-approver.html`
> **Penerima:** Approver / Manajer / Atasan (`approver_email`)  
> **Tujuan:** Notifikasi pengajuan klaim reimbursement dari anggota tim yang membutuhkan peninjauan dan persetujuan.

### Struktur Card 1:
1. **Header Top (3 Kolom Horizontal, Background White):** Berisi profil karyawan pemohon (Nama Karyawan, Posisi/Jabatan, dan Tipe Karyawan).
2. **Detail Pengajuan Klaim (2 Kolom Grid, Background Card `#F4F4F4`):**
   * **Kolom Kiri:** Tipe Klaim, Tanggal Transaksi, dan Tanggal Pengajuan Klaim.
   * **Kolom Kanan:** Total Klaim dan Deskripsi Klaim.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `form_edition_url` | `string` | **Ya** | URL ilustrasi banner pengajuan klaim (`assets/formEditionIcon.png`). |
| `approver_name` | `string` | **Ya** | Nama atasan / approver penerima email pada salam pembuka. Contoh: `Budi Santoso` |
| `employee_name` | `string` | **Ya** | Nama karyawan yang mengajukan klaim. Contoh: `Alexander Christian` |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan pemohon. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Status kepegawaian karyawan pemohon. Contoh: `Full-time (PKWTT)` |
| `claim_type` | `string` | **Ya** | Tipe klaim yang diajukan. Contoh: `Medical Reimbursement` atau `Transportasi & Perjalanan Dinas` |
| `transaction_date` | `string` | **Ya** | Tanggal terjadinya transaksi/pengeluaran. Contoh: `14 Okt 2026` |
| `claim_date` | `string` | **Ya** | Tanggal pengajuan klaim dibuat. Contoh: `16 Okt 2026` |
| `total_claim_amount` | `string` | **Ya** | Jumlah total biaya klaim yang diajukan. Contoh: `Rp 1.250.000` |
| `claim_description` | `string` | **Ya** | Deskripsi / rincian pengeluaran klaim. Contoh: `Biaya rawat jalan dan resep obat klinik Kimia Farma` |
| `approve_claim_url` | `string` | **Ya** | URL tujuan tombol CTA "Tinjau & Setujui Klaim". Contoh: `https://ezyhrm.id/claims/approvals/456` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

---

## 📋 7. Template: `claim-request-to-hr.html`
> **Penerima:** Tim HR (Email HR / Finance / PIC Personalia)  
> **Tujuan:** Pemberitahuan informatif kepada HR bahwa terdapat pengajuan klaim reimbursement baru yang telah dibuat dalam sistem dan sedang dalam proses peninjauan oleh approver terkait untuk pemantauan anggaran HR & Finance.

### Struktur Card 1:
1. **Header Top (3 Kolom Horizontal, Background White):** Berisi profil karyawan pemohon (Nama Karyawan, Posisi/Jabatan, dan Tipe Karyawan).
2. **Detail Pengajuan Klaim (2 Kolom Grid, Background Card `#F4F4F4`):**
   * **Kolom Kiri:** Tipe Klaim, Tanggal Transaksi, dan Tanggal Pengajuan Klaim.
   * **Kolom Kanan:** Total Klaim dan Deskripsi Klaim.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `form_edition_url` | `string` | **Ya** | URL ilustrasi banner pengajuan klaim (`assets/formEditionIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama karyawan yang mengajukan klaim. Contoh: `Alexander Christian` |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan pemohon. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Status kepegawaian karyawan pemohon. Contoh: `Full-time (PKWTT)` |
| `claim_type` | `string` | **Ya** | Tipe klaim yang diajukan. Contoh: `Medical Reimbursement` atau `Transportasi & Perjalanan Dinas` |
| `transaction_date` | `string` | **Ya** | Tanggal terjadinya transaksi/pengeluaran. Contoh: `14 Okt 2026` |
| `claim_date` | `string` | **Ya** | Tanggal pengajuan klaim dibuat. Contoh: `16 Okt 2026` |
| `total_claim_amount` | `string` | **Ya** | Jumlah total biaya klaim yang diajukan. Contoh: `Rp 1.250.000` |
| `claim_description` | `string` | **Ya** | Deskripsi / rincian pengeluaran klaim. Contoh: `Biaya rawat jalan dan resep obat klinik Kimia Farma` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

> **Catatan Teknis Template HR:**  
> * Salam pembuka dibuat statis **`Halo Tim HR,`**.
> * Template ini bersifat **informatif** (*FYI* / monitoring), sehingga **tidak memiliki tombol CTA persetujuan** (tindakan persetujuan dilakukan oleh Approver melalui Template 6).

---

## 📋 8. Template: `submission-status-update.html` (Master Status Update)
> **Penerima:** Karyawan (`employee_email`) dan/atau Tim HR (`hr_email`)  
> **Tujuan:** Notifikasi hasil keputusan pengajuan (Disetujui / Ditolak / Approved / Rejected) untuk semua modul (Cuti, Klaim, Lembur, Kehadiran, Perubahan Data Profil).

### Skenario yang Didukung (4 Email):
1. **Submission Approved (ke Karyawan):** `status_badge: "DISETUJUI"`, `status_color: "#2f855a"`, `status_bg: "#f0fdf4"`, `status_border: "#bbf7d0"`
2. **Submission Approved (ke Tim HR):** `status_badge: "DISETUJUI"`
3. **Submission Rejected (ke Karyawan):** `status_badge: "DITOLAK"`, `status_color: "#c53030"`, `status_bg: "#fff5f5"`, `status_border: "#fecaca"`
4. **Submission Rejected (ke Tim HR):** `status_badge: "DITOLAK"`

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `form_edition_url` | `string` | **Ya** | URL ilustrasi banner (`assets/formEditionIcon.png`). |
| `preheader_text` | `string` | **Ya** | Teks preview inbox. Contoh: `Pengajuan Cuti Tahunan Anda telah disetujui.` |
| `banner_title` | `string` | **Ya** | Judul banner. Contoh: `Pengajuan Disetujui` atau `Status Pengajuan Ditolak` |
| `banner_description` | `string` | **Ya** | Deskripsi banner. Contoh: `Pengajuan Anda telah diproses oleh atasan.` |
| `recipient_name` | `string` | **Ya** | Nama penerima email pada salam pembuka. Contoh: `Alexander Christian` atau `Tim HR` |
| `intro_message` | `string` | **Ya** | Kalimat pengantar. Contoh: `Berikut adalah pembaruan status terkait pengajuan yang telah ditinjau.` |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan pemohon. |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan. |
| `employment_type` | `string` | **Ya** | Status kepegawaian. Contoh: `Full-time (PKWTT)` |
| `status_badge` | `string` | **Ya** | Label status pill: `DISETUJUI` atau `DITOLAK` |
| `status_color` | `string` | Opsional | Warna teks badge (Hijau: `#2f855a`, Merah: `#c53030`). Default: `#2f855a` |
| `status_bg` | `string` | Opsional | Background badge (Hijau: `#f0fdf4`, Merah: `#fff5f5`). Default: `#f0fdf4` |
| `status_border` | `string` | Opsional | Border badge (Hijau: `#bbf7d0`, Merah: `#fecaca`). Default: `#bbf7d0` |
| `submission_type` | `string` | **Ya** | Jenis formulir. Contoh: `Cuti Tahunan`, `Klaim Rawat Jalan`, `Lembur Proyek` |
| `submission_date` | `string` | **Ya** | Tanggal pengajuan dibuat. Contoh: `15 Okt 2026` |
| `processed_by` | `string` | **Ya** | Nama atasan yang memproses. Contoh: `Budi Santoso (Engineering Lead)` |
| `decision_date` | `string` | **Ya** | Tanggal persetujuan/penolakan. Contoh: `16 Okt 2026` |
| `approval_notes` | `string` | **Ya** | Catatan atasan atau alasan penolakan. Contoh: `Disetujui, silakan atur handover pekerjaan.` |
| `view_detail_url` | `string` | **Ya** | URL tombol CTA "Lihat Detail Pengajuan". Contoh: `https://ezyhrm.id/requests/123` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

---

## 📋 9. Template: `payslip-published-to-employee.html`
> **Penerima:** Karyawan (`employee_email`)  
> **Tujuan:** Notifikasi bahwa slip gaji resmi periode tertentu telah terbit dan siap diunduh melalui portal EzyHRM.

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `job_profile_url` | `string` | **Ya** | URL ilustrasi profil pekerjaan (`assets/jobProfileIcon.png`). |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan penerima slip gaji. |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan. |
| `employment_type` | `string` | **Ya** | Status kepegawaian. |
| `payroll_period` | `string` | **Ya** | Periode bulan & tahun penggajian. Contoh: `Oktober 2026` |
| `payment_date` | `string` | **Ya** | Tanggal payroll ditransfer. Contoh: `25 Okt 2026` |
| `bank_account` | `string` | **Ya** | Informasi rekening tujuan. Contoh: `BCA •••• 5678` |
| `payment_status` | `string` | **Ya** | Status transfer. Contoh: `Berhasil Ditransfer` |
| `payroll_type` | `string` | **Ya** | Tipe penggajian. Contoh: `Gaji Reguler Bulanan` atau `THR / Bonus` |
| `payroll_notes` | `string` | **Ya** | Catatan tim finance/payroll. Contoh: `Dokumen slip gaji resmi terenkripsi demi keamanan data privasi Anda.` |
| `download_payslip_url`| `string` | **Ya** | URL tombol CTA "Lihat & Unduh Slip Gaji". Contoh: `https://ezyhrm.id/payroll/payslips/2026-10` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

---

## 📋 10. Template: `contract-end-notification.html` (Master Notifikasi Kontrak)
> **Penerima:** Manager / Approver / Tim HR  
> **Tujuan:** Notifikasi peringatan masa berakhirnya kontrak kerja karyawan (PKWT), pengingat evaluasi (*reminder*), serta pemberitahuan kontrak berakhir (*expired*).

### Skenario yang Didukung (5 Email):
1. **Contract end - New notification (MANAGER):** Peringatan awal (H-30 / H-60) kepada Manager untuk evaluasi performa karyawan.
2. **Contract end - New notification (APPROVER & HR):** Peringatan awal kepada atasan & HR untuk menyiapkan administrasi evaluasi.
3. **Contract end - Reminder (APPROVER):** Pengingat tindak lanjut (H-14 / H-7) kepada atasan.
4. **Contract end - Reminder (HR):** Pengingat tindak lanjut (H-14 / H-7) kepada HR.
5. **Contract end - Expired (HR):** Notifikasi resmi per hari ini bahwa masa kontrak karyawan telah berakhir (*status: Expired*).

### Binding Variabel (Data Contract):

| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url` | `string` | **Ya** | URL logo EzyHRM (`assets/ezyhrmLogo.png`). |
| `union1_url` | `string` | **Ya** | Icon dekoratif aksen atas (`assets/union1.png`). |
| `union2_url` | `string` | **Ya** | Icon dekoratif aksen bawah (`assets/union2.png`). |
| `job_profile_url` | `string` | **Ya** | URL ilustrasi banner (`assets/jobProfileIcon.png`). |
| `preheader_text` | `string` | **Ya** | Teks preview inbox. Contoh: `Masa kontrak kerja karyawan akan segera berakhir.` |
| `banner_title` | `string` | **Ya** | Judul banner. Contoh: `Pemberitahuan Masa Kontrak` / `Pengingat Kontrak Kerja` / `Kontrak Kerja Berakhir` |
| `banner_description` | `string` | **Ya** | Deskripsi banner. Contoh: `Informasi masa berakhir kontrak kerja PKWT untuk evaluasi perpanjangan.` |
| `recipient_name` | `string` | **Ya** | Nama penerima: `Bpk/Ibu [Nama Manager]` / `Tim HR` |
| `intro_message` | `string` | **Ya** | Kalimat pengantar detail sesuai skenario (New/Reminder/Expired). |
| `employee_name` | `string` | **Ya** | Nama karyawan yang bersangkutan. |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan. |
| `employment_type` | `string` | **Ya** | Tipe kepegawaian. Contoh: `PKWT (Kontrak)` |
| `contract_start_date`| `string` | **Ya** | Tanggal awal kontrak kerja. Contoh: `01 Nov 2025` |
| `contract_end_date` | `string` | **Ya** | Tanggal akhir kontrak kerja. Contoh: `31 Okt 2026` |
| `remaining_days` | `string` | **Ya** | Sisa hari aktif. Contoh: `30 Hari Lagi`, `7 Hari Lagi`, `Berakhir Hari Ini` |
| `contract_status` | `string` | **Ya** | Status tindak lanjut. Contoh: `Perlu Evaluasi Perpanjangan` atau `Expired` |
| `department` | `string` | **Ya** | Departemen/Divisi karyawan. Contoh: `Technology & Engineering` |
| `contract_notes` | `string` | **Ya** | Catatan tambahan HR / PIC. |
| `contract_action_url`| `string` | **Ya** | URL tombol CTA "Tinjau Status Kontrak". Contoh: `https://ezyhrm.id/contracts/evaluations/789` |
| `support_url` | `string` | **Ya** | URL portal bantuan: `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133` |
| `year` | `number` / `string` | Opsional | Tahun hak cipta di footer. Contoh: `2026` |

---

## 🚀 Contoh Implementasi di NestJS

Jika backend menggunakan modul **`@nestjs-modules/mailer`** dengan template engine **Handlebars (`hbs`)**, berikut contoh implementasi pada Service:

```typescript
import { Injectable } from '@nestjs/common';
import { MailerService } from '@nestjs-modules/mailer';

@Injectable()
export class NotificationService {
  constructor(private readonly mailerService: MailerService) {}

  private readonly cdnBase = process.env.CDN_BASE_URL || 'https://cdn.ezyhrm.id/assets';
  private readonly appUrl = process.env.APP_URL || 'https://ezyhrm.id';
  
  // URL Portal Bantuan IT RMA Service Desk
  private readonly supportPortalUrl =
    'https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133';

  /**
   * Helper untuk menyisipkan aset brand bersama (Logo & Aksen Hijau)
   */
  private getBrandAssets() {
    return {
      logo_url: `${this.cdnBase}/ezyhrmLogo.png`,
      union1_url: `${this.cdnBase}/union1.png`,
      union2_url: `${this.cdnBase}/union2.png`,
      support_url: this.supportPortalUrl,
      year: new Date().getFullYear(),
    };
  }

  /**
   * 1. Kirim Email ke Karyawan Baru (Welcome & Onboarding)
   */
  async sendWelcomeEmployeeEmail(employee: { name: string; email: string; tempPass: string }) {
    await this.mailerService.sendMail({
      to: employee.email,
      subject: 'Selamat Bergabung dengan Tim - Kredensial Akun EzyHRM Anda',
      template: './onboarding-to-employee-email',
      context: {
        ...this.getBrandAssets(),
        banner_wand_url: `${this.cdnBase}/magicWandIcon.png`,
        employee_name: employee.name,
        employee_email: employee.email,
        temporary_password: employee.tempPass,
        login_url: `${this.appUrl}/login`,
      },
    });
  }

  /**
   * 2. Kirim Notifikasi ke Tim HR saat Karyawan Selesai Onboarding
   */
  async sendOnboardingCompletedToHrEmail(data: {
    hrEmail: string;
    employeeName: string;
    position: string;
    employmentType: string;
  }) {
    await this.mailerService.sendMail({
      to: data.hrEmail,
      subject: `Onboarding Selesai: ${data.employeeName} (${data.position})`,
      template: './onboarding-to-hr-email',
      context: {
        ...this.getBrandAssets(),
        job_profile_url: `${this.cdnBase}/jobProfileIcon.png`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
      },
    });
  }

  /**
   * 3. Kirim Notifikasi Perubahan Kata Sandi ke Karyawan
   */
  async sendChangePasswordEmail(employee: { name: string; email: string; resetToken: string }) {
    await this.mailerService.sendMail({
      to: employee.email,
      subject: 'Permintaan Perubahan Kata Sandi Akun - EzyHRM',
      template: './change-password-to-employee',
      context: {
        ...this.getBrandAssets(),
        laptop_lock_url: `${this.cdnBase}/laptopLockIcon.png`,
        employee_name: employee.name,
        reset_password_url: `${this.appUrl}/reset-password?token=${employee.resetToken}`,
      },
    });
  }

  /**
   * 4. Kirim Notifikasi Permintaan Persetujuan Cuti ke Approver
   */
  async sendLeaveRequestToApproverEmail(data: {
    approverEmail: string;
    approverName: string;
    employeeName: string;
    position: string;
    employmentType: string;
    leaveType: string;
    startDate: string;
    endDate: string;
    workingHours: string;
    totalDays: string;
    description: string;
    leaveId: string | number;
  }) {
    await this.mailerService.sendMail({
      to: data.approverEmail,
      subject: `Pengajuan Cuti Membutuhkan Persetujuan: ${data.employeeName} (${data.leaveType})`,
      template: './leave-request-to-approver',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        approver_name: data.approverName,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        leave_type: data.leaveType,
        start_date: data.startDate,
        end_date: data.endDate,
        working_hours: data.workingHours,
        total_leave_days: data.totalDays,
        leave_description: data.description,
        approve_leave_url: `${this.appUrl}/leaves/approvals/${data.leaveId}`,
      },
    });
  }

  /**
   * 5. Kirim Notifikasi Pembuatan Pengajuan Cuti ke Tim HR
   */
  async sendLeaveNotificationToHrEmail(data: {
    hrEmail: string;
    employeeName: string;
    position: string;
    employmentType: string;
    leaveType: string;
    startDate: string;
    endDate: string;
    workingHours: string;
    totalDays: string;
    description: string;
  }) {
    await this.mailerService.sendMail({
      to: data.hrEmail,
      subject: `Pengajuan Cuti Dibuat: ${data.employeeName} (${data.leaveType})`,
      template: './leave-request-to-hr',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        leave_type: data.leaveType,
        start_date: data.startDate,
        end_date: data.endDate,
        working_hours: data.workingHours,
        total_leave_days: data.totalDays,
        leave_description: data.description,
      },
    });
  }

  /**
   * 6. Kirim Notifikasi Permintaan Persetujuan Klaim ke Approver
   */
  async sendClaimRequestToApproverEmail(data: {
    approverEmail: string;
    approverName: string;
    employeeName: string;
    position: string;
    employmentType: string;
    claimType: string;
    transactionDate: string;
    claimDate: string;
    totalAmount: string;
    description: string;
    claimId: string | number;
  }) {
    await this.mailerService.sendMail({
      to: data.approverEmail,
      subject: `Pengajuan Klaim Membutuhkan Persetujuan: ${data.employeeName} (${data.claimType})`,
      template: './claim-request-to-approver',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        approver_name: data.approverName,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        claim_type: data.claimType,
        transaction_date: data.transactionDate,
        claim_date: data.claimDate,
        total_claim_amount: data.totalAmount,
        claim_description: data.description,
        approve_claim_url: `${this.appUrl}/claims/approvals/${data.claimId}`,
      },
    });
  }

  /**
   * 7. Kirim Notifikasi Pembuatan Pengajuan Klaim ke Tim HR
   */
  async sendClaimNotificationToHrEmail(data: {
    hrEmail: string;
    employeeName: string;
    position: string;
    employmentType: string;
    claimType: string;
    transactionDate: string;
    claimDate: string;
    totalAmount: string;
    description: string;
  }) {
    await this.mailerService.sendMail({
      to: data.hrEmail,
      subject: `Pengajuan Klaim Dibuat: ${data.employeeName} (${data.claimType})`,
      template: './claim-request-to-hr',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        claim_type: data.claimType,
        transaction_date: data.transactionDate,
        claim_date: data.claimDate,
        total_claim_amount: data.totalAmount,
        claim_description: data.description,
      },
    });
  }

  /**
   * 8. Kirim Pembaruan Status Pengajuan (Approve / Reject ke Karyawan / HR)
   */
  async sendSubmissionStatusUpdateEmail(data: {
    recipientEmail: string;
    recipientName: string;
    employeeName: string;
    position: string;
    employmentType: string;
    isApproved: boolean;
    submissionType: string;
    submissionDate: string;
    processedBy: string;
    decisionDate: string;
    approvalNotes: string;
    requestId: string | number;
  }) {
    const isApprove = data.isApproved;
    await this.mailerService.sendMail({
      to: data.recipientEmail,
      subject: `Status Pengajuan ${data.submissionType}: ${isApprove ? 'Disetujui' : 'Ditolak'}`,
      template: './submission-status-update',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        preheader_text: `Pengajuan ${data.submissionType} Anda telah ${isApprove ? 'disetujui' : 'ditolak'}.`,
        banner_title: isApprove ? 'Pengajuan Disetujui' : 'Status Pengajuan Ditolak',
        banner_description: isApprove
          ? 'Kabar baik, pengajuan Anda telah disetujui oleh atasan.'
          : 'Mohon maaf, pengajuan Anda tidak dapat disetujui oleh atasan.',
        recipient_name: data.recipientName,
        intro_message: `Berikut adalah rincian keputusan status untuk formulir pengajuan ${data.submissionType} Anda.`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        status_badge: isApprove ? 'DISETUJUI' : 'DITOLAK',
        status_color: isApprove ? '#2f855a' : '#c53030',
        status_bg: isApprove ? '#f0fdf4' : '#fff5f5',
        status_border: isApprove ? '#bbf7d0' : '#fecaca',
        submission_type: data.submissionType,
        submission_date: data.submissionDate,
        processed_by: data.processedBy,
        decision_date: data.decisionDate,
        approval_notes: data.approvalNotes,
        view_detail_url: `${this.appUrl}/requests/detail/${data.requestId}`,
      },
    });
  }

  /**
   * 9. Kirim Notifikasi Slip Gaji Diterbitkan ke Karyawan
   */
  async sendPayslipPublishedEmail(data: {
    employeeEmail: string;
    employeeName: string;
    position: string;
    employmentType: string;
    payrollPeriod: string;
    paymentDate: string;
    bankAccount: string;
    payrollType?: string;
    payrollNotes?: string;
    payslipId: string | number;
  }) {
    await this.mailerService.sendMail({
      to: data.employeeEmail,
      subject: `Slip Gaji Periode ${data.payrollPeriod} Telah Terbit - EzyHRM`,
      template: './payslip-published-to-employee',
      context: {
        ...this.getBrandAssets(),
        job_profile_url: `${this.cdnBase}/jobProfileIcon.png`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        payroll_period: data.payrollPeriod,
        payment_date: data.paymentDate,
        bank_account: data.bankAccount,
        payment_status: 'Berhasil Ditransfer',
        payroll_type: data.payrollType || 'Gaji Reguler Bulanan',
        payroll_notes: data.payrollNotes || 'Dokumen slip gaji resmi terenkripsi demi keamanan data privasi Anda.',
        download_payslip_url: `${this.appUrl}/payroll/payslips/${data.payslipId}`,
      },
    });
  }

  /**
   * 10. Kirim Notifikasi Masa Berakhir Kontrak Kerja (Manager / Approver / HR)
   */
  async sendContractEndNotificationEmail(data: {
    recipientEmail: string;
    recipientName: string;
    employeeName: string;
    position: string;
    employmentType: string;
    scenario: 'NEW' | 'REMINDER' | 'EXPIRED';
    contractStartDate: string;
    contractEndDate: string;
    remainingDaysText: string;
    contractStatus: string;
    department: string;
    contractNotes: string;
    contractId: string | number;
  }) {
    let bannerTitle = 'Pemberitahuan Masa Kontrak';
    let bannerDesc = 'Informasi masa berakhir kontrak kerja PKWT untuk evaluasi perpanjangan.';
    let intro = 'Sistem mencatat bahwa kontrak kerja karyawan di bawah ini akan segera berakhir.';

    if (data.scenario === 'REMINDER') {
      bannerTitle = 'Pengingat Kontrak Kerja';
      bannerDesc = 'Pengingat evaluasi perpanjangan kontrak kerja karyawan yang mendekati jatuh tempo.';
      intro = 'Mohon segera lakukan tindak lanjut atau konfirmasi evaluasi kontrak kerja karyawan berikut.';
    } else if (data.scenario === 'EXPIRED') {
      bannerTitle = 'Kontrak Kerja Berakhir';
      bannerDesc = 'Pemberitahuan bahwa masa perjanjian kerja karyawan telah resmi berakhir.';
      intro = 'Per hari ini masa kontrak kerja karyawan berikut telah berakhir dalam sistem EzyHRM.';
    }

    await this.mailerService.sendMail({
      to: data.recipientEmail,
      subject: `${bannerTitle}: ${data.employeeName} (${data.remainingDaysText})`,
      template: './contract-end-notification',
      context: {
        ...this.getBrandAssets(),
        job_profile_url: `${this.cdnBase}/jobProfileIcon.png`,
        preheader_text: `${bannerTitle} untuk ${data.employeeName}.`,
        banner_title: bannerTitle,
        banner_description: bannerDesc,
        recipient_name: data.recipientName,
        intro_message: intro,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        contract_start_date: data.contractStartDate,
        contract_end_date: data.contractEndDate,
        remaining_days: data.remainingDaysText,
        contract_status: data.contractStatus,
        department: data.department,
        contract_notes: data.contractNotes,
        contract_action_url: `${this.appUrl}/contracts/evaluations/${data.contractId}`,
      },
    });
  }
}
```

---

## 💡 Fitur Bulletproof & Catatan Teknis

1. **Aksen Hijau Kiri Banner (`union1` & `union2`):**
   * Diatur dengan container kolom `width="40"` dan `overflow: hidden;`.
   * Masing-masing icon dibatasi lebar pasti `width: 40px; max-width: 40px;` sehingga **dijamin tidak akan pernah melebar atau meluap (*overflow*)** keluar dari batas aksen hijau pada email client mana pun.
   * `union1.png` menempel di bagian atas (`valign="top"`), dan `union2.png` menempel di bagian bawah (`valign="bottom"`).
2. **Link Bantuan (Help Center):**
   * Menggunakan variabel `support_url` yang langsung membuka web portal Jira Service Desk:  
     `https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133`.
   * **Bukan `mailto:`** atau form email lainnya.
3. **Aset Gambar:**
   * File gambar di folder `assets/` wajib di-upload ke CDN / Cloud Storage (AWS S3, Cloudflare, GCP, dsb).
   * **Hindari format SVG:** Banyak email client (Outlook Desktop, Gmail Mobile App, Yahoo) tidak merender kode `<svg>` atau format `.svg`. Format PNG transparan yang disediakan adalah format standar teraman.
4. **Typography (Font Inter):**  
   Semua template telah menggunakan font **Inter** dengan proteksi MSO conditional fallback (`Arial / Helvetica`) agar Microsoft Outlook Desktop tidak me-*render* font menjadi Times New Roman.
5. **Responsif di Smartphone:**  
   Kolom data pada Card akan otomatis bertumpuk secara vertikal (*stack vertically*) secara halus jika dibuka pada perangkat mobile (lebar layar < 600px).

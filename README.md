# Panduan Integrasi Template Email - EzyHRM
## Enterprise Email Notification Design System

Dokumen ini adalah referensi kontrak data (*data contract*) dan panduan integrasi resmi untuk tim backend (NestJS) dalam memasang template email notifikasi sistem **EzyHRM**.

Seluruh template telah dirancang menggunakan standar baku **Email Client Best Practice** (*table-based layout*, *inline CSS*, font **Inter**, *Outlook VML bulletproof button*, serta *mobile-responsive styling*).

---

## 📁 Struktur File & Aset

Repositori ini menerapkan arsitektur **Master Template Modular**. Cukup dengan **8 file master template**, seluruh **23 skenario email notifikasi** di EzyHRM dapat dijalankan secara konsisten, efisien, dan mudah dipelihara.

```text
├── onboarding-to-employee-email.html   # Template 1: Selamat Datang & Kredensial Akun (ke Karyawan Baru)
├── onboarding-to-hr-email.html         # Template 2: Checklist Onboarding Selesai (ke Tim HR)
├── change-password-to-employee.html    # Template 3: Permintaan Perubahan Kata Sandi (ke Karyawan)
├── request-submission-to-approver.html  # Template 4: Master Pengajuan Membutuhkan Persetujuan (ke Approver / Atasan)
├── request-submission-to-hr.html        # Template 5: Master Notifikasi Pengajuan Baru (ke Tim HR / Pencatatan)
├── submission-status-update.html       # Template 6: Master Pembaruan Status Approve / Reject (ke Karyawan & HR)
├── payslip-published-to-employee.html  # Template 7: Pemberitahuan Terbit Slip Gaji (ke Karyawan)
├── contract-end-notification.html      # Template 8: Master Masa Berakhir Kontrak / Reminder / Expired (Manager, Approver, HR)
├── assets/
│   ├── ezyhrmLogo.png                  # Logo EzyHRM (PNG Transparan High-Res)
│   ├── union1.png                      # Icon Dekoratif Aksen Hijau Atas (Semua Template)
│   ├── union2.png                      # Icon Dekoratif Aksen Hijau Bawah (Semua Template)
│   ├── magicWandIcon.png               # Ilustrasi Tongkat Sihir (untuk onboarding-to-employee)
│   ├── jobProfileIcon.png              # Ilustrasi Profil Pekerjaan (untuk onboarding-to-hr, payslip, contract)
│   ├── laptopLockIcon.png              # Ilustrasi Kunci Laptop (untuk change-password-to-employee)
│   └── formEditionIcon.png             # Ilustrasi Formulir (untuk request submission & status update)
└── README.md                           # Panduan integrasi & kontrak data ini
```

---

## 🗺️ Matriks Pemetaan 23 Email Notification EzyHRM

Gunakan tabel referensi cepat ini untuk mengetahui template mana yang dipanggil oleh backend untuk setiap skenario bisnis:

| No | Modul / Skenario Bisnis | Penerima | Template HTML yang Digunakan | Parameter Kunci / Nilai |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Onboarding Welcome & Credential | Karyawan Baru | `onboarding-to-employee-email.html` | Kredensial login sementara |
| **2** | Onboarding Completion Checklist | Tim HR | `onboarding-to-hr-email.html` | Ringkasan tugas selesai |
| **3** | Password Reset Request | Karyawan | `change-password-to-employee.html` | Token reset kata sandi |
| **4** | Leave - Request Submission | Approver / Atasan | `request-submission-to-approver.html` | `banner_title`: "Permintaan Persetujuan Cuti" |
| **5** | Leave - Request Submission | Tim HR | `request-submission-to-hr.html` | `banner_title`: "Pengajuan Cuti Dibuat" |
| **6** | Claim - Request Submission | Approver / Atasan | `request-submission-to-approver.html` | `banner_title`: "Permintaan Persetujuan Klaim" |
| **7** | Claim - Request Submission | Tim HR & Finance | `request-submission-to-hr.html` | `banner_title`: "Pengajuan Klaim Dibuat" |
| **8** | Overtime - Request Submission | Approver / Atasan | `request-submission-to-approver.html` | `banner_title`: "Permintaan Persetujuan Lembur" |
| **9** | Overtime - Request Submission | Tim HR | `request-submission-to-hr.html` | `banner_title`: "Pengajuan Lembur Dibuat" |
| **10** | Attendance - Request Submission | Approver / Atasan | `request-submission-to-approver.html` | `banner_title`: "Persetujuan Koreksi Kehadiran" |
| **11** | Attendance - Request Submission | Tim HR | `request-submission-to-hr.html` | `banner_title`: "Pengajuan Koreksi Kehadiran Dibuat" |
| **12** | Data Profile - Request Submission | Approver / Atasan | `request-submission-to-approver.html` | `banner_title`: "Persetujuan Pembaruan Profil" |
| **13** | Data Profile - Request Submission | Tim HR | `request-submission-to-hr.html` | `banner_title`: "Permintaan Pembaruan Profil Dibuat" |
| **14** | Status Update: Approved | Karyawan | `submission-status-update.html` | `status_badge`: "DISETUJUI" |
| **15** | Status Update: Approved | Tim HR | `submission-status-update.html` | `status_badge`: "DISETUJUI" |
| **16** | Status Update: Rejected | Karyawan | `submission-status-update.html` | `status_badge`: "DITOLAK" |
| **17** | Status Update: Rejected | Tim HR | `submission-status-update.html` | `status_badge`: "DITOLAK" |
| **18** | Payslip Published Notification | Karyawan | `payslip-published-to-employee.html` | Informasi periode gaji & link unduh |
| **19** | Contract End - New Notification | Manager | `contract-end-notification.html` | `banner_title`: "Pemberitahuan Masa Kontrak" (H-30/60) |
| **20** | Contract End - New Notification | Approver & HR | `contract-end-notification.html` | `banner_title`: "Pemberitahuan Masa Kontrak" |
| **21** | Contract End - Reminder | Approver | `contract-end-notification.html` | `banner_title`: "Pengingat Masa Kontrak Kerja" (H-14/7) |
| **22** | Contract End - Reminder | Tim HR | `contract-end-notification.html` | `banner_title`: "Pengingat Masa Kontrak Kerja" (H-14/7) |
| **23** | Contract End - Expired | Tim HR | `contract-end-notification.html` | `banner_title`: "Kontrak Kerja Berakhir" (Hari H) |

---

## 🎨 Aset Gambar Bersama (Global Brand Assets)

Setiap template email menggunakan aset visual brand EzyHRM yang seragam:

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
> **Tujuan:** Notifikasi penyambutan karyawan baru, memberikan kredensial login sementara, dan tautan aktivasi akun.

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `banner_wand_url` | `string` | **Ya** | `assets/magicWandIcon.png` |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan. Contoh: `Alexander Christian` |
| `employee_email` | `string` | **Ya** | Alamat email login akun. Contoh: `alexander@company.com` |
| `temporary_password` | `string` | **Ya** | Kata sandi sementara dari sistem. Contoh: `Welcome2026!` |
| `login_url` | `string` | **Ya** | URL tombol CTA "Masuk Sekarang". Contoh: `https://ezyhrm.id/login` |

---

## 📋 2. Template: `onboarding-to-hr-email.html`
> **Penerima:** Tim HR (Email HR / PIC Personalia)  
> **Tujuan:** Memberitahukan Tim HR bahwa seorang karyawan telah resmi menyelesaikan seluruh tugas checklist onboarding.

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `job_profile_url` | `string` | **Ya** | `assets/jobProfileIcon.png` |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan yang selesai onboarding. |
| `position` | `string` | **Ya** | Posisi / Jabatan karyawan. Contoh: `Senior Software Engineer` |
| `employment_type` | `string` | **Ya** | Tipe kepegawaian. Contoh: `Full-time (PKWTT)` |

---

## 📋 3. Template: `change-password-to-employee.html`
> **Penerima:** Karyawan (`employee_email`)  
> **Tujuan:** Notifikasi permintaan reset / perubahan kata sandi akun karyawan lengkap dengan panduan keamanan.

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `laptop_lock_url` | `string` | **Ya** | `assets/laptopLockIcon.png` |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan. |
| `reset_password_url` | `string` | **Ya** | URL tombol CTA "Atur Ulang Kata Sandi" (berlaku 60 menit). |

---

## 📋 4. Template: `request-submission-to-approver.html` (Master Request ke Approver)
> **Penerima:** Approver / Manajer / Atasan (`approver_email`)  
> **Tujuan:** Master template untuk **seluruh pengajuan yang membutuhkan persetujuan atasan** (Cuti, Klaim, Lembur, Koreksi Absensi, Perubahan Profil).  
> **Fitur:** Dilengkapi tombol aksi CTA *"Tinjau & Setujui"*.

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `form_edition_url` | `string` | **Ya** | `assets/formEditionIcon.png` |
| `preheader_text` | `string` | **Ya** | Contoh: `Pengajuan cuti baru dari Alexander Christian menunggu persetujuan Anda.` |
| `banner_title` | `string` | **Ya** | Contoh: `Permintaan Persetujuan Cuti` / `Permintaan Persetujuan Klaim` / `Permintaan Persetujuan Lembur` |
| `banner_description` | `string` | **Ya** | Contoh: `Mohon periksa dan setujui pengajuan cuti ini.` |
| `approver_name` | `string` | **Ya** | Nama atasan penerima email. Contoh: `Budi Santoso` |
| `intro_message` | `string` | **Ya** | Contoh: `Sebuah pengajuan cuti tahunan baru telah dikirimkan oleh anggota tim Anda.` |
| `employee_name` | `string` | **Ya** | Nama karyawan pemohon. |
| `position` | `string` | **Ya** | Posisi karyawan pemohon. |
| `employment_type` | `string` | **Ya** | Tipe karyawan pemohon. Contoh: `Full-time (PKWTT)` |
| `field1_label`, `field1_value` | `string` | **Ya** | Kolom 1 Kiri. Contoh: `Jenis Cuti` : `Cuti Tahunan` (atau `Tipe Klaim` : `Rawat Jalan`) |
| `field2_label`, `field2_value` | `string` | **Ya** | Kolom 2 Kiri. Contoh: `Tanggal Mulai` : `20 Okt 2026` (atau `Tanggal Transaksi` : `14 Okt 2026`) |
| `field3_label`, `field3_value` | `string` | **Ya** | Kolom 3 Kiri. Contoh: `Tanggal Selesai` : `22 Okt 2026` (atau `Tanggal Pengajuan` : `16 Okt 2026`) |
| `field4_label`, `field4_value` | `string` | Opsional | Kolom 4 Kiri. Contoh: `Durasi Jam Kerja` : `08:00 - 17:00 (8 Jam)` |
| `field5_label`, `field5_value` | `string` | **Ya** | Kolom 1 Kanan. Contoh: `Total Hari Cuti` : `3 Hari Kerja` (atau `Total Klaim` : `Rp 1.250.000`) |
| `field6_label`, `field6_value` | `string` | **Ya** | Kolom 2 Kanan. Contoh: `Keterangan / Alasan` : `Keperluan keluarga di luar kota` |
| `cta_text` | `string` | **Ya** | Teks tombol CTA. Contoh: `Tinjau & Setujui Cuti` |
| `approve_url` | `string` | **Ya** | URL tombol persetujuan. Contoh: `https://ezyhrm.id/approvals/leaves/123` |

---

## 📋 5. Template: `request-submission-to-hr.html` (Master Request ke HR)
> **Penerima:** Tim HR / Finance / Personalia  
> **Tujuan:** Master template untuk **pemberitahuan informatif ke HR mengenai pengajuan baru** (Cuti, Klaim, Lembur, Koreksi Absensi, Perubahan Profil).  
> **Sifat:** Informatif (*FYI* / pencatatan), tanpa tombol CTA persetujuan.

### Binding Variabel:
Sama persis dengan Template 4 di atas, dengan perbedaan:
* Salam pembuka dibuat statis **`Halo Tim HR,`**.
* Tidak memerlukan parameter `cta_text` dan `approve_url`.

---

## 📋 6. Template: `submission-status-update.html` (Master Status Update)
> **Penerima:** Karyawan (`employee_email`) dan/atau Tim HR (`hr_email`)  
> **Tujuan:** Notifikasi hasil keputusan pengajuan (Disetujui / Ditolak) untuk seluruh modul (Cuti, Klaim, Lembur, Kehadiran, Profil).

### Skenario yang Didukung (4 Email):
1. **Status Disetujui ke Karyawan:** `status_badge: "DISETUJUI"`, `status_color: "#2f855a"`, `status_bg: "#f0fdf4"`, `status_border: "#bbf7d0"`
2. **Status Disetujui ke Tim HR:** `status_badge: "DISETUJUI"`
3. **Status Ditolak ke Karyawan:** `status_badge: "DITOLAK"`, `status_color: "#c53030"`, `status_bg: "#fff5f5"`, `status_border: "#fecaca"`
4. **Status Ditolak ke Tim HR:** `status_badge: "DITOLAK"`

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `form_edition_url` | `string` | **Ya** | `assets/formEditionIcon.png` |
| `preheader_text` | `string` | **Ya** | Teks preview inbox. |
| `banner_title` | `string` | **Ya** | Contoh: `Pengajuan Disetujui` atau `Status Pengajuan Ditolak` |
| `banner_description` | `string` | **Ya** | Contoh: `Pengajuan Anda telah diproses oleh atasan.` |
| `recipient_name` | `string` | **Ya** | Contoh: `Alexander Christian` atau `Tim HR` |
| `intro_message` | `string` | **Ya** | Kalimat pengantar detail status. |
| `employee_name` | `string` | **Ya** | Nama karyawan pemohon. |
| `position` | `string` | **Ya** | Posisi karyawan pemohon. |
| `employment_type` | `string` | **Ya** | Tipe kepegawaian. |
| `status_badge` | `string` | **Ya** | `DISETUJUI` atau `DITOLAK` |
| `status_color` | `string` | Opsional | Warna teks badge (Hijau: `#2f855a`, Merah: `#c53030`). Default: `#2f855a` |
| `status_bg` | `string` | Opsional | Background badge (Hijau: `#f0fdf4`, Merah: `#fff5f5`). Default: `#f0fdf4` |
| `status_border` | `string` | Opsional | Border badge (Hijau: `#bbf7d0`, Merah: `#fecaca`). Default: `#bbf7d0` |
| `submission_type` | `string` | **Ya** | Contoh: `Cuti Tahunan`, `Klaim Rawat Jalan`, `Lembur Proyek` |
| `submission_date` | `string` | **Ya** | Tanggal pengajuan dibuat. Contoh: `15 Okt 2026` |
| `processed_by` | `string` | **Ya** | Nama approver. Contoh: `Budi Santoso (Engineering Lead)` |
| `decision_date` | `string` | **Ya** | Tanggal keputusan. Contoh: `16 Okt 2026` |
| `approval_notes` | `string` | **Ya** | Catatan persetujuan atau alasan penolakan. |
| `view_detail_url` | `string` | **Ya** | URL tombol CTA "Lihat Detail Pengajuan". |

---

## 📋 7. Template: `payslip-published-to-employee.html`
> **Penerima:** Karyawan (`employee_email`)  
> **Tujuan:** Notifikasi bahwa slip gaji resmi telah terbit dan siap diunduh melalui portal EzyHRM.

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `job_profile_url` | `string` | **Ya** | `assets/jobProfileIcon.png` |
| `employee_name` | `string` | **Ya** | Nama lengkap karyawan penerima slip gaji. |
| `position` | `string` | **Ya** | Posisi karyawan. |
| `employment_type` | `string` | **Ya** | Status kepegawaian. |
| `payroll_period` | `string` | **Ya** | Periode bulan & tahun. Contoh: `Oktober 2026` |
| `payment_date` | `string` | **Ya** | Tanggal ditransfer. Contoh: `25 Okt 2026` |
| `bank_account` | `string` | **Ya** | Rekening tujuan. Contoh: `BCA •••• 5678` |
| `payment_status` | `string` | **Ya** | Status transfer. Contoh: `Berhasil Ditransfer` |
| `payroll_type` | `string` | **Ya** | Contoh: `Gaji Reguler Bulanan` atau `THR / Bonus` |
| `payroll_notes` | `string` | **Ya** | Catatan keamanan dokumen slip gaji. |
| `download_payslip_url`| `string` | **Ya** | URL tombol CTA "Lihat & Unduh Slip Gaji". |

---

## 📋 8. Template: `contract-end-notification.html` (Master Kontrak)
> **Penerima:** Manager / Approver / Tim HR  
> **Tujuan:** Master notifikasi peringatan kontrak kerja PKWT (Pemberitahuan Baru H-30/60, Reminder H-14/7, dan Expired pada hari H).

### Binding Variabel:
| Nama Variabel | Tipe Data | Wajib? | Keterangan & Contoh Nilai |
| :--- | :--- | :--- | :--- |
| `logo_url`, `union1_url`, `union2_url`, `support_url`, `year` | Global | **Ya** | Brand assets. |
| `job_profile_url` | `string` | **Ya** | `assets/jobProfileIcon.png` |
| `preheader_text` | `string` | **Ya** | Teks preview inbox. |
| `banner_title` | `string` | **Ya** | Contoh: `Pemberitahuan Masa Kontrak` / `Pengingat Masa Kontrak Kerja` / `Kontrak Kerja Berakhir` |
| `banner_description` | `string` | **Ya** | Deskripsi banner sesuai status evaluasi. |
| `recipient_name` | `string` | **Ya** | Contoh: `Bpk/Ibu [Nama Manager]` / `Tim HR` |
| `intro_message` | `string` | **Ya** | Kalimat pengantar detail. |
| `employee_name` | `string` | **Ya** | Nama karyawan yang bersangkutan. |
| `position` | `string` | **Ya** | Posisi karyawan. |
| `employment_type` | `string` | **Ya** | Contoh: `PKWT (Kontrak)` |
| `contract_start_date`| `string` | **Ya** | Tanggal awal kontrak kerja. Contoh: `01 Nov 2025` |
| `contract_end_date` | `string` | **Ya** | Tanggal akhir kontrak kerja. Contoh: `31 Okt 2026` |
| `remaining_days` | `string` | **Ya** | Sisa hari aktif. Contoh: `30 Hari Lagi`, `7 Hari Lagi`, `Berakhir Hari Ini` |
| `contract_status` | `string` | **Ya** | Contoh: `Perlu Evaluasi Perpanjangan` atau `Expired` |
| `department` | `string` | **Ya** | Departemen/Divisi karyawan. |
| `contract_notes` | `string` | **Ya** | Catatan tambahan HR / PIC. |
| `contract_action_url`| `string` | **Ya** | URL tombol CTA "Tinjau Status Kontrak". |

---

## 🚀 Contoh Implementasi Bersih di NestJS

Berikut contoh implementasi `NotificationService` yang ringkas, bersih, dan menangani seluruh skenario menggunakan modul `@nestjs-modules/mailer`:

```typescript
import { Injectable } from '@nestjs/common';
import { MailerService } from '@nestjs-modules/mailer';

@Injectable()
export class NotificationService {
  constructor(private readonly mailerService: MailerService) {}

  private readonly cdnBase = process.env.CDN_BASE_URL || 'https://cdn.ezyhrm.id/assets';
  private readonly appUrl = process.env.APP_URL || 'https://ezyhrm.id';
  private readonly supportPortalUrl =
    'https://it-rma.atlassian.net/servicedesk/customer/portal/1/group/133';

  /**
   * Helper Brand Assets Global
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
   * 1. Kirim Email Selamat Datang & Kredensial ke Karyawan Baru
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
   * 2. Kirim Notifikasi Onboarding Selesai ke Tim HR
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
   * 3. Kirim Permintaan Reset Kata Sandi ke Karyawan
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
   * 4. Kirim Pengajuan Apapun ke Approver (Cuti, Klaim, Lembur, Kehadiran, Profil)
   */
  async sendRequestToApproverEmail(data: {
    approverEmail: string;
    approverName: string;
    employeeName: string;
    position: string;
    employmentType: string;
    submissionType: string; // 'Cuti', 'Klaim', 'Lembur', dll
    bannerTitle: string;
    bannerDesc: string;
    fields: {
      field1: { label: string; value: string };
      field2: { label: string; value: string };
      field3: { label: string; value: string };
      field4?: { label: string; value: string };
      field5: { label: string; value: string };
      field6: { label: string; value: string };
    };
    ctaText: string;
    approvalUrl: string;
  }) {
    await this.mailerService.sendMail({
      to: data.approverEmail,
      subject: `${data.bannerTitle}: ${data.employeeName}`,
      template: './request-submission-to-approver',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        preheader_text: `Pengajuan ${data.submissionType} baru dari ${data.employeeName} menunggu persetujuan Anda.`,
        banner_title: data.bannerTitle,
        banner_description: data.bannerDesc,
        approver_name: data.approverName,
        intro_message: `Sebuah pengajuan ${data.submissionType} baru telah dikirimkan dan membutuhkan peninjauan Anda.`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        field1_label: data.fields.field1.label,
        field1_value: data.fields.field1.value,
        field2_label: data.fields.field2.label,
        field2_value: data.fields.field2.value,
        field3_label: data.fields.field3.label,
        field3_value: data.fields.field3.value,
        field4_label: data.fields.field4?.label || '',
        field4_value: data.fields.field4?.value || '',
        field5_label: data.fields.field5.label,
        field5_value: data.fields.field5.value,
        field6_label: data.fields.field6.label,
        field6_value: data.fields.field6.value,
        cta_text: data.ctaText,
        approve_url: data.approvalUrl,
      },
    });
  }

  /**
   * 5. Kirim Pemberitahuan Pengajuan Baru ke Tim HR (Informatif / Audit Log)
   */
  async sendRequestNotificationToHrEmail(data: {
    hrEmail: string;
    employeeName: string;
    position: string;
    employmentType: string;
    submissionType: string;
    bannerTitle: string;
    bannerDesc: string;
    fields: {
      field1: { label: string; value: string };
      field2: { label: string; value: string };
      field3: { label: string; value: string };
      field4?: { label: string; value: string };
      field5: { label: string; value: string };
      field6: { label: string; value: string };
    };
  }) {
    await this.mailerService.sendMail({
      to: data.hrEmail,
      subject: `${data.bannerTitle}: ${data.employeeName}`,
      template: './request-submission-to-hr',
      context: {
        ...this.getBrandAssets(),
        form_edition_url: `${this.cdnBase}/formEditionIcon.png`,
        preheader_text: `Pengajuan ${data.submissionType} baru telah dibuat oleh ${data.employeeName}.`,
        banner_title: data.bannerTitle,
        banner_description: data.bannerDesc,
        intro_message: `Pemberitahuan bahwa pengajuan ${data.submissionType} baru telah masuk ke dalam sistem.`,
        employee_name: data.employeeName,
        position: data.position,
        employment_type: data.employmentType,
        field1_label: data.fields.field1.label,
        field1_value: data.fields.field1.value,
        field2_label: data.fields.field2.label,
        field2_value: data.fields.field2.value,
        field3_label: data.fields.field3.label,
        field3_value: data.fields.field3.value,
        field4_label: data.fields.field4?.label || '',
        field4_value: data.fields.field4?.value || '',
        field5_label: data.fields.field5.label,
        field5_value: data.fields.field5.value,
        field6_label: data.fields.field6.label,
        field6_value: data.fields.field6.value,
      },
    });
  }

  /**
   * 6. Kirim Status Update (Approve / Reject ke Karyawan / HR)
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
   * 7. Kirim Notifikasi Slip Gaji Terbit ke Karyawan
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
   * 8. Kirim Notifikasi Masa Berakhir Kontrak (Manager, Approver, HR)
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
      bannerTitle = 'Pengingat Masa Kontrak Kerja';
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

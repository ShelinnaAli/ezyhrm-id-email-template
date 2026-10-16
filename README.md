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
├── assets/
│   ├── ezyhrmLogo.png                  # Logo EzyHRM (PNG Transparan High-Res)
│   ├── union1.png                      # Icon Dekoratif Aksen Hijau Atas (Semua Template)
│   ├── union2.png                      # Icon Dekoratif Aksen Hijau Bawah (Semua Template)
│   ├── magicWandIcon.png               # Ilustrasi Tongkat Sihir (untuk onboarding-to-employee)
│   ├── jobProfileIcon.png              # Ilustrasi Profil Pekerjaan (untuk onboarding-to-hr)
│   ├── laptopLockIcon.png              # Ilustrasi Kunci Laptop (untuk change-password-to-employee)
│   └── formEditionIcon.png             # Ilustrasi Form Cuti (untuk leave-request-to-approver & to-hr)
└── README.md                           # Panduan integrasi & daftar binding data ini
```

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

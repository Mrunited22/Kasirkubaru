# HANDOVER PROYEK: iyonzkasir v2.0

## 1. Ringkasan Produk & Arsitektur
- **Repo aktif:** `Mrunited22/Kasirkubaru` (`main`)
- **Target:** UMKM, warung, gerobakan, hingga Owner multi-cabang/multi-gerobak.
- **Arsitektur:** Offline-First (Room SQLite UUID `IyonzDatabase`) + Auto Cloud Sync (`FirebaseAuth` & `Firestore`).
- **Auth 2 Lapis:**
  1. Owner daftar/login Email + Password di HP (`AuthEntryScreen`), lalu pilih perangkat untuk Owner atau cabang tertentu (`DeviceOutletPickerScreen`).
  2. Jika belum ada karyawan aktif: otomatis masuk. Jika ada karyawan: muncul layar pilih nama + PIN 4–6 digit dengan lockout 30 detik (`StaffPinScreen`).
- **Karyawan 100% Custom Akses (`AppAccess`):** Nama & jabatan bebas ketik, izin diatur lewat checklist halaman & tindakan khusus (termasuk pisah izin lihat HPP/untung bersih).
- **Foto Cloud:** Kompresi Data URI ~20KB (`ImageHelper`) agar gratis di Firebase Spark tanpa ImgBB.

## 2. Aturan Build & Terminal
- Edit lewat GitHub Codespaces terminal di HP; build APK via GitHub Actions (`.github/workflows/android-build.yml`).
- **ATURAN PASTE:** Pecah paste maks ~80–100 baris (`>` lalu `>>`) dan kirim 1 sub-fase per giliran chat agar terminal HP tidak macet.
- Stack: `compileSdk = 36`, `targetSdk = 36`, `minSdk = 24`, AGP `8.9.1`, Gradle `8.14.3`, JDK `17`, Kotlin `2.0.20`, KSP `2.0.20-1.0.25`, CameraX `1.4.2`, ML Kit `17.3.0`.

## 3. Struktur Paket Aktif (`com.iyonzkasir`)
- `MainActivity.kt` (`IyonzApp`, `MainActivity`, `IyonzRoot`, `MainShell`)
- `core/`: `Access.kt`, `Formatters.kt`, `Security.kt`, `SessionManager.kt`, `Theme.kt`
- `data/local/`: `Entities.kt`, `CatalogDaos.kt`, `OrderDaos.kt`, `FinanceDaos.kt`, `IyonzDatabase.kt`
- `data/remote/`: `ImageHelper.kt`, `CloudGateway.kt`, `FirebaseAuthCatalog.kt`, `FirebaseSalesSync.kt`, `SyncCoordinator.kt`
- `data/repo/`: `CatalogRepository.kt`, `FinanceAndCrmRepos.kt`, `OrderRepository.kt`, `PrefRepository.kt`, `StockRepository.kt`, `TeamRepository.kt`
- `di/`: `AppContainer.kt`
- `hardware/`: `AppSound.kt`, `ReceiptFormatter.kt`, `ScannerDialog.kt`, `ThermalPrinter.kt`
- `ui/auth/`: `AuthEntryScreen.kt`, `DeviceOutletPickerScreen.kt`, `StaffPinScreen.kt`
- `ui/home/`: `HomeV2Screen.kt`
- `ui/pos/`: `PosV2State.kt`, `PosV2Screen.kt`, `PosCheckoutScreen.kt`, `OrderSuccessV2Screen.kt`
- `ui/activity/`: `ActivityHubV2Screen.kt`, `KitchenV2Screen.kt`, `OrdersHistoryV2Screen.kt`, `KasbonAndCrmV2Screen.kt`, `WebOrdersV2Screen.kt`
- `ui/manage/`: `ManageHubV2Screen.kt`, `CatalogManageV2Screen.kt`, `CatalogDialogs.kt`, `BundleManageV2Screen.kt`, `ExpenseV2Screen.kt`, `ReportV2Screen.kt`, `ShiftV2Screen.kt`, `TeamManageV2Screen.kt`, `WebStoreV2Screen.kt`, `PrinterAndReceiptV2Screen.kt`, `SettingsAndBackupV2Screen.kt`, `V2BackupHelper.kt`

## 4. Progress Saat Ini
- [x] Langkah 1: CI Workflow + SDK 36 + Manifest + ProGuard
- [x] Langkah 2: `core/`
- [x] Langkah 3: `data/local/`
- [x] Langkah 4A: `data/remote/`
- [x] Langkah 4B: `data/repo/` + `SyncCoordinator.kt`
- [x] Langkah 5: `di/AppContainer.kt`, `ui/auth/*`, `ui/home/HomeV2Screen.kt`
- [x] Langkah 6A: `hardware/*` + `ui/pos/*`
- [x] Langkah 6B: `ui/activity/*`
- [x] Langkah 6C-1: `ui/manage/` bagian 1
- [x] Langkah 6C-2: `ui/manage/` bagian 2 (termasuk `WebStoreV2Screen.kt`)
- [x] Langkah 6D: Sambungkan `MainActivity.kt` & `IyonzApp` ke UI v2 + hapus file v1 lama (Build CI Hijau!)
- [ ] Langkah 7: Update `web/index.html` (Paket Bundling, pajak `pajakPersen`, foto Data URI) + buat `firestore.rules` + setup Firebase Console + tes APK v2

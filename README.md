# Exercise-8 Proyek Semaphore pada STM32 menggunakan FreeRTOS

Proyek ini bertujuan untuk mendemonstrasikan cara mengeliminasi kontensi sumber daya secara selektif menggunakan semaphore pada STM32 dengan FreeRTOS. Semaphore digunakan sebagai mekanisme kontrol akses untuk melindungi bagian kode kritis dari gangguan task lain, menggantikan metode penonaktifan interrupt yang berpotensi mengganggu seluruh sistem.

## Komponen yang Digunakan

- **Mikrokontroler:** STM32F103
- **RTOS:** FreeRTOS
- **Software:** STM32CubeMX, STM32CubeIDE
- **Perangkat tambahan:**
  - LED (merah, biru, dan oranye)
  - Resistor
  - Kabel jumper
  - Breadboard atau PCB

## Fitur Utama

- **Semaphore untuk Mutual Exclusion:** Menggunakan semaphore untuk mengontrol akses ke sumber daya kritis.
- **Manajemen Task Prioritas:** Task dengan prioritas lebih tinggi akan selalu dijalankan sesuai prioritasnya.
- **Konfigurasi Waktu Tunggu Semaphore:** Memungkinkan konfigurasi waktu tunggu task saat mengakses semaphore.

## Pengaturan

### Konfigurasi STM32CubeMX

1. **Konfigurasi FreeRTOS:**
   - Buka bagian *Timers and Semaphores* di menu konfigurasi FreeRTOS.
   - Tambahkan semaphore biner baru dan beri nama `CriticalResourceSemaphore`.

2. **Konfigurasi Semaphore:**
   - `osSemaphoreDef(CriticalResourceSemaphore);`
   - `CriticalResourceSemaphoreHandle = osSemaphoreCreate(osSemaphore(CriticalResourceSemaphore), 1);`

3. **Konfigurasi Task:**
   - Task LED Oranye memiliki prioritas tertinggi.
   - Task LED Biru memiliki prioritas lebih rendah.

### Modifikasi Kode

1. **Ganti `taskENTER_CRITICAL()` dengan:**
   ```c
   osSemaphoreWait(CriticalResourceSemaphoreHandle, WaitTimeMilliseconds);

## Uji Coba
<img src="Ex_8.gif" alt="Uji Coba GIF" style="max-width: 600px; height: auto">

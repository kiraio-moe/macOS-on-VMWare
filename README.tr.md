<div align="center">
    <img src="./images/mac-logo.png" width="30%" />
    <h1>VMWare'a MacOS Kurulumu</h1>
</div>

![macOS Desktop](./images/screenshot-0.png)

## Diller

- [English](READMEmd)
- [Русский](README.ru.md)
- [Türkçe](README.tr.md)

## Ön Gereksinimler

- [VMware Workstation](https://www.techspot.com/downloads/189-vmware-workstation-for-windows.html "TechSpot üzerinden VMware Workstation'ı indirin") uygulamasını indirin ve kurun.
- [VMware Auto Unlocker](https://github.com/paolo-projects/auto-unlocker/releases "GitHub üzerinden VMware Auto Unlocker'ı indirin") aracını indirin ve arşivden çıkarın.
- [macOS ISO kalıplarından](https://data.pyenb.network/macOS/isos/ "Pyenb macOS ISO deposuna göz atın") bir adet ISO dosyası indirin.
  > [ÖNEMLİ]  
  > VMware Auto Unlocker, macOS 14 sürümüne kadar destek sunmaktadır.

## Nasıl Yapılır?

### VMware'i Yamalama (Patching)

- Açık olan tüm VMware Workstation pencerelerini ve işlemlerini kapatın.
- VMware Auto Unlocker içindeki `Unlocker.exe` dosyasını **Yönetici olarak çalıştırın**.
- Unlocker programındaki bir hata nedeniyle ([paolo-projects/auto-unlocker#125](https://github.com/paolo-projects/auto-unlocker/issues/125)) şu adımları izlemeniz gerekir:

  > [DİKKAT]  
  > VMware Workstation'ı daha önce yamaladıysanız, önce unlocker programı içinden mevcut yamayı kaldırın (Uninstall).

  - <https://packages.vmware.com/tools/frozen/darwin/> adresinden hem `darwin.iso` hem de `darwinPre15.iso` dosyalarını indirin ve `tools` adlı bir klasörün içine koyun.
  - Unlocker programında `Download tools` seçeneğinin işaretini kaldırın ve indirdiğiniz dosyaların bulunduğu klasörü seçin.
- VMware Workstation'ı yamalayın!

### macOS Sanal Makinesi (VM) Oluşturma

- VMware Workstation'ı açın.
- Yeni bir sanal makine oluşturun:
  - **Configuration (Yapılandırma):** Custom (Özel)
  - **Hardware Compatibility (Donanım Uyumluluğu):** Varsayılan (Workstation 17.5.x)
  - **Image File (Kalıp Dosyası):** İndirdiğiniz ISO dosyasını seçin
  - **OS (İşletim Sistemi):** Apple Mac OS X
  - **Version (Sürüm):** İndirdiğiniz macOS sürümüne göre seçim yapın
  - **Name & Location (Ad ve Konum):** İstediğiniz adı ve konumu belirleyin. Adını ve dosya yolunu unutmayın!
  - **Processors (İşlemci):** Varsayılan veya daha fazlası (Sisteminize bağlı)
  - **RAM (Bellek):** 2 GB veya daha fazlası (Mümkünse 8GB)
  - **Network (Ağ):** Varsayılan (NAT)
  - **I/O (Giriş/Çıkış Denetleyicisi):** Varsayılan (LSI Logic)
  - **Virtual Disk (Sanal Disk):** Varsayılan (SATA)
  - **Disk:** Create New (Yeni Oluştur). Mümkünse 70 GB veya daha fazlası. Split Virtual Disk (Sanal diski böl). Varsayılan Ad.
  - İşlemi tamamlayın (Finish)! 
- Az önce oluşturduğunuz sanal makinenin konumuna gidin.  
  `{Sanal Makine Adınız}.vmx` dosyasını bir metin düzenleyici (Not Defteri vb.) ile açın:
  - `board-id.reflectHost = "FALSE"` olarak ayarlayın.
  - `ethernet0.virtualDev = "vmxnet3"` olarak ayarlayın.
  - Dosyanın en altına şu satırları ekleyin:
    ```
    board-id = "Mac-AA95B1DDAB278B95"
    hw.model.reflectHost = "FALSE"
    hw.model = "MacBookPro19,1"
    serialNumber.reflectHost = "FALSE"
    serialNumber = "C01234567890"
    ```
  - Eğer **AMD işlemci** kullanıyorsanız aşağıdaki satırları da ekleyin:
    ```
    cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
    cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
    cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
    cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
    cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
    cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
    cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
    cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
    ```
- 💾 Dosyayı kaydedin.

### macOS Kurulumu

- Sanal makinenizi başlatın.
- İlk hazırlık (önyükleme) işlemlerinin tamamlanmasını bekleyin.
- Dilinizi seçin.
- **Disk İzlencesi**'ni (Disk Utility) seçin.
- Sol menüden `VMware Virtual SATA Hard Drive Media` diskini seçin > **Sil**'e (Erase) tıklayın.
- Sürücü adını **Macintosh HD** yapın > Biçimi **APFS** olarak seçin > **Sil**'e tıklayın.
- **Bitti**'ye (Done) tıklayın > Disk İzlencesi'ni kapatın.
- **macOS Yükle** (Install macOS) seçeneğine tıklayın. Kurulum sırasında sanal makine birkaç kez yeniden başlatılacaktır.
- Standart işletim sistemi kurulum adımlarını takip edin. *(Genellikle **Şimdi Değil** veya **Atla** seçeneklerini kullanabilirsiniz)*
- Kurulum tamamlandı! İyi kullanımlar ;)

![macOS Bilgisi](./images/screenshot-1.png)

## Kaynaklar

- [VMware'de macOS 14 Sonoma Sanal Makinesi Çalıştırma](https://i12bretro.github.io/tutorials/0602.html) rehberi için [i12bretro](https://github.com/i12bretro)'ya teşekkürler.

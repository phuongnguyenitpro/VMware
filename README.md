# VMware
VMware
# Cập nhật VMware ESXi 8.0 mới nhất: Broadcom siết chặt URL update, license bắt buộc & hướng dẫn cập nhật offline

## Tác giả: Nguyễn Phương – IT Infra Admin  
**Ngày:** 24/05/2025

---

## Giới thiệu

Broadcom vừa thay đổi chính sách cập nhật hệ thống VMware ESXi bằng cách **bỏ hoàn toàn các URL update cũ** và thay bằng URL mới có **Download Token**, yêu cầu license hợp lệ để có thể update online.

Các link cũ không còn truy cập được:

- https://hostupdate.vmware.com  
- https://depot.vmware.com  
- https://vapp-updates.vmware.com

Thay vào đó, cần sử dụng:

https://dl.broadcom.com/<Download Token>/PROD/COMP/ESX_HOST/main/vmw-depot-index.xml
https://dl.broadcom.com/<Download Token>/PROD/COMP/ESX_HOST/addon-main/vmw-depot-index.xml
https://dl.broadcom.com/<Download Token>/PROD/COMP/ESX_HOST/iovp-main/vmw-depot-index.xml
https://dl.broadcom.com/<Download Token>/PROD/COMP/ESX_HOST/vmtools-main/vmw-depot-index.xml

---

## Các phương án cập nhật ESXi

### 1. Cập nhật CLI Offline (Standalone Host)

- Tải file zip offline từ Broadcom hoặc các nguồn có license.
- Upload file zip lên datastore.
- Thực hiện lệnh:

```bash
esxcli software profile update -d /vmfs/volumes/datastore1/ESXi-8.0U3e-depot.zip -p ESXi-8.0U3e-0-24674464
reboot
2. Cập nhật Offline bằng vCenter Lifecycle Manager
Upload ISO hoặc ZIP image ESXi vào vCenter Lifecycle Manager.

Tạo image base.

Gán image base cho cluster, stage và remediate các host.

Backup là bắt buộc
Trước khi update:

Snapshot VM

Backup cấu hình ESXi

Backup bằng phần mềm chuyên dụng (Veeam, Nakivo,...)

Kinh nghiệm cập nhật ESXi 8.0U3e
Đã cập nhật thành công bản vá CVE mới nhất

Hệ thống ổn định, không gặp lỗi driver hay network

Kết luận
Broadcom đang siết chặt kiểm soát license, làm tăng chi phí và giới hạn khả năng update. Đây là lúc các doanh nghiệp nên cân nhắc chuyển sang các nền tảng ảo hóa khác như:

Proxmox VE

Microsoft Hyper-V

Nutanix AHV

Để tránh phụ thuộc và giảm chi phí lâu dài.

Liên hệ
Email: phuongit.contact@gmail.com
Website: https://phuongnguyenit.com
Facebook: fb.com/jsisen

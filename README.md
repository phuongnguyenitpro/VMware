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

Các phương án cập nhật hệ thống VMware hiện tại
1. ✅ Cập nhật qua CLI – Dành cho hệ thống Standalone
Chuẩn bị:

Tải file .zip từ portal Broadcom hoặc từ bạn bè có license.

Upload lên /vmfs/volumes/datastore1/ hoặc thư mục tạm /tmp.

Lệnh cập nhật:

bash
Copy
Edit
esxcli software profile update -d /vmfs/volumes/datastore1/ESXi-8.0U3e-depot.zip -p ESXi-8.0U3e-0-24674464
reboot
2. ✅ Cập nhật Offline bằng vCenter (vSphere Lifecycle Manager)
Phù hợp cho hệ thống có vCenter nhưng không có license token hoặc muốn chủ động cập nhật nội bộ.

Tải về: File ISO hoặc ZIP của image ESXi/Patch

Thao tác:

Vào vCenter → Lifecycle Manager → Imported ISOs

Upload file ISO/ZIP

Tạo Image Base

Gán image vào cluster → Stage → Remediate

🛡️ ⚠️ ĐỪNG QUÊN: Backup trước khi update!
Backup là bắt buộc trước bất kỳ đợt cập nhật nào. Dưới đây là các gợi ý:

✅ Snapshot toàn bộ VM đang chạy (nếu dung lượng cho phép)

✅ Backup config ESXi host bằng PowerCLI hoặc vim-cmd / esxcli

✅ Với vCenter: export cấu hình bằng VAMI hoặc file OVF

✅ Sao lưu toàn bộ bằng phần mềm chuyên dụng như Veeam, Nakivo, Altaro, Vinchin...

Việc backup không chỉ giúp rollback khi lỗi mà còn đảm bảo an toàn nếu patch mới gây xung đột driver hoặc lỗi I/O.

🔧 Trải nghiệm thực tế: Cập nhật ESXi 8.0U3e vá CVE mới
Tôi vừa cập nhật thành công toàn bộ host lên bản:

ESXi 8.0U3e (Build 24674464)

Vá các lỗ hổng bảo mật nghiêm trọng được công bố tháng 5/2025

Hệ thống hoạt động mượt, không crash driver, không treo iSCSI/NIC

📌 Tổng hợp các phương án
Phương án cập nhật	License Broadcom	Internet	Mức độ dễ	Quản lý tập trung
Online qua token	✅ Cần	✅ Có	⭐⭐⭐⭐	✅ Có
Offline CLI	❌ Không cần	❌ Không	⭐⭐⭐	❌ Không
vCenter Offline	❌ Không cần	❌ Không	⭐⭐⭐⭐	✅ Có

🧭 Lời kết: Đã đến lúc giảm phụ thuộc vào VMware?
Broadcom đang khiến hệ sinh thái VMware trở nên "đắt đỏ" và khó tiếp cận hơn với:

Giá license tăng cao

Tính năng bị giới hạn nếu không có hỗ trợ chính thức

Khó khăn trong cập nhật và bảo trì nếu không có internet/token

💡 Giải pháp dài hạn:

👉 Xem xét chuyển sang nền tảng mã nguồn mở hoặc ít phụ thuộc:

Proxmox VE: Nguồn mở, ổn định, mạnh mẽ, dễ quản lý, cộng đồng lớn

Microsoft Hyper-V / Azure Stack HCI: Cho hệ sinh thái Microsoft, hybrid tốt

Nutanix AHV, XCP-ng, OpenStack: Nếu quy mô lớn

🌱 Nếu bạn là doanh nghiệp SME hoặc tổ chức IT nội bộ muốn linh hoạt và tiết kiệm hơn, Proxmox hoặc Hyper-V là hướng đi phù hợp để giảm rủi ro bị khóa vendor.

📬 Cần tư vấn thiết kế nền tảng ảo hóa mới, backup chuẩn 3-2-1 hoặc nâng cấp ESXi an toàn?

Liên hệ
Email: phuongit.contact@gmail.com
Website: https://phuongnguyenit.com
Facebook: fb.com/jsisen

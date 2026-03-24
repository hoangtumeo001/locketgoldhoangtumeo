#!name = Locket Gold Only
#!desc = Cấu hình tách lẻ mở khóa Locket Gold
#!author = hoangtumeo001

[Header Rewrite]
# Xóa bộ nhớ đệm (cache) của hệ thống thanh toán RevenueCat
^https?://api.revenuecat.com/.+/(receipts$|subscribers/?(.*?)*$) header-del x-revenuecat-etag
^https?://api.revenuecat.com/.+/(receipts$|subscribers/?(.*?)*$) header-del X-RevenueCat-ETag

[Script]
# Kịch bản can thiệp API để mở khóa tính năng Gold
revenuecat = type=http-response,pattern=^https:\/\/api\.revenuecat\.com\/.+\/(receipts$|subscribers\/[^/]+$),requires-body=true,max-size=-1,timeout=60,script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/refs/heads/main/js/Locket_DuyVinh09.js
deleteHeader = type=http-request,pattern=^https:\/\/api\.revenuecat\.com\/.+\/(receipts|subscribers),script-path=https://raw.githubusercontent.com/duyvinh09/Module_IOS/refs/heads/main/js/deleteHeader.js,timeout=60

[MITM]
# Bắt buộc phải có tên miền này để giải mã dữ liệu Locket
hostname = %APPEND%, api.revenuecat.com

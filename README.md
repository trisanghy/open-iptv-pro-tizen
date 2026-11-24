# Open IPTV Pro — Samsung TV WGT

Ứng dụng Tizen Web độc lập cho điều khiển bằng remote. Mã nguồn được giữ ở [nhánh tizen-wgt-installer](https://github.com/trisanghy/open-iptv-pro/tree/tizen-wgt-installer) của repository Open IPTV Pro. Repository này chỉ dành cho các WGT đã ký và đủ điều kiện phát hành.

## Tình trạng

**Chưa có GitHub Release Latest. Không nhập repository này vào TizenBrew Installer để cài đặt cho đến khi có release chứa WGT đã ký và được kiểm thử trên TV.** WGT phiên bản 0.1.52 trong [Actions run 45300343037](https://github.com/trisanghy/open-iptv-pro/actions/runs/45300343037) là bản **UNSIGNED**, dùng để ký; không phải gói cài đặt.

Samsung UA65AU8000KXXV chạy Tizen 6.0: TizenBrew Installer 1.1.3 đọc `GET /repos/trisanghy/open-iptv-pro-tizen/releases/latest` và chọn asset `.wgt` đầu tiên. Trên Tizen 6.0, Installer không tự ký lại WGT. Do đó cần chữ ký Samsung TV hợp lệ, gồm author và distributor certificate có DUID của TV, trước khi tạo release. Không đưa file `.p12`, mật khẩu, access token hoặc private key vào Git, Release hay issue.

## Thành phần ứng dụng

Giao diện remote kế thừa từ nhánh Tizen hiện có; AVPlay qua Samsung Product API, HLS.js, DASH.js, HTML5 và MPEGTS.js được đóng gói trong nguồn. Manifest `tv-samsung` yêu cầu internet, `tv.inputdevice`, `application.launch`; yêu cầu Tizen tối thiểu 3.0. Kiểm tra tĩnh chưa chứng minh phát kênh trên TV thật.

## Phát hành

1. Chủ TV tạo Samsung TV certificate profile với **DUID của UA65AU8000KXXV** và lưu author/distributor certificates ở nơi riêng tư.
2. Ký WGT nguồn bằng Tizen Studio hoặc công cụ ký tương thích; kiểm tra `author-signature.xml`, `signature1.xml`, tính hợp lệ của chữ ký và phiên bản manifest.
3. Thử cài và dùng remote/AVPlay trên TV thật. Tạo release bất biến `v0.1.52` ở **repository này**, đính kèm đúng một WGT đã ký, chọn Latest.
4. Kiểm tra API [Latest release](https://api.github.com/repos/trisanghy/open-iptv-pro-tizen/releases/latest) trả về asset `.wgt` và checksum tương ứng. Sau đó nhập `trisanghy/open-iptv-pro-tizen` trong TizenBrew Installer.

Mỗi bản mới dùng tag mới; không thay thế asset hoặc tag cũ.
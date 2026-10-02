# Mini World: CREATA — Bản lưu map `w30396532858891`

> 🇬🇧 [English](README.md) · [Hướng dẫn đóng góp (tiếng Việt)](CONTRIBUTING.md)

Các file của một map **Mini World: CREATA**, được giữ đúng theo cách game ghi ra.
Repo này chính là thư mục map — nên "cập nhật map" đơn giản là copy thư mục mà game
vừa lưu đè lên rồi push phần thay đổi.

## Thông tin map

| Trường | Giá trị |
| --- | --- |
| Thư mục / ID map | `w30396532858891` (world ID `30396532858891`) |
| Tên map | `Độc tày SangsDayy` |
| Tác giả | SangsDayy (UIN `1049305099`) |
| Game | Mini World: CREATA |
| Phiên bản bản lưu | `1.7.15` |
| Mô tả | `Currently under development` · `Hát [W.I.P]` |
| Ghi chú trong game | Mục "Danh sách lệnh", lưu trong `wglobal.fb` |

## Các lệnh có sẵn trong map

Lấy từ phần ghi chú trong game của chính map.
`<...>` = giá trị bắt buộc · `[...]` = giá trị tùy chọn.

| Lệnh | Ai dùng được |
| --- | --- |
| `/buff <buff_id> <buff_level> [tick_time]` | Mọi người |
| `/clearbuff <buff_id\|all>` | Mọi người |
| `/tpa <player_id>` | Mọi người |
| `/size <giá trị>` | Mọi người |
| `/money view [player_id]` | Mọi người |
| `/kill [player_id]` | Chủ phòng |
| `/fly [player_id]` | Chủ phòng |
| `/give <item_id> <số lượng> [player_id]` | Chủ phòng |
| `/tp <player_id\|pos>` | Chủ phòng |
| `/god [player_id]` | Chủ phòng |
| `/perm <quyền> <player_id\|all> <on\|off>` | Chủ phòng |
| `/perm view <player_id>` | Chủ phòng |
| `/revive <player_id>` | Chủ phòng |
| `/summon <mob_id\|tên> [pos\|player_id]` | Chủ phòng |
| `/tree <tên\|id\|random> [player_id] [giây]` | Chủ phòng |
| `/antivoid` | Chủ phòng |
| `/attr set\|add\|remove <id\|all> <attr> <giá trị>` · `/attr view <id>` | Chủ map |
| `/money <add\|set\|remove> <player_id\|all> <value>` | Chủ map |
| `/skybox` | Chủ map |

`/skybox` được định nghĩa trong script trigger đã mã hoá
`ss/trigger/game_type_1/script_179093296101.lua` nên cú pháp chi tiết không ghi ở đây.

Các bit quyền dùng cho `/perm`:

| Quyền | ID | Quyền | ID |
| --- | --- | --- | --- |
| `move` | 1 | `beattacked` | 64 |
| `place` | 2 | `bekilled` | 128 |
| `operate` | 4 | `pickup` | 256 |
| `destroy` | 8 | `drop` | 512 |
| `use` | 16 | `vehicle` | 1024 |
| `attack` | 32 | `discard` | 2048 |

Bảng thuộc tính cho `/attr`: `1` HP tối đa · `2` HP hiện tại · `3` Hồi phục HP ·
`4` Số mạng · `5` Đói tối đa · `6` Độ đói hiện tại · `7` Oxy tối đa · `8` Oxy hiện tại ·
`9` Hồi Oxy · `10` Tốc độ di chuyển · `11` Tốc độ chạy · `12` Tốc độ ẩn thân ·
`13` Tốc độ bơi · `14` Nhảy · `16` Tỷ lệ Né · `17` Tấn công cận chiến ·
`18` Tấn công tầm xa · `19` Phòng thủ cận chiến · `20` Phòng thủ tầm xa ·
`21` Kích thước mô hình · `22` Điểm · `23` Số lượng sao · `26` EXP hiện tại ·
`27` Cấp độ hiện tại · `28` Thể lực hiện tại · `29` Thể lực tối đa ·
`30` Tỷ lệ hồi Thể lực.

## NPC tuỳ chỉnh

Ba actor NPC nằm trong `mods/mapdefault_0.1_*/behavior/actor/`. Các file JSON này là
text thường nên toàn bộ thông tin dưới đây đọc trực tiếp từ repo.

| Actor ID | File | Tên | Chức năng | HP |
| --- | --- | --- | --- | --- |
| `100000` | `1790917867.json` | Lão Bạch | Người câu cá — phát cần câu khởi đầu, nâng cấp và sửa cần câu | `1200` |
| `100001` | `1790918605.json` | Báo Tuyết | Bán cá lấy tiền | `1200` |
| `100002` | `1790918662.json` | Đường Khả Hinh | Bán vé | `150` |

`mods/allocatedidid.json` cấp cho mỗi NPC một actor ID kèm item ID tương ứng
(item `4098`, `4099`, `4100`).

## Cấu trúc thư mục

| Đường dẫn | Nội dung |
| --- | --- |
| `m0/`, `m1/`, `m2/` | Dữ liệu khối (chunk) bản đồ — region `x<X>z<Z>.r` kèm `a<X>_<Z>.a`. `m1/` và `m2/` đang rỗng (chiều chưa dùng). |
| `sandbox/nodes/` | File nhị phân của sandbox: dữ liệu map, save, config, scene, checksum CRC. |
| `scenetree/scene/` | Mô tả scene `<worldId>_MapDefault.uscene` (dạng ZIP). |
| `ss/` | Hệ thống script — `config.lua`, các script trigger Lua ở `trigger/**`, kho biến `vardata/`. |
| `visualcode/` | Trạng thái editor lập trình khối — `actor.db`, `function.db`, `trigger.db`, `variable.db`, `custommsg.db` và Lua sinh ra ở `workspace/**`. |
| `customui/` | Dự án UI tuỳ chỉnh (`.proj`, trigger, visualcode riêng). |
| `custommodel/`, `custommotion/`, `custompic/` | Asset mô hình / động tác / ảnh tuỳ chỉnh, mỗi mục có `manifest.mf`. |
| `mods/` | Pack hành vi mặc định — 3 khối (`GrassBlock`, `PeachLeaves`, `Sand`), 1 item, các NPC tuỳ chỉnh ở trên, và bảng phân ID `allocatedidid.json`. |
| `modpkg/` | Manifest của các pack đã cài kèm kho biến `ss/` riêng. |
| `blueprint/`, `vbp/` | Blueprint (`.bp`) và mô tả blueprint. |
| `roles/` | File vai trò/quyền của từng người chơi, tên `u<UIN>.p`. |
| `string/` | Bảng chuỗi đa ngôn ngữ. |
| `objlibs/`, `vehicle/`, `tradeCaravanData/` | Thư viện object, dữ liệu xe, dữ liệu thương đội. |
| `wdesc.fb` | Metadata map — tên, tác giả, mô tả, phiên bản. |
| `wglobal.fb` | Dữ liệu toàn map, gồm JSON ghi chú danh sách lệnh. |
| `wsize.fb`, `wterrtype.fb`, `wmultilang.fb` | Kích thước map, loại địa hình, cài đặt đa ngôn ngữ. |
| `cover.data`, `thumb.png_` | Metadata ảnh bìa và thumbnail. |
| `resourceList.data`, `CoustomAvator.json` | Danh sách resource đã mã hoá và avatar tuỳ chỉnh. |
| `triggerarea.fb` | Định nghĩa khu vực trigger / teleport. |
| `UserConfig/`, `transfer/`, `starstationtransfer/` | Thư mục runtime đang rỗng — game sẽ tự tạo lại. |

## Định dạng file

Phần lớn file **không** phải text thường. Game mã hoá hoặc mã hoá cục bộ chúng:

- File `.ex` luôn kèm file mô tả `*_ex_desc_`:
  `{"encrypFlag":"xxtea_64","compressFlag":"none","serializeFlag":"json","version":...}`.
- File `.uscene` là ZIP, nhưng entry `desc.json` bên trong được bảo mật bằng mật khẩu.
- Payload `.lua`, `.db`, `.fb` là base64 bọc ciphertext (tiền tố `v1633` trên file `.db`
  là nhãn định dạng, không phải phần mã hoá).

Đọc được không cần công cụ gì: `mods/**/*.json`, các file `pack_manifest.json`,
phần text thô của `wdesc.fb` / `wglobal.fb`, và các rule trong `.gitignore`.

## Cập nhật map

> [!IMPORTANT]
> Copy thư mục map của game **đè lên** thư mục này, tuyệt đối không xóa rồi mới copy.
> Xóa trước sẽ mất `README.md`, `README.vi.md`, `CONTRIBUTING.md` và `.gitignore`.

1. Chơi/sửa map trong Mini World, rồi **thoát hẳn khỏi map** để game ghi file xong.
2. Tìm thư mục map trên máy (nó trùng tên với repo này).
3. Copy nội dung thư mục đó vào clone trên máy của bạn, giữ lại `.git/`, `README.md`,
   `README.vi.md`, `CONTRIBUTING.md` và `.gitignore`.
4. Chạy `git status` — xem file nào thay đổi.
5. `git add -A && git commit -m "<mô tả thay đổi>"`.
6. `git push`.

File khớp `.gitignore` (thư mục tạm, `*.uinError`, snapshot theo UIN, file log) sẽ
tự động bị bỏ qua — `git status` không nên liệt kê chúng.

Hướng dẫn từng bước đầy đủ, dành cho người chưa từng dùng git, xem trong
[CONTRIBUTING.md](CONTRIBUTING.md).

## Các file đã bị dọn khỏi repo

Những mục sau bị gỡ vì game sẽ tự tạo lại và chỉ làm nhiễu lịch sử.
Vẫn khôi phục được từ các commit cũ.

| Đã gỡ | Lý do |
| --- | --- |
| `modpkgtmp/` | Bản sao chưa đủ của `modpkg/`. |
| `ss/vardata/tmp/`, `modpkg/**/vardata/tmp/` | Cache biến đã cũ, thời gian sớm hơn bản đang dùng. |
| `wdescbackup.fb`, `thumb_temp.fb` | File backup / tạm của map. |
| `visualcode/**/*.uinError`, `visualcode/**/*.db.<uin>` | Dấu marker lỗi rỗng và snapshot theo UIN từ lần load lỗi. |
| `scenetree/scene/<idMapKhác>_MapDefault.uscene` | Mô tả scene thuộc về map khác. |

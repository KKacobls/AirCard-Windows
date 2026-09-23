# AirCard Windows Community Edition 🎴

> **繁體中文說明在前，English documentation below.**  
> 在 Windows 上自訂 Apple Wallet 卡面、使用內建圖層式卡面設計器，以及套用鎖定畫面密碼鍵盤主題。  
> Native Windows client for Apple Wallet card artwork customization and passcode themes.

---

# 中文說明

## 🚀 新手快速開始

如果你只是想直接使用 AirCard，不需要先學 Rust，也不需要自己編譯。

照下面做即可：

1. 安裝 Apple 官方 Windows 版 iTunes / Apple Mobile Device Support。
2. 用 PowerShell 跑完 **3 個 DLL 檢查**，三個都必須是 `True`。
3. USB 連接 iPhone、解鎖並按下「信任」。
4. 從 GitHub Releases 下載 `aircard.exe`。
5. 開啟 AirCard，掃描 Wallet 卡片後即可更換卡面。

---

## 1. 安裝 Apple USB 驅動

AirCard 需要 Apple Mobile Device Support 才能與 iPhone 通訊。

### 最簡單安裝方式

在 Windows：

**開始 → 搜尋 PowerShell → 右鍵 → 以系統管理員身分執行**

貼上這一整行：

```powershell
$p="$env:TEMP\iTunes64Setup.exe"; Invoke-WebRequest "https://www.apple.com/itunes/download/win64" -OutFile $p; Start-Process $p -Verb RunAs -Wait
```

這個指令會：

1. 從 Apple 官方網址下載 Windows 64-bit iTunes 安裝程式。
2. 儲存為 `%TEMP%\iTunes64Setup.exe`。
3. 以系統管理員權限啟動安裝程式。
4. 等待安裝完成。

下載來源：

```text
https://www.apple.com/itunes/download/win64
```

> 建議使用 Apple 官網提供的 Windows 安裝程式，不要只依賴 Microsoft Store 版本。

安裝時保持預設選項即可。  
AirCard 真正需要的是 iTunes 一起安裝的 **Apple Mobile Device Support**。

---

## 2. 安裝完成後，必須跑完這 3 個 PowerShell 檢查

**三個都顯示 `True` 才代表 AirCard 所需的 Apple DLL 已經準備完成。**

### 檢查 1：CoreFoundation.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\CoreFoundation.dll"
```

正常結果：

```text
True
```

### 檢查 2：MobileDevice.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\MobileDevice.dll"
```

正常結果：

```text
True
```

### 檢查 3：AirTrafficHost.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\AirTrafficHost.dll"
```

正常結果：

```text
True
```

### 三個都必須成功

你最後應該確認：

```text
CoreFoundation.dll = True
MobileDevice.dll    = True
AirTrafficHost.dll  = True
```

如果其中任何一個是 `False`，先不要開 AirCard。

重新執行 iTunes 安裝：

```powershell
$p="$env:TEMP\iTunes64Setup.exe"; Invoke-WebRequest "https://www.apple.com/itunes/download/win64" -OutFile $p; Start-Process $p -Verb RunAs -Wait
```

完成後重新啟動 Windows，再跑上面三個檢查。

---

## 3. 連接 iPhone

1. 使用可傳輸資料的 USB-C 或 Lightning 線連接 iPhone。
2. 解鎖 iPhone。
3. 如果 iPhone 顯示「要信任這部電腦嗎？」請按 **信任**。
4. 輸入 iPhone 密碼。
5. 保持 iPhone 解鎖，再啟動 AirCard。

---

## 4. 開啟 AirCard

從 GitHub Releases 下載：

```text
aircard.exe
```

一般使用者不需要安裝 Rust，也不需要執行 `cargo build`。

直接雙擊：

```text
aircard.exe
```

即可使用。

---

# ✨ 主要功能

- Apple Wallet 自訂卡面
- 卡片自動偵測
- Saved Cards
- 內建 Card Designer
- 背景圖片裁切、縮放與拖曳
- 圖片 / Logo 獨立圖層
- 文字圖層
- 矩形、圓角矩形、圓形
- 每個物件都能獨立拖曳
- Layers 圖層管理
- 圖層前後順序調整
- 圖層鎖定 / 隱藏 / 複製 / 刪除
- `.passthm` 鎖定畫面密碼鍵盤主題
- Suica / 交通卡原廠 PDF Restore
- USB / Wi-Fi transport
- Logs
- 多國語言 JSON

---

# 🎨 更換 Apple Wallet 卡面

## 1. 找到卡片

1. USB 連接 iPhone。
2. 保持 iPhone 解鎖。
3. 開啟 AirCard。
4. 進入 **Wallet**。
5. 按下 **Scan**。
6. 在 iPhone 開啟 Apple Wallet。
7. 點選你要修改的卡片。
8. AirCard 會自動取得並保存卡片識別資訊。

---

## 2. 匯入圖片

按：

```text
Choose Image
```

選擇圖片。

支援的圖片格式依程式版本而定，常見格式包含 PNG、JPG、WebP。

---

## 3. 使用 Card Designer

背景圖片可以：

- 拖曳位置
- Zoom 縮放
- 調整 X / Y
- Fit / Reset
- 裁切成 Wallet 卡片比例

Wallet 輸出尺寸：

```text
@3x = 1536 × 969
@2x = 1024 × 646
```

---

## 4. 每一個物件都是獨立 Layer

例如：

```text
Text
Logo
Circle
Image
Background
```

點選哪一層，就只操作那一層。

如果物件重疊、不好在畫布上點選，請直接使用 **Layers** 面板選取。

每個圖層可以：

- 移動
- 縮放
- 旋轉
- 調整透明度
- 隱藏
- 鎖定
- 複製
- 刪除
- Bring Forward
- Send Backward
- Bring to Front
- Send to Back

---

## 5. Logo / 圖片

按：

```text
Add Image / Logo
```

每張圖片都可以獨立設定：

- X / Y
- Width / Height
- Scale
- Rotation
- Opacity
- Rectangle
- Rounded Rectangle
- Circle
- Corner Radius
- 去除純色背景
- 背景色容差
- Outline

---

## 6. 文字

按：

```text
Add Text
```

文字也是獨立圖層，可以：

- 拖曳
- 縮放
- 調整字級
- 粗體
- 顏色
- 透明度
- 旋轉
- 圖層順序

---

## 7. 套用卡面

設計完成後按：

```text
Apply Card Skin
```

等待完成。

接著在 iPhone：

1. 開啟多工畫面。
2. 把 Wallet 往上滑關閉。
3. 重新開啟 Wallet。

---

# ⚠️ Suica / 交通卡

部分交通卡（例如 Suica）可能會使用：

```text
cardBackgroundCombined.pdf
```

如果測試卡面後出現黑卡，可使用：

```text
Restore Original PDF
```

恢復原始 PDF 卡面資產。

不要因為卡面顯示異常就直接移除交通卡。

---

# 🔢 Passcode Theme

1. 進入 **Passcode**。
2. 選擇 `.passthm`。
3. 選擇目標 TelephonyUI 版本。
4. 按下 Apply。
5. 鎖定 iPhone 或重新開啟相關畫面查看效果。

如果主題沒有套用，請確認 iPhone 的 **粗體文字（Bold Text）** 是否關閉。

---

# 🌐 多國語言

語言檔位於：

```text
locales/
```

例如：

```text
en.json
zh-TW.json
zh-CN.json
ja.json
ko.json
es.json
pt-BR.json
fr.json
de.json
ru.json
id.json
vi.json
th.json
tr.json
it.json
pl.json
hi.json
ar.json
```

語言系統使用 JSON key。

找不到翻譯時應 fallback 到 English。

如果想協助翻譯，只要修改或新增 JSON 語言檔後提交 Pull Request。

---

# 🛠 從原始碼編譯

這一段只給開發者。

先安裝 Rust：

```text
https://rustup.rs/
```

Clone：

```powershell
git clone https://github.com/KKacobls/AirCard-Windows.git
```

進入資料夾：

```powershell
cd AirCard-Windows
```

執行測試：

```powershell
cargo test
```

編譯 Release：

```powershell
cargo build --release
```

輸出：

```text
target\release\aircard.exe
```

---

# 🧯 iPhone 找不到時

## 重新啟動 Apple Mobile Device Service

以系統管理員身分開啟 PowerShell：

```powershell
Get-Service | Where-Object {$_.DisplayName -like "*Apple Mobile Device*"} | Restart-Service
```

然後：

1. 拔掉 iPhone。
2. 再插回 USB。
3. 解鎖。
4. 確認已按「信任」。
5. 重新啟動 AirCard。

如果仍有問題，再次確認前面的三個 DLL 檢查全部是 `True`。

---

# 👤 Authors / Credits

本專案建立在多個開源專案與研究成果之上。  
請保留原始 LICENSE、版權聲明與第三方授權資訊。

### AirCard-Windows

- **Lumid-Off** — Windows Native Rust Port & Maintainer  
  https://github.com/Lumid-Off/AirCard-Windows

### Original AirCard / iOS research

- **mak5er** — Original app / exploit research  
  https://github.com/mak5er

### AirLift

- **0xjohnnydev / 0xjohnny** — AirTraffic / ATAirlock research  
  https://github.com/0xjohnnydev/airlift

### Card Design Generator

Card Designer functionality is inspired by / derived from the MIT-licensed:

- **Susie Meow** — `card-design-generator`  
  https://github.com/Susie-Meow/card-design-generator

### Community Edition

- **KKacobls** — Community Edition integration, i18n, Card Designer integration, recovery tools and additional Windows UX

> 發布到 GitHub 前，請把 `KKacobls` 改成你的 GitHub 使用者名稱。

---

# 📜 License

AirCard-Windows 使用 **MIT License**。

如果你修改、重新發布或提供編譯版本：

- 保留原始 MIT LICENSE。
- 保留原始著作權與授權聲明。
- 保留使用到的第三方 MIT 授權資訊。
- 建議保留 `THIRD_PARTY_NOTICES.md`。
- 不要把原作者的成果寫成自己從零開發。

---

# English Documentation

## 🚀 Quick Start

You do not need Rust or source-code knowledge to use AirCard.

Follow these steps:

1. Install Apple's Windows iTunes / Apple Mobile Device Support.
2. Run the **three PowerShell DLL checks** below. All three must return `True`.
3. Connect and unlock your iPhone, then tap **Trust**.
4. Download `aircard.exe` from GitHub Releases.
5. Start AirCard and scan the Wallet card you want to customize.

---

## 1. Install Apple USB Support

AirCard requires Apple Mobile Device Support to communicate with the iPhone.

Open:

**Start → PowerShell → Run as administrator**

Paste this single command:

```powershell
$p="$env:TEMP\iTunes64Setup.exe"; Invoke-WebRequest "https://www.apple.com/itunes/download/win64" -OutFile $p; Start-Process $p -Verb RunAs -Wait
```

This command:

1. Downloads the official 64-bit Windows iTunes installer from Apple.
2. Saves it as `%TEMP%\iTunes64Setup.exe`.
3. Starts the installer with administrator privileges.
4. Waits for installation to finish.

Official download redirect:

```text
https://www.apple.com/itunes/download/win64
```

> The Apple website installer is recommended. Do not rely only on the Microsoft Store version.

Keep the default installation options.

AirCard specifically needs **Apple Mobile Device Support**, which is installed with iTunes.

---

## 2. Run all three PowerShell checks

**Do not consider the Apple runtime ready until all three commands return `True`.**

### Check 1 — CoreFoundation.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\CoreFoundation.dll"
```

Expected:

```text
True
```

### Check 2 — MobileDevice.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\MobileDevice.dll"
```

Expected:

```text
True
```

### Check 3 — AirTrafficHost.dll

```powershell
Test-Path "C:\Program Files\Common Files\Apple\Mobile Device Support\AirTrafficHost.dll"
```

Expected:

```text
True
```

You should have:

```text
CoreFoundation.dll = True
MobileDevice.dll    = True
AirTrafficHost.dll  = True
```

If any result is `False`, reinstall iTunes:

```powershell
$p="$env:TEMP\iTunes64Setup.exe"; Invoke-WebRequest "https://www.apple.com/itunes/download/win64" -OutFile $p; Start-Process $p -Verb RunAs -Wait
```

Then restart Windows and run all three checks again.

---

## 3. Connect the iPhone

1. Connect the iPhone using a data-capable USB-C or Lightning cable.
2. Unlock the iPhone.
3. Tap **Trust** if iOS asks whether you trust this computer.
4. Enter the device passcode.
5. Keep the iPhone unlocked while starting AirCard.

---

## 4. Start AirCard

Download:

```text
aircard.exe
```

from GitHub Releases.

Normal users do not need Rust and do not need to run `cargo build`.

Simply start:

```text
aircard.exe
```

---

# ✨ Features

- Custom Apple Wallet card artwork
- Automatic card detection
- Saved Cards
- Built-in Card Designer
- Background image crop / zoom / drag
- Independent image and logo layers
- Text layers
- Rectangle / Rounded Rectangle / Circle objects
- Independent object movement
- Layers panel
- Layer ordering
- Lock / hide / duplicate / delete layers
- `.passthm` lock-screen passcode themes
- Original PDF restore for Suica / transit cards
- USB / Wi-Fi transport
- Logs
- JSON-based multilingual UI

---

# 🎨 Customize a Wallet Card

## 1. Detect the card

1. Connect the iPhone over USB.
2. Keep it unlocked.
3. Start AirCard.
4. Open the **Wallet** tab.
5. Click **Scan**.
6. Open Apple Wallet on the iPhone.
7. Select the card you want to customize.
8. AirCard detects and stores the card identifier.

---

## 2. Choose artwork

Click:

```text
Choose Image
```

and select your image.

Supported formats depend on the build and commonly include PNG, JPG and WebP.

---

## 3. Use Card Designer

The background image can be:

- Dragged
- Zoomed
- Positioned using X / Y
- Fit or reset
- Cropped to the Wallet card ratio

Wallet output sizes:

```text
@3x = 1536 × 969
@2x = 1024 × 646
```

---

## 4. Every object is its own layer

Example:

```text
Text
Logo
Circle
Image
Background
```

Only the currently selected layer is edited.

If overlapping objects are difficult to select on the canvas, select the exact object from the **Layers** panel.

Each layer can be:

- Moved
- Scaled
- Rotated
- Given opacity
- Hidden
- Locked
- Duplicated
- Deleted
- Brought forward
- Sent backward
- Brought to front
- Sent to back

---

## 5. Images / Logos

Click:

```text
Add Image / Logo
```

Each image can have independent:

- X / Y
- Width / Height
- Scale
- Rotation
- Opacity
- Rectangle mask
- Rounded Rectangle mask
- Circle mask
- Corner radius
- Flat-color background removal
- Tolerance
- Outline

---

## 6. Text

Click:

```text
Add Text
```

Text is also an independent layer.

It can be:

- Dragged
- Scaled
- Resized
- Bold
- Recolored
- Rotated
- Given opacity
- Reordered

---

## 7. Apply the card skin

When the design is ready, click:

```text
Apply Card Skin
```

After completion:

1. Open the iPhone App Switcher.
2. Force-close Wallet.
3. Reopen Wallet.

---

# ⚠️ Suica / Transit Cards

Some transit cards, including Suica, may use:

```text
cardBackgroundCombined.pdf
```

If experimentation causes a black card face, use:

```text
Restore Original PDF
```

to restore the original PDF artwork.

Do not remove a transit card merely because the artwork is temporarily incorrect.

---

# 🔢 Passcode Themes

1. Open the **Passcode** tab.
2. Choose a `.passthm` package.
3. Select the target TelephonyUI version.
4. Apply the theme.
5. Lock the iPhone or reopen the relevant UI.

If the theme does not appear, make sure **Bold Text** is disabled on the iPhone.

---

# 🌐 Languages

Translation files are stored under:

```text
locales/
```

Example files:

```text
en.json
zh-TW.json
zh-CN.json
ja.json
ko.json
es.json
pt-BR.json
fr.json
de.json
ru.json
id.json
vi.json
th.json
tr.json
it.json
pl.json
hi.json
ar.json
```

Translations use JSON keys.

Missing keys should fall back to English.

Translation contributions can be submitted as Pull Requests without changing Rust code.

---

# 🛠 Building from Source

This section is for developers.

Install Rust:

```text
https://rustup.rs/
```

Clone:

```powershell
git clone https://github.com/KKacobls/AirCard-Windows.git
```

Enter the directory:

```powershell
cd AirCard-Windows
```

Run tests:

```powershell
cargo test
```

Build:

```powershell
cargo build --release
```

Output:

```text
target\release\aircard.exe
```

---

# 🧯 iPhone Not Detected

Restart Apple Mobile Device Service from an administrator PowerShell:

```powershell
Get-Service | Where-Object {$_.DisplayName -like "*Apple Mobile Device*"} | Restart-Service
```

Then:

1. Disconnect the iPhone.
2. Reconnect it.
3. Unlock it.
4. Confirm the Trust prompt.
5. Restart AirCard.

If it still fails, run the three DLL checks again and make sure all three return `True`.

---

# 👤 Authors / Credits

This project builds on several open-source projects and research efforts.

Please preserve the original LICENSE, copyright notices and third-party license notices.

### AirCard-Windows

- **Lumid-Off** — Windows Native Rust Port & Maintainer  
  https://github.com/Lumid-Off/AirCard-Windows

### Original AirCard / iOS research

- **mak5er** — Original app / exploit research  
  https://github.com/mak5er

### AirLift

- **0xjohnnydev / 0xjohnny** — AirTraffic / ATAirlock research  
  https://github.com/0xjohnnydev/airlift

### Card Design Generator

Card Designer functionality is inspired by / derived from the MIT-licensed:

- **Susie Meow** — `card-design-generator`  
  https://github.com/Susie-Meow/card-design-generator

### Community Edition

- **KKacobls** — Community Edition integration, i18n, Card Designer integration, recovery tools and additional Windows UX

> Before publishing, replace `KKacobls` with your GitHub username.

---

# 📜 License

AirCard-Windows is licensed under the **MIT License**.

When modifying or redistributing the project:

- Preserve the original MIT LICENSE.
- Preserve original copyright and permission notices.
- Preserve applicable third-party MIT notices.
- Keep `THIRD_PARTY_NOTICES.md`.
- Do not present the upstream authors' work as if it were developed from scratch by the Community Edition maintainer.


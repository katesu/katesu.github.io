---
title: 在 WIN10 安裝 LINUX 雙系統(ubuntu)，以 acer aspire V3-372 為例
category: ubuntu
tags: []
date: 2018-05-02
updated: 2018-06-04
---
第一次在 WIN10 上安裝 LINUX 雙系統(Ubuntu)，記錄了一些個人在安裝過程中遇到的問題，\
使用的電腦是 acer aspire V3-372(BIOS 模式: UEFI)，安裝 Ubuntu 16.04.4 LTS

<!-- more -->

## 製作 Live USB 開機隨身碟
需要準備一個至少 2GB 的空隨身碟\
方法參考至 [Ubuntu 16.04製作Live USB隨身碟的軟體Unetbootin](http://blog.xuite.net/yh96301/blog/57645340-Ubuntu+16.04%E8%A3%BD%E4%BD%9CLive+USB%E9%9A%A8%E8%BA%AB%E7%A2%9F%E7%9A%84%E8%BB%9F%E9%AB%94Unetbootin)

因為 V3 沒有光碟機所以用 Live USB 安裝 Ubuntu，
利用 UNetbootin 這個軟體將 Ubuntu 的 ISO 檔複製至到隨身碟，
然後更改電腦為 USB 開機來安裝作業系統。

### 檔案與工具準備
1 在 [Ubuntu官網](https://www.ubuntu-tw.org/modules/tinyd0/)下載 Ubuntu 16.04.4 LTS ISO 檔案 ⇂
![下載Ubuntu選項](https://i.imgur.com/lEpgsIT.png)

2 在 [unetbootin官網](http://unetbootin.github.io/)下載 UNetbootin ⇂
![unetbootin官網檔案下載位置](https://i.imgur.com/hK1uaoE.png)

3 格式化隨身碟

對隨身碟點右鍵，選擇"格式化" ⇂
![點選格式化](https://i.imgur.com/Hkytbki.png)

格式化選項 ⇂\
![格式化選項](https://i.imgur.com/FGT7q39.png)

4 使用 UNetbootin 複製 Ubuntu ISO 檔案到隨身碟，
	開啟剛才下載的 unetbootin-windows-661.exe
- 發行版: Ubuntu 16.04_Live
- 映像檔路徑: <下載 Ubuntu ISO 的位置>
- 磁碟機: <使用的隨身碟槽名> ⇂

![UNetbootin 選項](https://i.imgur.com/F7SG07C.png)\
點選"確認"後等待執行結束， Live USB 就製作完成了。



## 安裝 Ubuntu
### 安裝前的準備
1 磁碟壓縮\
方法參考至 [輕鬆學會 Windows / Ubuntu 雙系統安裝 (簡易教學)](https://www.youtube.com/watch?v=rjpBTT6AmeU)

- 對 "本機(或我的電腦)" 按右鍵，選擇 "管理"⇂
	![開啟電腦管理](https://i.imgur.com/wd0GcBN.png)
- 在右邊選單中找到 "存放裝置 >> 硬碟管理"\
  對要壓縮空間的磁碟按右鍵按，點選 "壓縮磁碟區"\
  (這張截圖的 D槽原本是 464GB，截圖時我已經壓縮了 200GB安裝 Ubuntu)⇂
![開啟硬碟管理](https://i.imgur.com/CrDbH8o.png)
- 填入要壓縮的空間大小(MB)\
  如果只是使用一般應用程式不玩遊戲的話\
  主要有三個目錄的空間要分配：/(root), /home, swap\
  這些目錄配置沒有一定的規定，依個人需求調整
  - / 通常大約 10~15G
  - swap
    官方建議
    {% blockquote @Ubuntu 正體中文 Wiki https://wiki.ubuntu-tw.org/index.php?title=UbuntuInstallNEW UbuntuInstallNEW %}
    新分割區大小：請輸入您想要建立新分割區的大小，皆以MB為單位（建議如果您的記憶體大於2G，請輸入空白分割區大小-256；記憶體1G~2G，輸入空白分割區大小-512；記憶體512~1G，輸入空白分割區大小-1024）
    {% endblockquote %}
    若會使用休眠的話，要給物理記憶體*2
  - /home\
    功用類似 windows 的 C槽，存放個人資料，大小隨意

  個人的配置是 / 15GB，/swap 11GB，/home 174GB\
  我這臺電腦只用來寫 code、上網和存放資料，所以/home分配比較多空間\
  (現在發現 swap 給太多了，之後要縮小一點...)\
  截圖壓縮了 200GB⇂
  ![壓縮硬碟選項](https://i.imgur.com/yarHxGG.png)
- 壓縮之後\
  "200GB 未配置"是準備安裝 Ubuntu 的空間，要記下這個位置前後的分割容量，\
  安裝 Ubuntu 時需要前後的分割槽容量確認選到是的預定的分割空間⇂
![硬碟壓縮後](https://i.imgur.com/ajl8JPS.jpg)

2 關閉"快速啟動"

3 調整電腦為 USB 開機\
  插入開機隨身碟，開機後、還沒看到 acer logo 前一直按 F2 進入 BIOS
- 從 "Main" 分頁找到 "F12 Boot Menu"，設定為 "Enable"⇂
	![BIOS Main分頁](https://i.imgur.com/DTBTaYh.jpg)
- 切換到 "Security" 分頁，若 "Supervisor Password Is: Set" 則跳過此步驟。⇂
	![BIOS Security分頁](https://i.imgur.com/cqHQHcj.jpg)
	1. 移動到 "Set Supervisor Password" 按下 "Enter"，輸入密碼後按 "Enter"，再次輸入密碼按"Enter" 結束密碼設定。
	1. 確認 "Supervisor Password Is: Set"
- 切換到 "Boot" 分頁
	1. 找到 "Secure Boot" 改變為 "disable"，
	1. 將 "USD HDD:" 移動到第一順位，按 "F10" 選擇 "YES" 儲存設定離開⇂
	![BIOS Secure Boot分頁修改前](https://i.imgur.com/4SYzI02.jpg)
	![BIOS Secure Boot分頁修改後](https://i.imgur.com/3hsTQiP.jpg)
	![F10儲存設定離開BIOS](https://i.imgur.com/MjlAVwx.jpg)

離開後會自動重開機，還沒看到 acer logo 前一直按 F12 就會出現開機選單。⇂
![開機選單](https://i.imgur.com/EuERRh5.jpg)
電腦有讀到開機隨身碟的話會有一個 USB HDD 開頭的選項，
選擇 "USB HDD" 按下 "Enter"。
因為我的開機隨身碟壞了，無法拍到有 USB HDD 的選項照片。

### 安裝過程
1 USB 開機後會出現安裝選單，選擇 "install ubuntu"

2 語言選擇 >> 繼續

3 準備安裝 Ubuntu
- √ 安裝 Ubuntu 同時下載更新
- √ 為圖像及 Wi-Fi硬體、Flash、MP3與其他媒體安裝第三方軟體\
\>\> "繼續"

4 安裝類型
- √ 其他

**目錄空間分配**\
確認"可用空間"前後的空間與前面記下來的相同，選擇"可用空間"，點選左下的 " + "，出現建立分割區的選項。\
建議依序 / >> swap >> /home 分割
- / (root)
  - 大小： 依個人安排
  - 新分割區的類型： 主分割區
  - 新分割區的位置： 此空間的開頭
  - 用途： Ext4 日誌式檔案系統
  - 掛載點： /
- swap
  - 大小： 依個人安排
  - 新分割區的類型： 主分割區
  - 新分割區的位置： 此空間的開頭
  - 用途： Ext4 日誌式檔案系統
- /home\
  - 大小： 剩餘的空間
  - 新分割區的類型： 主分割區
  - 新分割區的位置： 此空間的開頭
  - 用途： 換置空間
  - 掛載點： /home

**用來安裝開機程式的裝置**\
只有一個硬碟只能選 /dev/sda。\
\>\> "立刻安裝" \>\> 是否要將變更寫入磁碟中？ \>\> (確認無誤)"繼續"

實體硬碟檔名是 /dev/sd，虛擬硬碟是 /dev/vd\
第一顆磁碟的名稱是 /dev/sda，有第二顆的話會叫做 /dev/sdb\
/dev/sd[a-p][1-128] 這些是實體硬碟的分割槽


5 填寫一些問題

- 您在哪裡？ \>\> 所在地
- 鍵盤排列方式 \>\> "偵測鍵盤配置" \>\> 回答問題 \>\> "繼續"
- 您是誰？ \>\> (建立使用者帳號) \>\> "繼續"

6 等待安裝 \>\> 完成安裝 \>\> 重新開機



## 開機後沒有出現 Grub 選單

安裝完成重開機卻直奔 windows 沒有出現 grub 選單選擇作業系統？

開啟 cmd 輸入以下指令，替換引導文件
`bcdedit /set {bootmgr} path \EFI\Microsoft\Boot\bootmgfw.efi`





## References
1. [UEFI主機板關閉Secure Boot](http://blog.xuite.net/yh96301/blog/317040181-UEFI%E4%B8%BB%E6%A9%9F%E6%9D%BF%E9%97%9C%E9%96%89Secure+Boot) @軟體使用教學
1. [如何進入BIOS及開啟F12開機選單？](https://tw.answers.acer.com/app/answers/detail/a_id/26992/~/%E5%A6%82%E4%BD%95%E9%80%B2%E5%85%A5bios%E5%8F%8A%E9%96%8B%E5%95%9Ff12%E9%96%8B%E6%A9%9F%E9%81%B8%E5%96%AE%EF%BC%9F) @acer/ANSWERS
1. [Linux分區技巧](http://blog.shiami.info/peterliu/24-linux%E5%88%86%E5%8D%80%E6%8A%80%E5%B7%A7/) @Ubuntu筆記
1. [第七章、Linux 磁碟與檔案系統管理](http://linux.vbird.org/linux_basic/0230filesystem.php) @鳥哥的 Linux 私房菜
1. [Fix Grub Not Showing For Windows 10 Linux Dual Boot](https://itsfoss.com/no-grub-windows-linux/) @It's FOSS
1. [Linux 与 Windows 10 用 GRUB 引导教程](https://blog.itswincer.com/posts/ad42f575/) @Wincer's Blog
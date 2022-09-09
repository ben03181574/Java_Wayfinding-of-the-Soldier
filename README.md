# Java_Wayfinding-of-the-Soldier
Implementing Soldier's Path Visit with BFS, DFS, and UCS Algorithms

## 功能設計（Design of functionality）
藉由讀取資料庫並在地圖上擺放物件，且須能利用滑鼠達到拖動地圖的功能，另外也需要在命令列輸入不同指令的情況下產出結果。
此外，須能利用滑鼠點擊及鍵盤按鍵以選擇達到在地圖上創建不同建築物物件的功能，
創建房屋時需判斷滑鼠點擊位置是否合法能創建房屋，並且利用滑鼠點擊創建多個執行緒，藉此達到可一次蓋不同的房子，
同時，須能利用滑鼠點擊房子來顯示生產 UI，此外需要做到可以讓畫面上多個士兵同時移動且也能進行畫面的拖曳、房子的建造。
最後，需實作 DFS、BFS 以及 UCS，並透過命令列選擇士兵移動所依據的演算法。
而此外移動的路徑要改以 linked list 儲存，如果目的地無法到達則不移動。

## 使用說明（Instructions for use）：
在編譯完成後，可以於 Command Line 上輸入 “java –cp “/home/driver/post-gresql-42.2.23.jar”:./: A1083341_checkpoint3 0 4 2”
後方之數字為欲載入的地圖編號以及地圖縮放程度和演算法編號。
輸入 Enter 後，會顯示地圖以及障礙物圖片。
後方的-cp 為設定其 classpath，告訴系統找不到 package 時，可以尋找的路徑，”./”指主目錄，而在 linux 中冒號為分隔符（windows 則為分號）。
此外使用者可以按鍵以及點擊螢幕以產生不同類型的房屋，如果按下 ‘ b ‘ 則建立 1*1 的軍營，如果按下 ‘ h ’ 則建立 1*1 的普通房子，其他則建立 2*2 的金字塔。


## OOP的考量（The consideration of Object-Oriented Programing）
* A1083341_ checkpoint4_QueryDB：
  * 將障礙物位置資訊以及障礙物的樣式和照片路徑查詢出來後將值存入物件變數以及 ArrayList 和 hashmap。
* A1083341_ checkpoint4_GamePanel：
  * 須利用使窗大小、照片大小計算出需繪製之圖片的起始位置。每個房屋的物件須利用 setLocation()設定該 label 的位置。
* A1083341_ checkpoint4_GameFrame：
  * 建立 panel 物件，已顯示出 panel 內容，同時為了讓使用者可以藉由拖動達成移動地圖之需求，需註冊滑鼠事件，利用滑鼠放開以及點擊計算出移動距離，同時將中心點加上移動距離後即可根據使用者拖動幅度移動地圖。而當使用者完成一次點擊時，需計算出該位置屬於地圖網格中第幾格，確定該位置可以建置房屋後，利用 add 將此房屋的 label 新增至此panel 中。
* A1083341_checkpoint4_Game：
  * 此為主程式，須包含建立資料庫連接、查詢的物件，以便將資料查詢出來給 panel 使用以繪製出地圖，達成題目要求
* A1083341_checkpoint6_House：
  * 此為建築物 house 的類別，玩家點及時會建立此物件並進入其中之 run函式來進行切換建構%數，同時設定滑鼠監聽，當點擊 house label 時，將 spawnMenu 顯示出來。
* A1083341_checkpoint6_Pyramid：
  * 此為建築物 house 的類別，玩家點及時會建立此物件並進入其中之 run函式來進行切換建構%數。
* A1083341_checkpoint6_Barrack：
  * 此為建築物 house 的類別，玩家點及時會建立此物件並進入其中之 run函式來進行切換建構%數。
* A1083341_checkpoint6_SpawnMenu：
  * 此類別用以顯示建構士兵之按鈕，同時設定監聽相關按鈕點擊事件，當點擊按鈕時，新增出 Solider 物件並將其新增 Thread 中同時運行此Thread。
* A1083341_checkpoint6_Soldier_Movement：
  * Solider 類別的 interface 用以確保有時做出 startMove()、detectRoute()兩個 method。
* A1083341_checkpoint6_Soldier：
  * 此類別設有目前位置以及目標位置還有目前是否有被選取的布林值，當此條 Solider 的 Thread 被通知可以運行時，可以利用其中的detectRoute，使用目前位置以及目標位置進行計算達到目的地之路徑，再利用 startMove()確保下一步不會有障礙物後進行移動並重畫。
* A1083341_checkpoint6_Block：
  * 此類別存有目前之位置以及此位置之類型以及花費。設有獲取以及設定以上料之方法。
* A1083341_checkpoint6_BlockPriorityQueue：
此類別為為了實作 UCS 之演算法。
* A1083341_checkpoint6_BlockQueue：
  * 此類別為為了實作出 BFS 之演算法。
* A1083341_checkpoint6_BlockStack：
  * 此類別為為了實作出 DFS 之演算法。
* A1083341_checkpoint6_Fringe：
  * 以上三種類別皆實作此介面，設有新增、刪除、判斷是否為空之方法。
* A1083341_checkpoint6_Node：
  * 此類別存有目前之位置以及下一個 Node 的物件。設有獲取以及設定以上料之方法
* A1083341_checkpoint6_RouteFinder：
  * 此類別為為了找出路經。其設有搜尋、拓展方法，以上兩種方法為為了實作出個演算法所需之操作。而 createRoute 方法則是將搜尋到之路徑以鏈結串列形式回傳。
* A1083341_checkpoint6_RouteLinkedList：
  *此類別為讓士兵能根據此鏈結串列來得知移動步驟，設有新增、刪除、插入、回傳長度、以及設定及獲取 head 的方法。

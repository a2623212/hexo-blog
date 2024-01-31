---
title: 【Web】從輸入網址列到畫面出現，經歷了哪些過程？
tag:
  - MentoCamp
  - FrontEnd
---

遠古以前你會聽到這句話：「輸入 triple W 點 OOO 點 com，就可以了解的更多！」現在的小孩子可能會問什麼是「triple W」？不是直接在網址列輸入 OOO 就好了嗎？

天真！你一定沒有要當工程師，這題可是經典的前端工程師面試題呢，所以今天藉此來練習一下在沒有圖示的情況下，可不可以把這個問題說清楚。

最簡單的說法就是使用者發出了一個 request，然後最後從伺服器收到一個 response，不過這過程可是很複雜的，就拿我的部落格網址「https://blog.chih-yuu.me/blog 」來步步拆解吧！

## 域名解析 (DNS Lookup)？

### 域名 (Domain Name)是什麼？

網址又叫做 URL(Uniform Resource Locator)，一個網址包含通訊協定、域名還有路徑，以我的部落格而言：

- 【https】是通訊協定
- 【blog.chih-yuu.me】是域名
- 【blog】是路徑

### 域名如何轉成 IP?

瀏覽器是讀不懂域名的，所以他必須找出伺服器的 IP 位址，才可以進行通訊，瀏覽器會通過作業系統訪問 DNS(domain name system)找出域名【blog.chih-yuu.me】的 IP 地址，這個過程就叫做域名解析。

## 建立 TCP/IP 連線

### 什麼是 TCP？

知道伺服器的住址(IP)還不夠，你總不能貿然跑去喜歡的人的家跟他要照片嘛（？），你需要遵守交往的步驟，在瀏覽器和伺服器之間也一樣，要遵守 TCP/IP 傳輸協定，它的三次握手(Three-way handshake)，可以確保資料的傳遞與接受是暢通的。

- 第 1 次：客戶端向伺服器端送出 SYN packet
- 第 2 次：伺服器端收到後回覆 SYN/ACK packet
- 第 3 次：客戶端收到後回覆 ACK packet

看到一篇用傳紙條來解釋網路傳輸的文章，很值得參考：
[從傳紙條輕鬆學習基本網路概念](https://hulitw.medium.com/learning-tcp-ip-http-via-sending-letter-5d3299203660)

### TCP 跟 UDP 有什麼差異？

補充 TCP 和 UDP 有什麼不一樣呢？簡單來說，TCP 重視資料的順序與完整傳輸，所以傳資料很可靠，但 UDP 更重視快速，例如現在的串流技術就是 UDP 協定。

## 瀏覽器渲染機制

那我從家裡的電腦輸入「https://blog.chih-yuu.me/blog 」，經過域名解析、建立 TCP 連線之後，為什麼「可以」看到畫面，就要先從瀏覽器從伺服器這裡拿到什麼了？

### Client request

瀏覽器知道了網址的 IP 位置，並建立連線之後，他會向對方發出一個 Http request，Http request 包含 request line、header、body。
request line，也可以翻譯做「請求行」包含 3 個部分：

- 請求方法：GET/POST/PUT/PATCH/DELETE
- 請求對象的路徑
- HTTP 通訊協定的版本
  例如:`GET /hello-world HTTP/1.1`

header，它包含客戶端的資訊，用來告訴伺服器自己是誰，協助伺服器給予相對應的資料。
body，通常在`GET`方法下是空白的，但如果是`POST`，`PUT`或`PATCH`的方法，body 會包含資料格式，還有要新增或是修改的內容，實際上還是要看後端需要什麼資料而定。

### Server response

伺服器端收到要求之後，會根據需求給出一個 response，包含 status line、response header、resources 等三個部分。

status line 很重要，例如大家熟知的 200 = OK、404 = page not fond，可以告訴請求端目前的狀態，如果有錯，問題又在哪裡，可以做初步的判斷。

header，它包含伺服器端的資訊，以我的部落格來說還可以看到我的 server 是架在 Vercel 上面，如果今天的錯誤訊息是 5XX，那可能可以找 Vercel 處理。

接下來的重頭戲就是瀏覽器的渲染啦，也就是針對 resource 的部分，不只有靜態的檔案例如`index.html`，也有其他非文字檔案，如 img 檔。

### 瀏覽器的渲染

瀏覽器是看的懂 HTML 檔案的，瀏覽器在讀完 HTML 之後就會進行 DOM tree 的建構。DOM，全名為 Document Object Model ( 文件物件模型 )。由 Browser 解析 HTML/CSS 檔案，為了讓 JavaScript 操作物件，而建立物件模型 ( object model )。在 DOM 階段可以操作 JS 來增修內容或修改樣式。

這部分完全是前端工程師的五星重點區，重要到必須要特別拉出來再寫一篇。

## 總結

從輸入網址列到畫面出現，經歷了 6 個步驟：

1. 輸入網址
2. 瀏覽器透過作業系統和 DNS 系統進行域名解析
3. 瀏覽器向已知的 IP 位置建立 TCP/IP 通訊
4. 瀏覽器對伺服器發出 request
5. 伺服器收到 request 後，回傳 response
6. 瀏覽器根據 response 的內容進行解析、渲染出網頁畫面。

這是一篇簡單的筆記文章，每一個步驟都有繼續優化的可能性，特別是瀏覽器渲染，完全需要再做筆記。

## 推薦文章

- [What happens when you type a URL into your browser?](https://aws.amazon.com/tw/blogs/mobile/what-happens-when-you-type-a-url-into-your-browser/)
- [Web ブラウザのレンダリングの仕組みを理解する](https://zenn.dev/oreo2990/articles/280d39a45c203e)
- [What happens when you type a URL in your browser and press enter?](https://medium.com/@birnbera/what-happens-when-you-type-a-url-in-your-browser-and-press-enter-f5f4957ba108)
- [【Web】瀏覽器如何繪製網頁？探討 DOM、CSSOM 與渲染](https://medium.someone.tw/web-%E7%80%8F%E8%A6%BD%E5%99%A8%E5%A6%82%E4%BD%95%E7%B9%AA%E8%A3%BD%E7%B6%B2%E9%A0%81-%E6%8E%A2%E8%A8%8E-dom-cssom-%E8%88%87%E6%B8%B2%E6%9F%93-%E7%BF%BB%E8%AD%AF-e9ba8c2be451)

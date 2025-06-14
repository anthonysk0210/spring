# spring
Spring Boot MyWeb應用環境設定總覽

⚙️ 應用啟動設定
Project：Maven
Java Version：17
伺服器埠號：8081
應用程式執行於 localhost:8081，非預設的 8080。
測試用登入帳號/密碼：
Admin： admin@gmail.com / admin
Student： student@gmail.com / student
Anthony： anthony@gmail.com / anthony

🛢️ H2 內嵌式記憶體資料庫
資料庫位置：jdbc:h2:mem:testdb
使用 H2 記憶體資料庫，每次啟動應用都會重建資料。
H2 Console：已啟用 👉 http://localhost:8081/h2-console
登入資訊：
使用者名稱：sa
密碼：空白
驅動類別：org.h2.Driver

🌐 Contact REST API 設定
控制器位置：com.company.MyWeb.rest.ContactRestController
對應路徑前綴：/api/contact ( 僅允許具有 ADMIN 角色的使用者存取 )
例如：👉 /api/contact/getContactMessageByStatus?status=OPEN
支援格式：
application/json
application/xml（若請求包含 Accept: application/xml）

🌐 Spring Data REST 設定
REST API 基底路徑：/spring-data-api ( 僅允許具有 ADMIN 角色的使用者存取 )
所有由 Spring Data 自動產生的 REST 端點將以此為開頭：
例如：👉 /spring-data-api/contacts
HAl Explorer： 視覺化探索 HAL 格式 API 的網頁工具
👉 /spring-data-api

📊 Spring Boot Actuator（系統監控端點）
Actuator 基底路徑：/myWeb/actuator
開放所有端點：management.endpoints.web.exposure.include=*
執行埠號：與應用共用埠號 8081

🖥️ Spring Boot Admin 客戶端
註冊至 Admin Server 的位置：http://localhost:8083 ( 需同步啟動 AdminActuatorApplication 使用 )
身份驗證資訊（用於監控元資料傳遞）：
使用者名稱：admin@gmail.com
密碼：admin

📡 MyWeb 專案中的 REST API 客戶端（ContactRestController）
ContactRestController: 一個 REST API 客戶端控制器，負責向外部 REST 服務發送請求並處理回應資料。
所屬應用名稱：ConsumingRestService
控制器位置：com.company.ConsumingRestService.controller
應用預設埠號：8082
實作途徑： 使用 FeignClient RestTemplate WebClient 實作

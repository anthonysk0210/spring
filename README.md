# spring
**本Web Application以 Spring Boot 為核心開發，模擬一個線上課程教育平台系統。使用者可註冊帳號、選修課程，並依照不同權限角色進行操作。 系統具備學生功能與後台管理功能，實現前後端分離與角色分層控制。**

使用者角色權限總覽：匿名訪客、學生、管理員功能區分與操作權限
【匿名訪客】可：
瀏覽公開頁面：
首頁（Home）
關於我們（About）
最新消息（News）
聯絡我們（Contact）
透過聯絡表單提交留言
註冊成為學生帳號

【學生】登入後可：
進入個人 學生儀錶板（Dashboard），顯示隸屬方案(Plan)
修改／更新個人資料(Profile)
選購課程(Courses)
查看已選購的課程(Courses)

【管理員】登入後可：
進入個人 管理員儀錶板（Dashboard）
修改／更新管理員個人資料(Profile)
查看聯絡表單內容(Contact Message)
進行方案(Plan)管理：新增／刪除方案、設定學生方案
進行課程(Courses)管理：新增／刪除課程、指派／移除學生課程

**Spring Boot 架構整合與功能實作亮點**
✅ Spring Boot MVC 架構： 採用標準的 @Controller、@Service、@Repository 三層架構進行模組分離與職責劃分
✅ Spring Security 安全機制：
實作登入／登出流程與角色授權（ROLE_STUDENT、ROLE_ADMIN）
防範 CSRF 攻擊（預設啟用）
使用 Bcrypt 對使用者密碼加密
自訂登入頁面與導向邏輯，保護敏感路由並實現角色導向的頁面權限控管
✅ Spring Data JPA (Hibernate) 與 Spring JDBC：
使用 @Entity 將 POJO 映射至資料表（ORM）
使用 Spring Data JPA & Spring JDBC 操作 H2 Database
建立資料表之間關聯：
學生(Person @ManyToOne @JoinColumn ) ↔ 角色 (Role)：單向關聯
學生(Person @OneToOne @JoinColumn) ↔ 地址 (Address)：單向關聯
學生(Person @ManyToOne @JoinColumn) ↔ 方案 (Plan @OneToMany )：雙向關聯
學生(Person @ManyToMany @JoinTable) ↔ 課程 (Course @ManyToMany )：雙向關聯
✅ 審計功能（Auditing）： 實作 AuditorAware 自動填入 createdAt、createdBy、updatedAt、updatedBy
✅ 分頁與動態排序功能： 使用 Pageable 實作 contact_msg 表單的分頁與排序，提升查詢效率與使用者體驗
✅ Lombok 工具套件：
使用 @Data 自動產生 Getter、Setter、Constructor 等樣板程式碼
使用 @Slf4j 注入日誌物件，簡化 log 管理
✅ AOP 切面應用： 使用 @Around、@AfterThrowing 實作 LoggerAspect，自動攔截方法執行與例外行為，統一記錄系統日誌
✅ 表單處理與資料驗證：
整合 @Valid 與 BindingResult 實現後端驗證
自訂驗證註解（@interface + ConstraintValidator）驗證 email/password 確認欄位
搭配 Thymeleaf 即時回饋錯誤訊息至前端，提升使用者體驗
✅ Thymeleaf 模板引擎應用：
動態渲染所有頁面內容
使用 th:replace 重複利用共用元件（如 Navbar）
使用 sec:authorize 控制角色導向的內容顯示（如 Dashboard）
支援 Model、ModelAndView、@PathVariable、@RequestParam 傳遞資料
✅ REST API 建構： 客製化 @RestController 與 Spring Data REST 整合，提供管理員對 contact_msg 表單進行 CRUD 操作（兩種路徑並存）
✅ 例外處理機制： 使用 @ControllerAdvice 與 @RestControllerAdvice，分別處理 MVC 與 REST API 模式下的例外情況，提升系統穩定性

**Spring Boot MyWeb應用環境設定總覽**
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

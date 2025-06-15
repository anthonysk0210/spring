# Spring Boot 教育平台系統專案

本專案模擬一個線上課程教育平台系統，使用 Spring Boot 為核心技術，實作使用者註冊、課程選修與分層權限控制。系統包含學生與管理員兩類角色功能，支援前後端分離與安全性驗證，完整展現企業級 Web 開發能力。

## 🧩 使用者角色權限總覽

### 匿名訪客
- 瀏覽首頁(HOME)、關於我們(ABOUT)、最新消息(NEWS)、聯絡我們(CONTACT)
- 提交聯絡表單
- 註冊帳號

### 學生
- 查看個人儀錶板（方案資訊）
- 修改/更新個人資料
- 選購課程、查看已購清單

### 管理員
- 存取管理員儀錶板
- 修改/更新個人資料
- 查看聯絡表單訊息
- 管理方案（新增／刪除／設定學生）
- 管理課程（新增／刪除／指派學生）

## 🔧 技術整合與系統亮點

### Spring 技術架構
- **Spring Boot MVC**：採三層架構 @Controller / @Service / @Repository
- **Spring Security**：登入／授權／登出，CSRF 防護，Bcrypt 密碼加密，自訂登入邏輯與頁面
- **Spring Data JPA & JDBC**：H2 資料庫操作、ORM 映射、多對多／一對一／雙向關聯
- **Spring Data REST**：自動化建構 RESTful API
- **Spring Boot Actuator & Admin**：系統監控與管理

### 核心實作功能
- ✅ 審計功能：AuditorAware 自動寫入 createdAt、createdBy、updatedAt、updatedBy 等欄位
- ✅ 分頁排序：Pageable 實作聯絡表單查詢
- ✅ Lombok：使用 @Data、@Slf4j 精簡樣板程式碼
- ✅ AOP：使用 @Around、@AfterThrowing 實作 LoggerAspect 方法攔截與日誌紀錄
- ✅ 表單驗證：@Valid + BindingResult 與自訂驗證註解
- ✅ Thymeleaf 整合：th:replace 重用元件、sec:authorize 控制頁面內容顯示
- ✅ REST API：手動建構與 Spring Data REST 並行支援
- ✅ 例外處理：@ControllerAdvice / @RestControllerAdvice 例外分離提高穩定性

## 🗃️ 資料庫實體關聯
- Person ↔ Role：@ManyToOne（單向）
- Person ↔ Address：@OneToOne（單向）
- Person ↔ Plan：@ManyToOne ↔ @OneToMany（雙向）
- Person ↔ Course：@ManyToMany ↔ @ManyToMany（雙向）

## ⚙️ 系統啟動設定
- Java：17
- Build：Maven
- 埠號：8081
- 測試帳號：
  - admin@gmail.com / admin
  - student@gmail.com / student
  - anthony@gmail.com / anthony

## 🛢️ H2 資料庫設定
- 位置：`jdbc:h2:mem:testdb`
- H2 Console：`http://localhost:8081/h2-console`
- 登入：使用者 sa／密碼空白／Driver：org.h2.Driver

## 🌐 REST API 路由

### ContactRestController
- 路徑：`/api/contact`
- 僅限 ROLE_ADMIN 存取
- 範例：`/api/contact/getContactMessageByStatus?status=OPEN`
- 支援格式：JSON／XML

### Spring Data REST 自動端點
- 路徑：`/spring-data-api`
- 僅限 ROLE_ADMIN 存取
- 範例：`/spring-data-api/contacts`
- HAL Explorer：`/spring-data-api`

## 📊 Actuator 監控端點
- 基底路徑：`/myWeb/actuator`
- 全部啟用：`management.endpoints.web.exposure.include=*`
- 共用埠號 8081

## 🖥️ 系統監控模組：(AdminActuator)

本模組負責提供監控界面與監控端點整合，需搭配主系統共同啟動。

- 模組名稱：AdminActuator
- 啟動位置：`com.company.AdminActuatorApplication`
- 埠號：8083
- 功能：
  - 顯示應用健康狀態（health）
  - 檢視應用端點（endpoints）
  - 查看環境變數、日誌、記憶體等即時資訊
- 用戶認證資訊（提供給被監控端）：
  - 帳號：admin@gmail.com
  - 密碼：admin

## 📡 REST API 客戶端模組（ConsumingRestService）
- 模組名稱：ConsumingRestService
- 啟動位置：`com.company.ConsumingRestServiceApplication`
- 控制器位置：`com.company.ConsumingRestService.controller`
- 埠號：8082
- 實作：FeignClient、RestTemplate、WebClient

---

本專案展示從認證授權、資料建模、REST API 架構、系統監控到例外處理的完整實作，適合作為 Spring Boot 全端後端開發學習範例。

🔗 GitHub 專案連結：[https://github.com/anthonysk0210/spring.git](https://github.com/anthonysk0210/spring.git)

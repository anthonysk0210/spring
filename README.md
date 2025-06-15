# Spring Boot 教育平台系統專案

本專案模擬一個線上課程教育平台，整合 Spring Boot 生態系統中的多項技術，實作使用者角色分層權限控管、資料操作與安全性驗證，具備完整後端開發與系統整合能力。

## 🧩 使用者角色權限概述

### 匿名訪客
- 瀏覽：首頁、關於我們、最新消息、聯絡我們
- 提交聯絡表單
- 註冊成為學生帳號

### 學生（登入後）
- 學生儀錶板（Dashboard）：查看所屬方案
- 修改／更新個人資料
- 選購課程／查看已購課程

### 管理員（登入後）
- 管理員儀錶板
- 更新個人資料
- 查看聯絡表單內容
- 管理方案與課程（新增／刪除、設定所屬學生）

## 🔧 技術整合亮點

### Spring Framework 模組
- `Spring Boot MVC`：Controller／Service／Repository 分層設計
- `Spring Security`：登入／登出、角色授權、密碼加密、防止 CSRF、頁面導向控管
- `Spring Data JPA & JDBC`：操作 H2 Database，ORM 映射，實作多對多／一對一／雙向關聯
- `Spring Data REST`：建構 RESTful 端點
- `Spring Boot Actuator`：系統監控管理
- `Spring Boot Admin`：整合式監控界面

### 其他功能
- **Lombok**：@Data, @Slf4j 等簡化程式碼
- **AOP**：LoggerAspect 切面實作方法紀錄與錯誤攔截
- **Auditing**：自動填寫 createdAt／updatedAt／createdBy／updatedBy
- **分頁與排序**：使用 Pageable 處理 Contact 表單
- **表單驗證**：使用 @Valid、BindingResult 與自訂驗證註解
- **Thymeleaf**：模板引擎，支援 th:replace、sec:authorize、Model 傳值

## 🌐 REST API 支援
- `/api/contact`：由 `ContactRestController` 客製化建構（限 ADMIN）
- `/spring-data-api`：由 Spring Data REST 自動建構（限 ADMIN）

## 🧪 應用與測試環境
- Java：17
- Build 工具：Maven
- Port：8081
- Database：H2 In-Memory
- H2 Console：`http://localhost:8081/h2-console`
- Admin 帳號：`admin@gmail.com / admin`
- Student 帳號：`student@gmail.com / student`

## 🔄 其他模組
- **Rest API Client 模組（ConsumingRestService）**：8082 埠口實作 FeignClient, RestTemplate, WebClient

## 🔗 GitHub 專案連結
[🔗 https://github.com/anthonysk0210/spring.git](https://github.com/anthonysk0210/spring.git)

---

本專案展示了從登入流程、資料儲存、到角色導向權限控管等完整後端開發技能。適合作為實戰級 Spring Boot 全端系統範例。

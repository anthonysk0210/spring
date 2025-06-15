# Spring Boot 教育平台系統專案

本專案模擬一個線上課程教育平台，整合 Spring Boot 生態系統中的多項技術，實作使用者角色分層權限控管、資料操作與安全性驗證，具備完整後端開發與系統整合能力。

## 🧩 使用者角色權限概述

### 匿名訪客
- 瀏覽公開頁面：首頁、關於我們、最新消息、聯絡我們
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
- `Spring Boot MVC`：三層架構設計（@Controller / @Service / @Repository）
- `Spring Security`：
  - 登入／登出與角色授權
  - CSRF 防護、Bcrypt 密碼加密
  - 自訂登入頁與導向邏輯
- `Spring Data JPA & JDBC`：
  - 操作 H2 Database
  - ORM 實體映射與資料關聯（@OneToOne, @ManyToOne, @ManyToMany）
- `Spring Data REST`：自動生成 REST API
- `Spring Boot Actuator` 與 `Admin`：系統監控與健康檢查

### 其他整合功能
- ✅ 審計功能：`AuditorAware` 自動填入 createdAt / updatedBy 等欄位
- ✅ Lombok：簡化樣板程式碼（@Data, @Slf4j 等）
- ✅ AOP：使用 @Around 與 @AfterThrowing 建立統一日誌切面
- ✅ 表單驗證：
  - @Valid 與 BindingResult 驗證邏輯
  - 自訂驗證註解（如 email、密碼確認）
  - 與 Thymeleaf 整合即時回饋
- ✅ Thymeleaf 模板引擎：
  - th:replace 模組化元件（如 Navbar）
  - sec:authorize 控制內容顯示
  - 支援 Model, ModelAndView, @PathVariable, @RequestParam 等傳值方式
- ✅ 分頁與排序：使用 Pageable 優化聯絡表單查詢效率

## 🌐 REST API 設定

### ContactRestController
- 路徑：`/api/contact`
- 權限：限 ADMIN 存取
- 支援格式：application/json、application/xml

### Spring Data REST
- 路徑前綴：`/spring-data-api`
- 功能：自動生成 CRUD API（限 ADMIN）
- HAl Explorer：`/spring-data-api` 可視化探索介面

## 🧪 系統運行環境

- Java：17  
- Build Tool：Maven  
- Web Port：8081  
- Database：H2（In-Memory）
- H2 Console：`http://localhost:8081/h2-console`  
- 測試帳號：
  - Admin：`admin@gmail.com / admin`
  - Student：`student@gmail.com / student`
  - Anthony：`anthony@gmail.com / anthony`

## 🔁 其他模組（REST 客戶端）

### ConsumingRestService
- 埠號：8082
- 技術：整合 FeignClient、RestTemplate、WebClient
- 控制器位置：`com.company.ConsumingRestService.controller`

## 🔗 GitHub 專案連結

[📁 GitHub Repository](https://github.com/anthonysk0210/spring.git)

---

本專案展示從登入認證、資料操作到角色權限管理的完整實作流程，適合作為 Java / Spring Boot 技術整合與後端開發實戰參考。


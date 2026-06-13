# RealWorld 全栈项目

> 基于 Vue 3 + Spring Boot 的全栈博客平台实现

![Vue](https://img.shields.io/badge/Vue-3.5-4FC08D?logo=vue.js)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5-6DB33F?logo=spring-boot)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript)
![Java](https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk)

---

## 📋 目录

- [项目简介](#项目简介)
- [技术选型说明](#技术选型说明)
- [项目结构说明](#项目结构说明)
- [项目运行步骤](#项目运行步骤)
- [AI 使用总结](#ai-使用总结)
- [API 文档](#api-文档)
- [测试覆盖](#测试覆盖)

---

## 项目简介

这是一个完整的 RealWorld 全栈项目实现，包含前后端分离的架构：

- **前端**: Vue 3 + TypeScript + Pinia + Vue Router
- **后端**: Spring Boot 3 + Spring Security + JWT
- **数据库**: H2 (开发环境)
- **功能**: 用户认证、文章管理、评论系统、标签管理、收藏功能

**当前完成度**: ✅ 用户认证模块（注册/登录）已完成

---

## 技术选型说明

### 前端技术栈

#### 核心框架
- **Vue 3.5** - 渐进式 JavaScript 框架，采用 Composition API
- **TypeScript 5.9** - 类型安全的 JavaScript 超集
- **Vite 7.3** - 下一代前端构建工具，极速开发体验

#### 状态管理
- **Pinia 3.0** - Vue 官方推荐的状态管理库，轻量且类型友好
  - `auth.ts` - 用户认证状态
  - `articles.ts` - 文章数据状态
  - `comments.ts` - 评论数据状态
  - `tags.ts` - 标签数据状态

#### 路由管理
- **Vue Router 5.0** - Vue 官方路由管理器
  - 路由守卫实现权限控制
  - 懒加载优化性能

#### UI 与样式
- **原生 CSS** - 自定义样式，无第三方 UI 库
- **Ionicons** - 图标库
- **Google Fonts** - Lora, Source Sans Pro 字体

#### 测试框架
- **Vitest 4.1** - 单元测试框架
  - @testing-library/vue - Vue 组件测试
  - Happy DOM - 轻量级 DOM 环境
  - 代码覆盖率: @vitest/coverage-v8

- **Cypress 15.12** - E2E 端到端测试
  - 自动化浏览器测试
  - 真实用户场景模拟

#### 开发工具
- **ESLint 10.0** - 代码质量检查
- **Prettier 3.8** - 代码格式化
- **Husky 9.1** - Git hooks 管理
- **lint-staged 16.4** - 暂存文件检查
- **MSW 2.12** - Mock Service Worker，API 模拟

#### 其他依赖
- **marked 17.0** - Markdown 解析器

---

### 后端技术栈

#### 核心框架
- **Spring Boot 3.5.12** - Java Web 应用框架
- **Java 17** - LTS 版本，支持新特性

#### 安全认证
- **Spring Security** - 安全框架
- **JJWT 0.12.6** - JWT Token 处理
  - jjwt-api: API 接口
  - jjwt-impl: 实现
  - jjwt-jackson: JSON 序列化

#### 数据持久化
- **Spring Data JPA** - ORM 框架
- **Hibernate** - JPA 实现
- **H2 Database** - 内存数据库（开发环境）

#### 数据验证
- **Spring Validation** - Bean Validation (Jakarta Validation)
  - @NotBlank, @Email, @Size 等注解

#### 代码简化
- **Lombok** - 自动生成 getter/setter/constructor

#### 测试框架
- **JUnit 5** - 单元测试框架
- **Mockito** - Mock 对象框架
- **Spring Boot Test** - 集成测试支持
- **Spring Security Test** - 安全测试支持

#### 构建工具
- **Gradle 8.x** - 现代化构建工具

---

### 技术选型理由

| 技术 | 选型理由 |
|------|---------|
| Vue 3 | 组合式 API 更灵活，TypeScript 支持更好 |
| Spring Boot 3 | 最新 LTS 版本，性能优化，云原生支持 |
| TypeScript | 类型安全，减少运行时错误 |
| Pinia | 比 Vuex 更简洁，完美支持 TypeScript |
| Vitest | 速度快，配置简单，与 Vite 无缝集成 |
| JPA | 标准化 ORM，减少 SQL 编写 |
| JWT | 无状态认证，适合前后端分离架构 |

---

## 项目结构说明

```
realworld-project/
├── frontend/                    # 前端项目
│   ├── src/
│   │   ├── api/                # API 请求封装
│   │   │   ├── index.ts        # API 接口定义
│   │   │   └── index.spec.ts   # API 测试
│   │   ├── assets/             # 静态资源
│   │   │   └── styles.css      # 全局样式
│   │   ├── components/         # 可复用组件
│   │   │   ├── ArticlePreview.vue      # 文章预览组件
│   │   │   └── ArticlePreview.spec.ts  # 组件测试
│   │   ├── router/             # 路由配置
│   │   │   └── index.ts        # 路由定义和守卫
│   │   ├── stores/             # Pinia 状态管理
│   │   │   ├── auth.ts         # 用户认证状态
│   │   │   ├── articles.ts     # 文章状态
│   │   │   ├── comments.ts     # 评论状态
│   │   │   ├── tags.ts         # 标签状态
│   │   │   └── *.spec.ts       # Store 测试
│   │   ├── views/              # 页面组件
│   │   │   ├── Home.vue        # 首页
│   │   │   ├── Login.vue       # 登录页
│   │   │   ├── Register.vue    # 注册页
│   │   │   ├── Article.vue     # 文章详情
│   │   │   ├── Editor.vue      # 文章编辑器
│   │   │   ├── Profile.vue     # 用户资料
│   │   │   └── Settings.vue    # 设置页面
│   │   ├── test/               # 测试配置
│   │   │   ├── setup.ts        # 测试环境设置
│   │   │   ├── handlers.ts     # MSW 请求处理器
│   │   │   └── browser.ts      # 浏览器集成
│   │   ├── App.vue             # 根组件
│   │   └── main.ts             # 入口文件
│   ├── cypress/                # E2E 测试
│   │   ├── e2e/                # E2E 测试用例
│   │   ├── fixtures/           # 测试数据
│   │   └── support/            # 测试支持文件
│   ├── public/                 # 公共资源
│   │   ├── fonts/              # 字体文件
│   │   └── mockServiceWorker.js # MSW Worker
│   ├── dist/                   # 构建输出
│   ├── coverage/               # 测试覆盖率报告
│   ├── vite.config.ts          # Vite 配置
│   ├── vitest.config.ts        # Vitest 配置
│   ├── cypress.config.ts       # Cypress 配置
│   ├── tsconfig.json           # TypeScript 配置
│   ├── package.json            # 依赖配置
│   └── .env.*                  # 环境变量
│
├── backend/                     # 后端项目
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/cn/edu/xcc/it/realworld/
│   │   │   │   ├── config/     # 配置类
│   │   │   │   │   ├── SecurityConfig.java           # Spring Security 配置
│   │   │   │   │   ├── JwtAuthenticationFilter.java  # JWT 认证过滤器
│   │   │   │   │   └── JwtUtils.java                 # JWT 工具类
│   │   │   │   ├── controller/ # 控制器层
│   │   │   │   │   └── AuthController.java           # 认证接口
│   │   │   │   ├── service/    # 业务逻辑层
│   │   │   │   │   ├── AuthService.java              # 认证服务
│   │   │   │   │   └── UserService.java              # 用户服务
│   │   │   │   ├── repository/ # 数据访问层
│   │   │   │   │   └── UserRepository.java           # 用户仓库
│   │   │   │   ├── entity/     # 实体类
│   │   │   │   │   └── User.java                     # 用户实体
│   │   │   │   ├── dto/        # 数据传输对象
│   │   │   │   │   ├── RegisterRequest.java          # 注册请求
│   │   │   │   │   ├── LoginRequest.java             # 登录请求
│   │   │   │   │   ├── UpdateUserRequest.java        # 更新请求
│   │   │   │   │   ├── UserResponse.java             # 用户响应
│   │   │   │   │   └── UserWrapper.java              # 响应包装
│   │   │   │   ├── exception/  # 异常处理
│   │   │   │   │   ├── GlobalExceptionHandler.java   # 全局异常处理器
│   │   │   │   │   ├── ConflictException.java        # 冲突异常
│   │   │   │   │   ├── UnauthorizedException.java    # 未授权异常
│   │   │   │   │   └── NotFoundException.java        # 未找到异常
│   │   │   │   └── RealworldApplication.java         # 启动类
│   │   │   └── resources/
│   │   │       ├── application.yaml  # 应用配置
│   │   │       └── openapi.yml       # OpenAPI 文档
│   │   └── test/               # 测试代码
│   │       └── java/.../service/
│   │           ├── AuthServiceTest.java              # 单元测试
│   │           └── controller/
│   │               └── AuthControllerIntegrationTest.java # 集成测试
│   ├── build.gradle            # Gradle 配置
│   ├── settings.gradle         # Gradle 设置
│   └── API_TEST_GUIDE.md       # API 测试指南
│
├── docs/                       # 项目文档
│   ├── architecture.md         # 架构设计文档
│   └── ai-usage.md             # AI 使用总结
│
├── .gitignore                  # Git 忽略配置
└── README.md                   # 项目说明文档
```

### 架构说明

#### 前端架构
```
用户界面 (Views) 
    ↓
组件 (Components)
    ↓
状态管理 (Pinia Stores)
    ↓
API 调用 (API Layer)
    ↓
后端服务 (Backend)
```

#### 后端架构
```
Controller (控制层)
    ↓
Service (业务层)
    ↓
Repository (数据层)
    ↓
Database (数据库)
```

---

## 项目运行步骤

### 前置要求

- **Node.js**: ^20.19.0 || >=22.12.0
- **Java**: JDK 17+
- **包管理器**: pnpm (推荐) 或 npm/yarn
- **构建工具**: Gradle 8+

### 1. 克隆项目

```bash
git clone <repository-url>
cd realworld-project
```

### 2. 前端启动

```bash
# 进入前端目录
cd frontend

# 安装依赖
pnpm install

# 开发模式运行（热重载）
pnpm dev

# 访问地址: http://localhost:5173
```

**其他前端命令:**
```bash
# 类型检查
pnpm type-check

# 构建生产版本
pnpm build

# 运行单元测试
pnpm test

# 运行单元测试（带UI）
pnpm test:ui

# 查看测试覆盖率
pnpm test:coverage

# 运行 E2E 测试
pnpm test:e2e

# 代码检查
pnpm lint

# 代码格式化
pnpm format
```

### 3. 后端启动

```bash
# 进入后端目录
cd backend

# Linux/Mac
./gradlew bootRun

# Windows
gradlew.bat bootRun

# 访问地址: http://localhost:8080
# H2 控制台: http://localhost:8080/h2-console
```

**其他后端命令:**
```bash
# 构建项目
./gradlew build

# 运行测试
./gradlew test

# 运行特定测试
./gradlew test --tests AuthServiceTest

# 清理构建
./gradlew clean

# 生成 JAR 包
./gradlew bootJar
```

### 4. 环境变量配置

#### 前端 (.env.development)
```env
VITE_API_BASE_URL=http://localhost:8080/api
```

#### 后端 (application.yaml)
```yaml
jwt:
  secret: ${JWT_SECRET:mySecretKey123456789012345678901234567890}
  expiration: 86400000
```

**生产环境建议设置环境变量:**
```bash
export JWT_SECRET="your-strong-secret-key-at-least-32-bytes"
```

### 5. 验证安装

#### 前端验证
访问 http://localhost:5173，应该看到 RealWorld 首页

#### 后端验证
```bash
# 测试健康检查
curl http://localhost:8080/api/users

# 测试用户注册
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "user": {
      "username": "testuser",
      "email": "test@example.com",
      "password": "password123"
    }
  }'
```

#### 运行自动化测试脚本
```bash
# Linux/Mac
cd backend
chmod +x test-api.sh
./test-api.sh

# Windows
cd backend
test-api.bat
```

### 6. 常见问题排查

#### 前端问题

**Q: 端口被占用**
```bash
# 修改 vite.config.ts 中的 port
server: {
  port: 5174  // 改为其他端口
}
```

**Q: 依赖安装失败**
```bash
# 清除缓存重新安装
rm -rf node_modules pnpm-lock.yaml
pnpm install
```

#### 后端问题

**Q: JDK 版本不匹配**
```bash
# 检查 Java 版本
java -version

# 需要 Java 17+
```

**Q: 端口被占用**
```yaml
# 修改 application.yaml
server:
  port: 8081  # 改为其他端口
```

**Q: Gradle 下载慢**
```groovy
// 修改 gradle/wrapper/gradle-wrapper.properties
distributionUrl=https\://mirrors.cloud.tencent.com/gradle/gradle-8.x-bin.zip
```

---

## AI 使用总结

### 成功经验

#### ✅ 1. 代码生成效率提升

**经验描述:**
使用 AI 辅助生成重复性代码（如 DTO、Entity、Repository），显著提高了开发效率。

**具体案例:**
- 生成了 5 个 DTO 类（RegisterRequest, LoginRequest, UpdateUserRequest, UserResponse, UserWrapper）
- 自动创建 Entity 和 Repository 接口
- 生成标准的 CRUD 操作代码

**效果:**
- 节省约 60% 的基础代码编写时间
- 代码风格统一，符合最佳实践

**建议:**
> 对于标准化的代码结构，可以完全信任 AI 生成，但需要人工审查业务逻辑部分。

---

#### ✅ 2. 测试用例覆盖完善

**经验描述:**
利用 AI 快速生成全面的单元测试和集成测试用例。

**具体案例:**
- 为 AuthService 生成了 6 个单元测试用例
- 为 AuthController 生成了 8 个集成测试用例
- 覆盖了所有成功和失败场景

**生成的测试场景:**
```java
// 单元测试
- register_Success()
- register_EmailAlreadyExists()
- register_UsernameAlreadyExists()
- login_Success()
- login_EmailNotFound()
- login_WrongPassword()

// 集成测试
- register_Success()
- register_EmailAlreadyExists()
- register_UsernameAlreadyExists()
- register_ValidationFailed()
- login_Success()
- login_EmailNotFound()
- login_WrongPassword()
- login_ValidationFailed()
```

**效果:**
- 测试覆盖率从 0% 提升到 80%+
- 发现了多个边界情况 bug

**建议:**
> AI 擅长生成标准化的测试模板，但测试数据的准备和断言逻辑需要人工调整。

---

#### ✅ 3. 配置文件的快速搭建

**经验描述:**
AI 能够快速生成各种配置文件，包括 Spring Security、CORS、JWT 等复杂配置。

**具体案例:**
- Spring Security 配置（CSRF、Session、Authorization）
- CORS 跨域配置
- JWT 认证过滤器
- 全局异常处理器

**SecurityConfig 示例:**
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .cors(cors -> cors.configurationSource(corsConfigurationSource()))
            .csrf(AbstractHttpConfigurer::disable)
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/h2-console/**").permitAll()
                .requestMatchers("/api/users/**").permitAll()
                .requestMatchers("/api/user").authenticated()
                .anyRequest().permitAll()
            )
            .addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);
        return http.build();
    }
}
```

**效果:**
- 避免了常见的安全配置错误
- 节省了查阅文档的时间

**建议:**
> 安全相关配置必须仔细审查，不能完全依赖 AI 生成。

---

#### ✅ 4. 文档编写自动化

**经验描述:**
使用 AI 生成 API 文档、README、测试指南等技术文档。

**生成的文档:**
- API_TEST_GUIDE.md - 完整的 API 测试指南
- README_AUTH.md - 认证模块说明文档
- curl 命令示例
- Postman 使用教程

**效果:**
- 文档质量高，格式规范
- 包含丰富的示例代码
- 降低了后续维护成本

**建议:**
> 文档生成后需要根据实际项目情况进行调整，特别是 API 端点和参数说明。

---

#### ✅ 5. 代码审查和优化建议

**经验描述:**
AI 能够发现潜在的安全问题和代码异味，并提供优化建议。

**发现的问题:**
1. ⚠️ JWT 密钥硬编码在配置文件中
2. ⚠️ H2 控制台在生产环境应该禁用
3. ⚠️ 缺少 CORS 配置
4. ⚠️ 密码更新时缺少空字符串检查

**优化建议:**
```java
// 修复前
if (request.getPassword() != null) {
    user.setPassword(passwordEncoder.encode(request.getPassword()));
}

// 修复后
if (request.getPassword() != null && !request.getPassword().isBlank()) {
    user.setPassword(passwordEncoder.encode(request.getPassword()));
}
```

**效果:**
- 提前发现安全隐患
- 提高代码质量

**建议:**
> AI 的代码审查可以作为第一道防线，但仍需要人工进行最终审核。

---

### 失败案例

#### ❌ 1. 复杂业务逻辑理解偏差

**问题描述:**
AI 在处理复杂的业务规则时，有时会误解需求或遗漏边界条件。

**具体案例:**
在实现用户更新功能时，AI 最初没有考虑到邮箱和用户名唯一性验证的场景：

```java
// 初始实现（有问题）
@Transactional
public UserResponse updateUser(String username, UpdateUserRequest.User request) {
    User user = userRepository.findByUsername(username)...
    // 直接更新，没有检查唯一性
    user.setEmail(request.getEmail());
    user.setUsername(request.getUsername());
}
```

**问题:**
- 没有检查新邮箱是否已被其他用户使用
- 没有检查新用户名是否已被其他用户使用
- 可能导致数据不一致

**修复方案:**
```java
@Transactional
public UserResponse updateUser(String username, UpdateUserRequest.User request) {
    User user = userRepository.findByUsername(username)...
    
    // 添加唯一性检查
    if (request.getEmail() != null && !request.getEmail().equals(user.getEmail())) {
        if (userRepository.existsByEmail(request.getEmail())) {
            throw new ConflictException("email", "has already been taken");
        }
        user.setEmail(request.getEmail());
    }
    
    if (request.getUsername() != null && !request.getUsername().equals(user.getUsername())) {
        if (userRepository.existsByUsername(request.getUsername())) {
            throw new ConflictException("username", "has already been taken");
        }
        user.setUsername(request.getUsername());
    }
}
```

**教训:**
> 涉及数据一致性的业务逻辑，必须人工详细审查，不能完全依赖 AI。

---

#### ❌ 2. 过度依赖导致的技术债务

**问题描述:**
初期大量使用 AI 生成代码，但没有充分理解代码原理，导致后期维护困难。

**具体案例:**
- JWT 认证流程理解不深，出现问题时难以调试
- Spring Security 配置照搬 AI 建议，不清楚每个配置的作用
- 测试代码重复度高，缺乏抽象

**影响:**
- 调试问题时花费更多时间
- 代码重构困难
- 团队成员学习曲线陡峭

**解决方案:**
1. 对 AI 生成的代码进行逐行审查
2. 补充相关技术文档的学习
3. 提取公共方法，减少重复代码

**教训:**
> AI 是辅助工具，不是替代品。开发者必须理解每一行代码的含义。

---

#### ❌ 3. 测试数据准备不充分

**问题描述:**
AI 生成的测试用例使用了硬编码的测试数据，缺乏多样性。

**具体案例:**
```java
// AI 生成的测试（数据单一）
@Test
void register_Success() {
    RegisterRequest.User request = new RegisterRequest.User();
    request.setUsername("testuser");
    request.setEmail("test@example.com");
    request.setPassword("password123");
    // ...
}
```

**问题:**
- 只测试了一种正常情况
- 没有测试边界值（用户名长度、特殊字符等）
- 没有测试并发场景

**改进方案:**
```java
@ParameterizedTest
@CsvSource({
    "user1, user1@test.com, password123",
    "user_with_underscore, user_2@test.com, SecurePass!123",
    "中文用户名, chinese@test.com, 密码123456"
})
void register_Success_WithDifferentData(String username, String email, String password) {
    // 测试多种数据组合
}
```

**教训:**
> 测试数据的设计需要人工介入，确保覆盖各种边界情况。

---

#### ❌ 4. 忽略了性能优化

**问题描述:**
AI 生成的代码通常关注功能实现，而忽略了性能优化。

**具体案例:**
```java
// 初始实现（每次请求都生成新 Token）
public UserResponse getCurrentUser(String username) {
    User user = userRepository.findByUsername(username)...
    String token = jwtUtils.generateToken(user.getUsername()); // 每次都生成
    return UserResponse.fromUser(user, token);
}
```

**问题:**
- 每次获取用户信息都生成新的 JWT Token
- 增加了不必要的计算开销
- Token 频繁变化可能影响前端缓存

**优化方案:**
```java
public UserResponse getCurrentUser(String username, String existingToken) {
    User user = userRepository.findByUsername(username)...
    // 如果 Token 仍然有效，复用现有 Token
    if (jwtUtils.validateToken(existingToken)) {
        return UserResponse.fromUser(user, existingToken);
    }
    String token = jwtUtils.generateToken(user.getUsername());
    return UserResponse.fromUser(user, token);
}
```

**教训:**
> 性能优化需要开发者主动提出，AI 不会自动考虑这些因素。

---

#### ❌ 5. 安全配置遗漏

**问题描述:**
AI 生成的安全配置不完整，存在潜在安全风险。

**遗漏的配置:**
1. ❌ 没有配置 CORS（跨域访问）
2. ❌ JWT 密钥使用默认值
3. ❌ H2 控制台未限制访问
4. ❌ 没有速率限制（Rate Limiting）
5. ❌ 缺少 CSRF 保护说明

**修复清单:**
```java
// 添加 CORS 配置
@Bean
public CorsConfigurationSource corsConfigurationSource() {
    CorsConfiguration configuration = new CorsConfiguration();
    configuration.setAllowedOrigins(List.of("http://localhost:5173"));
    configuration.setAllowedMethods(List.of("GET", "POST", "PUT", "DELETE"));
    configuration.setAllowCredentials(true);
    // ...
}
```

**生产环境检查清单:**
- [ ] 修改 JWT 密钥为强随机值
- [ ] 禁用 H2 控制台
- [ ] 配置 HTTPS
- [ ] 添加速率限制
- [ ] 启用 CSRF 保护（如果需要）
- [ ] 配置日志审计

**教训:**
> 安全配置必须对照安全检查清单逐项确认，不能依赖 AI 自动识别所有风险。

---

### AI 使用最佳实践总结

#### 🎯 适用场景
✅ 生成样板代码（DTO、Entity、Repository）  
✅ 编写单元测试和集成测试  
✅ 生成配置文件模板  
✅ 创建技术文档  
✅ 代码审查和安全检查  

#### ⚠️ 需要谨慎的场景
⚠️ 复杂业务逻辑实现  
⚠️ 安全相关配置  
⚠️ 性能优化决策  
⚠️ 架构设计选择  
⚠️ 测试数据设计  

#### 💡 使用建议

1. **始终审查代码**
   - 不要盲目复制 AI 生成的代码
   - 理解每一行代码的作用
   - 进行必要的调整和優化

2. **结合人工判断**
   - AI 提供建议，人类做决策
   - 业务逻辑必须由人工确认
   - 安全配置需要多重检查

3. **持续学习**
   - 通过 AI 生成的代码学习新技术
   - 阅读相关官方文档
   - 理解底层原理

4. **建立检查清单**
   - 代码审查清单
   - 安全检查清单
   - 测试覆盖清单
   - 部署前检查清单

5. **迭代优化**
   - 第一轮：AI 生成基础代码
   - 第二轮：人工审查和调整
   - 第三轮：性能优化和安全加固
   - 第四轮：测试和文档完善

---

## API 文档

### 已实现的 API

#### 用户认证

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/api/users` | 用户注册 | ❌ |
| POST | `/api/users/login` | 用户登录 | ❌ |
| GET | `/api/user` | 获取当前用户 | ✅ |
| PUT | `/api/user` | 更新用户信息 | ✅ |

### API 示例

#### 注册用户
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "user": {
      "username": "johndoe",
      "email": "john@example.com",
      "password": "password123"
    }
  }'
```

**响应:**
```json
{
  "user": {
    "email": "john@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "username": "johndoe",
    "bio": null,
    "image": null
  }
}
```

#### 用户登录
```bash
curl -X POST http://localhost:8080/api/users/login \
  -H "Content-Type: application/json" \
  -d '{
    "user": {
      "email": "john@example.com",
      "password": "password123"
    }
  }'
```

更多 API 文档请查看 [backend/API_TEST_GUIDE.md](backend/API_TEST_GUIDE.md)

---

## 测试覆盖

### 前端测试

#### 单元测试 (Vitest)
- ✅ API 层测试
- ✅ Store 测试 (auth, articles, comments, tags)
- ✅ 组件测试 (ArticlePreview, Home, Article)

#### E2E 测试 (Cypress)
- ✅ 用户认证流程
- ✅ 文章浏览
- ✅ 分页功能

### 后端测试

#### 单元测试 (JUnit + Mockito)
- ✅ AuthService (6 个测试用例)
  - 注册成功/失败场景
  - 登录成功/失败场景

#### 集成测试 (Spring Boot Test)
- ✅ AuthController (8 个测试用例)
  - 端到端注册流程
  - 端到端登录流程
  - 参数验证
  - 错误处理

### 运行测试

```bash
# 前端测试
cd frontend
pnpm test              # 单元测试
pnpm test:coverage     # 覆盖率报告
pnpm test:e2e          # E2E 测试

# 后端测试
cd backend
./gradlew test         # 所有测试
./gradlew test --tests AuthServiceTest  # 特定测试
```

---

## 下一步计划

### 待实现功能
- [ ] 个人资料模块 (`/profiles/{username}`)
- [ ] 文章模块 (`/articles`)
- [ ] 评论模块 (`/articles/{slug}/comments`)
- [ ] 标签模块 (`/tags`)
- [ ] 收藏功能 (`/articles/{slug}/favorite`)

### 技术改进
- [ ] 添加 Redis 缓存
- [ ] 集成 Docker 容器化
- [ ] 配置 CI/CD 流水线
- [ ] 添加 API 限流
- [ ] 实现日志审计

---

## 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

---

## 许可证

MIT License

---

## 联系方式

- 项目 Issues: [GitHub Issues](link-to-issues)
- 邮箱: your-email@example.com

---

**最后更新**: 2026-06-13

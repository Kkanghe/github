# Java项目代码规范

## 1. 项目概述

### 1.1 适用范围
- **适用项目**: 所有Java项目
- **项目类型**: Spring Boot单体应用、Spring Cloud微服务系统
- **开发语言**: Java 8+
- **构建工具**: Maven/Gradle

### 1.2 推荐技术栈
- **框架版本**:
    - Spring Boot: 2.7.x+ / 3.x+
    - Spring Cloud: 2021.x+ / 2022.x+
    - Spring Security: 5.8.x+ / 6.x+
- **注册中心**: Nacos / Eureka / Consul
- **数据库**: MyBatis Plus / JPA
- **缓存**: Redis / Caffeine
- **文档**: Swagger/OpenAPI 3.0
- **容器化**: Docker
- **CI/CD**: GitLab CI / Jenkins / GitHub Actions

## 2. 项目结构规范

### 2.1 单体应用结构
```
project-name/
├── src/main/java/
│   └── com/company/project/
│       ├── config/                     # 配置类
│       │   ├── handler/               # 处理器配置
│       │   ├── aspect/                # 切面配置
│       │   ├── exception/             # 异常处理配置
│       │   ├── interceptor/           # 拦截器配置
│       │   ├── annotation/            # 自定义注解
│       │   ├── threadpool/            # 线程池配置
│       │   └── listener/              # 监听器配置
│       ├── common/                    # 公共组件
│       │   ├── domain/                # 领域对象
│       │   │   ├── XXXDO/             # 数据对象
│       │   │   ├── vo/                # 视图对象
│       │   │   ├── dto/               # 数据传输对象
│       │   │   └── query/             # 查询对象
│       │   ├── enums/                 # 枚举类
│       │   ├── constants/             # 常量
│       │   ├── properties/            # 配置属性
│       │   ├── utils/                 # 工具类
│       │   └── convert/               # 对象转换器
│       ├── controller/                 # 控制器
│       ├── service/                    # 业务逻辑层
│       ├── mapper/                     # 数据访问层
│       ├── entity/                     # 实体类
│       └── Application.java            # 启动类
├── src/main/resources/
│   ├── application.yml                 # 应用配置
│   ├── application-{profile}.yml       # 环境配置
│   └── logback-spring.xml             # 日志配置
├── src/test/java/                      # 测试代码
├── Dockerfile                          # Docker构建文件
├── .gitignore                          # Git忽略文件
└── pom.xml                             # Maven配置
```

### 2.2 微服务项目结构
```
project-name/
├── project-api/                        # API接口模块
│   ├── src/main/java/
│   │   └── com/company/project/
│   │       ├── api/                    # Feign接口定义
│   │       ├── common/                 # 公共组件
│   │       │   └── pojo/               # 数据对象
│   │       │       ├── dto/            # 数据传输对象
│   │       │       ├── vo/             # 视图对象
│   │       │       ├── do/             # 数据对象
│   │       │       └── query/          # 查询对象
│   │       └── factory/                # 降级工厂类
│   └── pom.xml
├── project-server/                     # 服务实现模块
│   ├── src/main/java/
│   │   └── com/company/project/server/
│   │       ├── config/                 # 配置类
│   │       │   ├── handler/           # 处理器配置
│   │       │   ├── aspect/            # 切面配置
│   │       │   ├── exception/         # 异常处理配置
│   │       │   ├── interceptor/       # 拦截器配置
│   │       │   ├── annotation/        # 自定义注解
│   │       │   ├── threadpool/        # 线程池配置
│   │       │   └── listener/          # 监听器配置
│   │       ├── api/                    # RPC接口实现
│   │       ├── common/                 # 公共组件
│   │       │   ├── constants/         # 常量
│   │       │   ├── enums/             # 枚举类
│   │       │   ├── exception/         # 异常处理
│   │       │   ├── page/              # 分页相关
│   │       │   ├── pojo/              # 数据对象
│   │       │   │   ├── dto/           # 数据传输对象
│   │       │   │   ├── entity/        # 实体类
│   │       │   │   ├── query/         # 查询对象
│   │       │   │   └── vo/            # 视图对象
│   │       │   └── convert/           # 对象转换器
│   │       ├── controller/             # 控制器
│   │       ├── service/                # 业务逻辑层
│   │       │   └── impl/              # 业务实现类
│   │       ├── mapper/                 # 数据访问层
│   │       └── Application.java        # 启动类
│   ├── src/main/resources/
│   │   ├── bootstrap.yml               # 启动配置
│   │   ├── application-{profile}.yml   # 环境配置
│   │   └── logback-spring.xml         # 日志配置
│   ├── Dockerfile                      # Docker构建文件
│   └── pom.xml
├── .gitlab-ci.yml                      # CI/CD配置
├── .gitignore                          # Git忽略文件
└── pom.xml                             # 父级POM
```

### 2.3 包命名规范
- **基础包名**: `com.{company}.{project}`
- **API包名**: `com.{company}.{project}.api`
- **包名使用小写字母，多个单词用点分隔**
- **按功能模块划分包结构**
- **包结构**:
    - `config`: 配置类
        - `handler`: 处理器配置
        - `aspect`: 切面配置
        - `exception`: 异常处理配置
        - `interceptor`: 拦截器配置
        - `annotation`: 自定义注解
        - `threadpool`: 线程池配置
        - `listener`: 监听器配置
    - `api`: RPC接口定义/实现
    - `common`: 公共组件
        - `constants`: 常量
        - `enums`: 枚举类
        - `exception`: 异常处理
        - `page`: 分页相关
        - `pojo`: 数据对象
            - `dto`: 数据传输对象
            - `entity`: 实体类
            - `query`: 查询对象
            - `vo`: 视图对象
        - `convert`: 对象转换器
    - `controller`: REST控制器
    - `service`: 业务服务接口和实现
        - `impl`: 业务实现类
    - `mapper`: 数据访问层

## 3. 编码规范

### 3.1 类命名规范
- **Controller**: 以`Controller`结尾，如`UserController`
- **Service接口**: 以`Service`结尾，如`UserService`
- **Service实现**: 以`ServiceImpl`结尾，如`UserServiceImpl`
- **Entity**: 只能以`DO`结尾，如`UserDO`、`MenuDO`
- **DTO**: 以`DTO`结尾，如`UserCreateDTO`、`UserUpdateDTO`
- **VO**: 以`VO`结尾，如`UserVO`、`UserDetailVO`
- **Query**: 以`Query`结尾，如`UserPageQuery`
- **Mapper**: 以`Mapper`结尾，如`UserMapper`
- **Config**: 以`Config`或`Configuration`结尾
- **Exception**: 以`Exception`结尾
- **Utils**: 以`Utils`或`Util`结尾

### 3.2 方法命名规范
- **查询方法**: `get`、`find`、`list`、`page`、`query`
- **新增方法**: `create`、`save`、`add`、`insert`
- **修改方法**: `update`、`modify`、`edit`
- **删除方法**: `delete`、`remove`
- **校验方法**: `validate`、`check`、`verify`
- **转换方法**: `convert`、`transform`、`map`

### 3.3 变量命名规范
- 使用驼峰命名法
- 常量使用大写字母和下划线
- 布尔变量以`flag`结尾
- 集合变量使用复数形式

### 3.4 注解使用规范
- **API文档**: 使用`@Api`、`@ApiOperation`、`@Schema`、`@Parameter`
- **参数校验**: 使用`@Valid`、`@Validated`、`@NotNull`、`@NotEmpty`
- **权限控制**: 使用`@PreAuthorize`、`@Secured`
- **事务管理**: 使用`@Transactional`
- **缓存**: 使用`@Cacheable`、`@CacheEvict`、`@CachePut`
- **异步**: 使用`@Async`
- **定时任务**: 使用`@Scheduled`

## 4. 配置规范

### 4.1 配置文件结构
- **application.yml**: 主配置文件
- **application-{profile}.yml**: 环境特定配置
- **bootstrap.yml**: 启动配置（微服务项目）
- **logback-spring.xml**: 日志配置

### 4.2 环境配置
- **dev**: 开发环境
- **release**: 测试环境
- **prod**: 生产环境

### 4.3 配置加密
- 使用Jasypt对敏感配置进行加密
- 密码通过环境变量传入
- 敏感信息不得明文存储

### 4.4 配置项命名
- 使用小写字母和连字符
- 层级结构清晰
- 示例：`spring.datasource.url`、`logging.level.com.company`

## 5. 数据库规范

### 5.1 表命名规范
- 使用小写字母和下划线
- 表名使用单数形式
- **MySQL表**: 以`t_`开头，如`t_user`、`t_order`
- **Doris表**: 以业务前缀开头，如`sys_user`、`biz_order`

### 5.2 字段命名规范
- 主键：`id`或`{表名}_id`
- 创建时间：`create_time`
- 更新时间：`update_time`
- 创建者：`created_by`
- 更新者：`updated_by`
- 逻辑删除：`delete_flag`
- 状态字段：`status`

### 5.3 实体类规范
- 使用`@Table`指定表名
- 使用`@Id`指定主键
- 使用`@Column`指定字段映射
- 使用Lombok注解简化代码
- 实现序列化接口

### 5.4 索引规范
- 主键自动创建聚集索引
- 外键字段创建索引
- 查询频繁的字段创建索引
- 复合索引遵循最左前缀原则

## 6. API设计规范

### 6.1 REST API规范
- **GET**: 查询操作，幂等
- **POST**: 创建操作，非幂等
- **PUT**: 更新操作（全量），幂等
- **PATCH**: 更新操作（部分），幂等
- **DELETE**: 删除操作，幂等

### 6.2 URL命名规范
- 使用小写字母和连字符
- 资源名使用复数形式
- 层级关系清晰
- 示例：
    - `GET /api/v1/users` - 获取用户列表
    - `GET /api/v1/users/{id}` - 获取用户详情
    - `POST /api/v1/users` - 创建用户
    - `PUT /api/v1/users/{id}` - 更新用户
    - `DELETE /api/v1/users/{id}` - 删除用户

### 6.3 响应格式规范
```java
public class Result<T> {
    private int code;      // 状态码
    private String message; // 消息
    private T data;        // 数据
    private long timestamp; // 时间戳
}
```

### 6.4 状态码规范
- **200**: 成功
- **400**: 请求参数错误
- **401**: 未认证
- **403**: 无权限
- **404**: 资源不存在
- **500**: 服务器内部错误

### 6.5 分页规范
```java
public class PageQuery {
    private Integer pageNum = 1;        // 页码，从1开始
    private Integer pageSize = 10;      // 页大小
    private String orderBy;             // 排序字段
    private String order = "asc";       // 排序方向：asc/desc
}

public class PageResult<T> {
    private List<T> list;            // 数据列表
    private long total;                 // 总记录数
}
```

## 7. 安全规范

### 7.1 认证授权
- 使用Spring Security进行认证授权
- JWT Token进行无状态认证
- 权限标识格式：`{系统}:{模块}:{操作}`
- 示例：`system:user:create`、`system:role:update`

### 7.2 数据权限
- 支持全部数据权限
- 支持部门数据权限
- 支持个人数据权限
- 支持自定义数据权限

### 7.3 接口安全
- 敏感接口需要权限控制
- 参数校验和SQL注入防护
- XSS攻击防护
- CSRF攻击防护
- 接口限流和防刷

### 7.4 数据安全
- 敏感数据加密存储
- 日志脱敏处理
- 数据传输加密
- 定期备份重要数据

## 8. 日志规范

### 8.1 日志级别
- **ERROR**: 系统错误，需要立即处理
- **WARN**: 警告信息，需要关注
- **INFO**: 一般信息，业务流程记录
- **DEBUG**: 调试信息，开发阶段使用
- **TRACE**: 跟踪信息，详细的执行路径

### 8.2 日志格式
```
%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
```

### 8.3 日志内容规范
- 关键业务操作必须记录日志
- 异常信息必须记录完整堆栈
- 敏感信息不得记录到日志
- 使用结构化日志格式
- 包含必要的上下文信息

### 8.4 日志输出
- 开发环境：控制台输出
- 测试环境：文件输出
- 生产环境：文件输出 + 日志收集系统
- 日志文件按日期滚动
- 设置合理的日志保留期

## 9. 异常处理规范

### 9.1 异常分类
- **业务异常**: 可预期的业务逻辑异常
- **系统异常**: 不可预期的系统级异常
- **参数异常**: 请求参数校验异常

### 9.2 异常处理
- 使用`@ControllerAdvice`全局异常处理
- 自定义业务异常类
- 异常信息国际化
- 不向前端暴露系统内部信息

### 9.3 异常码规范
- 使用数字错误码
- 按模块分段管理
- 错误码与错误信息分离
- 提供错误码文档

## 10. 测试规范

### 10.1 单元测试
- 使用JUnit 5
- 使用Mockito进行Mock
- 测试覆盖率要求：>80%
- 测试方法命名：`should_ExpectedBehavior_When_StateUnderTest`

### 10.2 集成测试
- 使用TestContainers
- 使用内存数据库（H2）
- 测试真实的业务场景
- 测试数据隔离

### 10.3 测试数据
- 使用测试专用数据
- 测试数据可重复执行
- 清理测试产生的数据
- 不依赖外部环境

## 11. 部署规范

### 11.1 Docker规范
- 使用官方基础镜像
- 多阶段构建减小镜像大小
- 设置合理的JVM参数
- 健康检查配置
- 非root用户运行

### 11.2 CI/CD规范
- 代码提交触发自动构建
- 自动化测试
- 代码质量检查
- 自动化部署
- 回滚机制

### 11.3 环境管理
- 环境隔离
- 配置外部化
- 蓝绿部署
- 灰度发布

### 11.4 版本管理
- 语义化版本号：`主版本.次版本.修订版本`
- Git标签管理版本
- 变更日志记录
- 版本兼容性说明

## 12. 代码质量规范

### 12.1 代码检查
- 使用SonarQube进行代码质量检查
- 代码重复率：<3%
- 代码复杂度：<10
- 代码覆盖率：>80%

### 12.2 代码审查
- 所有代码必须经过审查
- 审查清单标准化
- 及时反馈和修改
- 知识分享和传承

### 12.3 依赖管理
- 统一管理依赖版本
- 定期更新依赖版本
- 避免使用快照版本
- 依赖安全扫描

### 12.4 文档规范
- 类和方法必须有JavaDoc注释
- 复杂业务逻辑必须有注释说明
- API接口必须有文档
- README文件完整
- 架构设计文档

## 13. 性能规范

### 13.1 缓存策略
- 合理使用缓存
- 缓存Key规范：`{模块}:{业务}:{标识}`
- 设置合理的过期时间
- 缓存穿透、击穿、雪崩防护

### 13.2 数据库优化
- 合理使用索引
- 避免N+1查询
- 使用分页查询大数据量
- 读写分离
- 分库分表

### 13.3 接口性能
- 接口响应时间：<500ms
- 并发处理能力：>1000 TPS
- 异步处理耗时操作
- 接口限流保护

### 13.4 JVM优化
- 合理设置堆内存大小
- 选择合适的垃圾收集器
- JVM参数调优
- 内存泄漏监控

## 14. 监控规范

### 14.1 应用监控
- 使用Spring Boot Actuator
- 监控端点：`/actuator/health`、`/actuator/metrics`
- 自定义健康检查
- 应用性能监控（APM）

### 14.2 日志监控
- 使用ELK Stack进行日志分析
- 关键业务操作必须记录日志
- 异常日志告警
- 日志统计分析

### 14.3 链路追踪
- 使用分布式链路追踪
- 请求链路可视化
- 性能瓶颈分析
- 依赖关系梳理

### 14.4 告警机制
- 系统异常告警
- 性能指标告警
- 业务指标告警
- 告警升级机制

## 15. 开发流程规范

### 15.1 分支管理
- 使用Git Flow工作流
- 主分支：`master`
- 开发分支：`develop`
- 功能分支：`feature/*`
- 发布分支：`release/*`
- 热修复分支：`hotfix/*`

### 15.2 提交规范
- 提交信息格式：`type(scope): description`
- 类型：`feat`、`fix`、`docs`、`style`、`refactor`、`test`、`chore`
- 提交粒度要合适
- 避免大量文件的单次提交

### 15.3 代码审查
- Pull Request/Merge Request流程
- 至少一人审查
- 自动化检查通过
- 及时处理审查意见

### 15.4 发布流程
- 版本规划
- 功能测试
- 性能测试
- 安全测试
- 生产发布
- 发布验证

## 16. 对象转换规范

### 16.1 转换器命名
- 使用`Converter`结尾
- 示例：`OrderConverter`

### 16.2 转换工具
- 推荐使用MapStruct进行对象转换
- 避免手动编写转换代码
- 支持复杂对象映射

### 16.3 转换规范
```java
@Mapper
public interface UserConverter {
    UserConverter INSTANCE = Mappers.getMapper(UserConverter.class);
    
    UserVO toVO(UserEntity entity);
    UserEntity toEntity(UserCreateDTO dto);
    List<UserVO> toVOList(List<UserEntity> entities);
}
```

## 17. 常量管理规范

### 17.1 常量分类
- **系统常量**: 系统级别的配置常量
- **业务常量**: 业务逻辑相关常量
- **错误码常量**: 错误码定义
- **缓存常量**: 缓存Key相关常量

### 17.2 常量定义
- 使用`public static final`修饰
- 常量名使用大写字母和下划线
- 按功能模块分类管理
- 提供清晰的注释说明

### 17.3 常量类示例
```java
public class UserConstants {
    /** 用户状态 - 正常 */
    public static final Integer STATUS_NORMAL = 1;
    /** 用户状态 - 禁用 */
    public static final Integer STATUS_DISABLED = 0;
    /** 默认密码 */
    public static final String DEFAULT_PASSWORD = "123456";
}
```

## 18. 枚举使用规范

### 18.1 枚举定义
- 实现通用接口（如`CodeEnum`）
- 提供code和message属性
- 重写toString方法
- 提供静态方法根据code获取枚举

### 18.2 枚举示例
```java
public enum UserStatusEnum implements CodeEnum {
    NORMAL(1, "正常"),
    DISABLED(0, "禁用");
    
    private final Integer code;
    private final String message;
    
    UserStatusEnum(Integer code, String message) {
        this.code = code;
        this.message = message;
    }
    
    public static UserStatusEnum getByCode(Integer code) {
        for (UserStatusEnum status : values()) {
            if (status.getCode().equals(code)) {
                return status;
            }
        }
        return null;
    }
}
```

## 19. 工具类规范

### 19.1 工具类设计
- 工具类应该是无状态的
- 构造函数私有化
- 所有方法都是静态方法
- 方法应该是纯函数（无副作用）

### 19.2 常用工具类
- **StringUtil**: 字符串处理工具
- **DateUtil**: 日期时间工具
- **JsonUtil**: JSON序列化工具
- **BeanUtil**: 对象属性复制工具
- **ValidationUtil**: 参数校验工具
- **EncryptUtil**: 加密解密工具

### 19.3 工具类示例
```java
public class StringUtil {
    private StringUtils() {
        throw new UnsupportedOperationException();
    }
    
    public static boolean isEmpty(String str) {
        return str == null || str.length() == 0;
    }
    
    public static boolean isNotEmpty(String str) {
        return !isEmpty(str);
    }
}

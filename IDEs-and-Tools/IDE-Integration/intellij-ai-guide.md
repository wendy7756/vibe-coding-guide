# IntelliJ IDEA + AI 完整指南

[English](./intellij-ai-guide-en.md) | 中文

## 目录
1. [概述](#概述)
2. [AI功能配置](#ai功能配置)
3. [智能代码生成](#智能代码生成)
4. [AI辅助重构](#ai辅助重构)
5. [自动化测试](#自动化测试)
6. [代码审查](#代码审查)
7. [性能优化](#性能优化)
8. [最佳实践](#最佳实践)

## 概述

IntelliJ IDEA作为Java开发的首选IDE，集成了强大的AI功能，为Java开发者提供智能编程体验。本指南专注于Java开发中的AI应用。

### 主要AI功能
- **智能代码补全**: 基于上下文的精准Java代码建议
- **重构建议**: 智能的代码重构和现代化建议
- **测试生成**: 自动生成JUnit测试用例
- **错误修复**: AI驱动的代码错误检测和修复
- **性能优化**: 智能的性能优化建议

## AI功能配置

### 1. JetBrains AI Assistant

#### 安装步骤
```bash
# 通过插件管理器安装
File -> Settings -> Plugins -> Marketplace
搜索 "JetBrains AI Assistant" -> Install
```

#### 基础配置
```xml
<!-- .idea/workspace.xml -->
<component name="AIAssistantSettings">
  <option name="enableCodeCompletion" value="true" />
  <option name="enableJavaOptimizations" value="true" />
  <option name="enableTestGeneration" value="true" />
  <option name="showInlineHints" value="true" />
</component>
```

### 2. GitHub Copilot配置

#### Java特定设置
```json
{
  "github.copilot.enable": {
    "java": true,
    "kotlin": true,
    "gradle": true,
    "maven": true
  },
  "github.copilot.inlineSuggest.enable": true
}
```

## 智能代码生成

### 1. 从注释生成代码

#### 服务层代码生成
```java
/**
 * 用户服务类，处理用户相关的业务逻辑
 * 包括用户注册、登录、信息更新等功能
 */
@Service
@Transactional
public class UserService {

    @Autowired
    private UserRepository userRepository;
    
    @Autowired
    private PasswordEncoder passwordEncoder;

    // TODO: 实现用户注册方法，需要验证邮箱唯一性
    // AI会生成以下完整实现
    public UserDto registerUser(UserRegistrationDto registrationDto) {
        // 检查邮箱是否已存在
        if (userRepository.existsByEmail(registrationDto.getEmail())) {
            throw new EmailAlreadyExistsException("邮箱已被使用");
        }
        
        // 创建新用户
        User user = new User();
        user.setEmail(registrationDto.getEmail());
        user.setPassword(passwordEncoder.encode(registrationDto.getPassword()));
        user.setFirstName(registrationDto.getFirstName());
        user.setLastName(registrationDto.getLastName());
        user.setCreatedAt(LocalDateTime.now());
        user.setEnabled(true);
        
        User savedUser = userRepository.save(user);
        return convertToDto(savedUser);
    }
}
```

### 2. Spring Boot应用生成

#### Controller自动生成
```java
// 输入：创建RESTful API for Product management
@RestController
@RequestMapping("/api/v1/products")
@Validated
@Slf4j
public class ProductController {

    private final ProductService productService;

    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    @GetMapping
    public ResponseEntity<Page<ProductDto>> getAllProducts(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size,
            @RequestParam(defaultValue = "id") String sortBy) {
        
        Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
        Page<ProductDto> products = productService.getAllProducts(pageable);
        return ResponseEntity.ok(products);
    }

    @GetMapping("/{id}")
    public ResponseEntity<ProductDto> getProductById(@PathVariable Long id) {
        ProductDto product = productService.getProductById(id);
        return ResponseEntity.ok(product);
    }

    @PostMapping
    public ResponseEntity<ProductDto> createProduct(
            @Valid @RequestBody CreateProductDto createProductDto) {
        
        ProductDto createdProduct = productService.createProduct(createProductDto);
        return ResponseEntity.status(HttpStatus.CREATED).body(createdProduct);
    }

    @PutMapping("/{id}")
    public ResponseEntity<ProductDto> updateProduct(
            @PathVariable Long id,
            @Valid @RequestBody UpdateProductDto updateProductDto) {
        
        ProductDto updatedProduct = productService.updateProduct(id, updateProductDto);
        return ResponseEntity.ok(updatedProduct);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
        productService.deleteProduct(id);
        return ResponseEntity.noContent().build();
    }
}
```

### 3. 数据库相关代码

#### Repository和Entity生成
```java
// Entity
@Entity
@Table(name = "orders")
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Order {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true)
    private String orderNumber;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "customer_id", nullable = false)
    private Customer customer;
    
    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<OrderItem> orderItems = new ArrayList<>();
    
    @Enumerated(EnumType.STRING)
    private OrderStatus status;
    
    @Column(nullable = false)
    private BigDecimal totalAmount;
    
    @CreationTimestamp
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    private LocalDateTime updatedAt;
}

// Repository
@Repository
public interface OrderRepository extends JpaRepository<Order, Long> {
    
    @Query("SELECT o FROM Order o WHERE o.customer.id = :customerId AND o.status = :status")
    List<Order> findByCustomerIdAndStatus(@Param("customerId") Long customerId, 
                                         @Param("status") OrderStatus status);
    
    @Query("SELECT o FROM Order o WHERE o.createdAt BETWEEN :startDate AND :endDate")
    List<Order> findOrdersByDateRange(@Param("startDate") LocalDateTime startDate,
                                    @Param("endDate") LocalDateTime endDate);
    
    Optional<Order> findByOrderNumber(String orderNumber);
    
    @Modifying
    @Query("UPDATE Order o SET o.status = :status WHERE o.id = :orderId")
    int updateOrderStatus(@Param("orderId") Long orderId, @Param("status") OrderStatus status);
}
```

## AI辅助重构

### 1. 代码现代化

#### 从传统Java到现代Java
```java
// 原始代码 (Java 8之前的风格)
public class OrderProcessor {
    
    public List<Order> processOrders(List<Order> orders) {
        List<Order> validOrders = new ArrayList<>();
        for (Order order : orders) {
            if (order.getStatus() == OrderStatus.PENDING) {
                validOrders.add(order);
            }
        }
        
        Collections.sort(validOrders, new Comparator<Order>() {
            @Override
            public int compare(Order o1, Order o2) {
                return o1.getCreatedAt().compareTo(o2.getCreatedAt());
            }
        });
        
        List<Order> processedOrders = new ArrayList<>();
        for (Order order : validOrders) {
            Order processed = processOrder(order);
            processedOrders.add(processed);
        }
        
        return processedOrders;
    }
}

// AI重构后 (现代Java风格)
@Component
public class OrderProcessor {
    
    public List<Order> processOrders(List<Order> orders) {
        return orders.stream()
                .filter(order -> order.getStatus() == OrderStatus.PENDING)
                .sorted(Comparator.comparing(Order::getCreatedAt))
                .map(this::processOrder)
                .collect(Collectors.toList());
    }
}
```

### 2. 设计模式应用

#### 引入设计模式
```java
// 原始代码：硬编码的支付处理
public class PaymentService {
    
    public void processPayment(PaymentRequest request) {
        if (request.getType().equals("CREDIT_CARD")) {
            // 信用卡支付逻辑
            processCreditCardPayment(request);
        } else if (request.getType().equals("PAYPAL")) {
            // PayPal支付逻辑
            processPayPalPayment(request);
        } else if (request.getType().equals("BANK_TRANSFER")) {
            // 银行转账逻辑
            processBankTransferPayment(request);
        }
    }
}

// AI建议使用策略模式重构
public interface PaymentStrategy {
    PaymentResult process(PaymentRequest request);
}

@Component("creditCardPayment")
public class CreditCardPaymentStrategy implements PaymentStrategy {
    @Override
    public PaymentResult process(PaymentRequest request) {
        // 信用卡支付实现
        return PaymentResult.success();
    }
}

@Component("paypalPayment")
public class PayPalPaymentStrategy implements PaymentStrategy {
    @Override
    public PaymentResult process(PaymentRequest request) {
        // PayPal支付实现
        return PaymentResult.success();
    }
}

@Service
public class PaymentService {
    
    private final Map<String, PaymentStrategy> strategies;
    
    public PaymentService(Map<String, PaymentStrategy> strategies) {
        this.strategies = strategies;
    }
    
    public PaymentResult processPayment(PaymentRequest request) {
        PaymentStrategy strategy = strategies.get(request.getType() + "Payment");
        if (strategy == null) {
            throw new UnsupportedPaymentTypeException("不支持的支付类型: " + request.getType());
        }
        return strategy.process(request);
    }
}
```

## 自动化测试

### 1. 单元测试生成

#### Service层测试
```java
// 原始服务类
@Service
public class UserService {
    
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    
    public UserService(UserRepository userRepository, PasswordEncoder passwordEncoder) {
        this.userRepository = userRepository;
        this.passwordEncoder = passwordEncoder;
    }
    
    public User createUser(CreateUserDto createUserDto) {
        if (userRepository.existsByEmail(createUserDto.getEmail())) {
            throw new EmailAlreadyExistsException("Email already exists");
        }
        
        User user = User.builder()
                .email(createUserDto.getEmail())
                .password(passwordEncoder.encode(createUserDto.getPassword()))
                .firstName(createUserDto.getFirstName())
                .lastName(createUserDto.getLastName())
                .build();
                
        return userRepository.save(user);
    }
}

// AI生成的测试类
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    
    @Mock
    private UserRepository userRepository;
    
    @Mock
    private PasswordEncoder passwordEncoder;
    
    @InjectMocks
    private UserService userService;
    
    @Test
    @DisplayName("成功创建用户")
    void shouldCreateUserSuccessfully() {
        // Given
        CreateUserDto createUserDto = CreateUserDto.builder()
                .email("test@example.com")
                .password("password123")
                .firstName("John")
                .lastName("Doe")
                .build();
        
        when(userRepository.existsByEmail(createUserDto.getEmail())).thenReturn(false);
        when(passwordEncoder.encode(createUserDto.getPassword())).thenReturn("encodedPassword");
        
        User savedUser = User.builder()
                .id(1L)
                .email(createUserDto.getEmail())
                .password("encodedPassword")
                .firstName(createUserDto.getFirstName())
                .lastName(createUserDto.getLastName())
                .build();
        
        when(userRepository.save(any(User.class))).thenReturn(savedUser);
        
        // When
        User result = userService.createUser(createUserDto);
        
        // Then
        assertThat(result).isNotNull();
        assertThat(result.getEmail()).isEqualTo(createUserDto.getEmail());
        assertThat(result.getFirstName()).isEqualTo(createUserDto.getFirstName());
        assertThat(result.getLastName()).isEqualTo(createUserDto.getLastName());
        
        verify(userRepository).existsByEmail(createUserDto.getEmail());
        verify(passwordEncoder).encode(createUserDto.getPassword());
        verify(userRepository).save(any(User.class));
    }
    
    @Test
    @DisplayName("邮箱已存在时抛出异常")
    void shouldThrowExceptionWhenEmailExists() {
        // Given
        CreateUserDto createUserDto = CreateUserDto.builder()
                .email("existing@example.com")
                .password("password123")
                .firstName("Jane")
                .lastName("Doe")
                .build();
        
        when(userRepository.existsByEmail(createUserDto.getEmail())).thenReturn(true);
        
        // When & Then
        assertThatThrownBy(() -> userService.createUser(createUserDto))
                .isInstanceOf(EmailAlreadyExistsException.class)
                .hasMessage("Email already exists");
        
        verify(userRepository).existsByEmail(createUserDto.getEmail());
        verifyNoMoreInteractions(passwordEncoder, userRepository);
    }
}
```

### 2. 集成测试生成

#### Controller集成测试
```java
@SpringBootTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@TestPropertySource(locations = "classpath:application-test.properties")
@Transactional
class ProductControllerIntegrationTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @Autowired
    private ObjectMapper objectMapper;
    
    @Autowired
    private ProductRepository productRepository;
    
    @Test
    @DisplayName("创建产品 - 成功案例")
    void shouldCreateProductSuccessfully() throws Exception {
        // Given
        CreateProductDto createProductDto = CreateProductDto.builder()
                .name("iPhone 15")
                .description("Latest iPhone model")
                .price(new BigDecimal("999.99"))
                .categoryId(1L)
                .build();
        
        // When & Then
        mockMvc.perform(post("/api/v1/products")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(createProductDto)))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.name").value("iPhone 15"))
                .andExpect(jsonPath("$.description").value("Latest iPhone model"))
                .andExpect(jsonPath("$.price").value(999.99))
                .andExpect(jsonPath("$.id").exists());
        
        // 验证数据库中确实创建了产品
        Optional<Product> savedProduct = productRepository.findByName("iPhone 15");
        assertThat(savedProduct).isPresent();
        assertThat(savedProduct.get().getDescription()).isEqualTo("Latest iPhone model");
    }
    
    @Test
    @DisplayName("获取产品列表 - 分页查询")
    void shouldGetProductsWithPagination() throws Exception {
        // Given - 创建测试数据
        List<Product> products = IntStream.range(1, 6)
                .mapToObj(i -> Product.builder()
                        .name("Product " + i)
                        .description("Description " + i)
                        .price(new BigDecimal(i * 100))
                        .build())
                .collect(Collectors.toList());
        
        productRepository.saveAll(products);
        
        // When & Then
        mockMvc.perform(get("/api/v1/products")
                        .param("page", "0")
                        .param("size", "3")
                        .param("sortBy", "name"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.content").isArray())
                .andExpect(jsonPath("$.content", hasSize(3)))
                .andExpect(jsonPath("$.totalElements").value(5))
                .andExpect(jsonPath("$.totalPages").value(2))
                .andExpect(jsonPath("$.first").value(true))
                .andExpected(jsonPath("$.last").value(false));
    }
}
```

## 代码审查

### AI驱动的代码审查

#### 安全性检查
```java
// AI检测到的安全问题
@RestController
public class UserController {
    
    // ❌ 安全问题：SQL注入风险
    @GetMapping("/users/search")
    public List<User> searchUsers(@RequestParam String query) {
        String sql = "SELECT * FROM users WHERE name LIKE '%" + query + "%'";
        return jdbcTemplate.query(sql, userRowMapper);
    }
    
    // ✅ AI建议的修复
    @GetMapping("/users/search")
    public List<User> searchUsers(@RequestParam String query) {
        String sql = "SELECT * FROM users WHERE name LIKE ?";
        return jdbcTemplate.query(sql, userRowMapper, "%" + query + "%");
    }
}
```

#### 性能问题检测
```java
// AI检测到的性能问题
@Service
public class OrderService {
    
    // ❌ N+1查询问题
    public List<OrderDto> getAllOrdersWithItems() {
        List<Order> orders = orderRepository.findAll();
        return orders.stream()
                .map(order -> {
                    List<OrderItem> items = orderItemRepository.findByOrderId(order.getId());
                    return mapToDto(order, items);
                })
                .collect(Collectors.toList());
    }
    
    // ✅ AI建议的优化
    public List<OrderDto> getAllOrdersWithItems() {
        List<Order> orders = orderRepository.findAllWithItems();
        return orders.stream()
                .map(this::mapToDto)
                .collect(Collectors.toList());
    }
}

// Repository优化
@Repository
public interface OrderRepository extends JpaRepository<Order, Long> {
    
    @Query("SELECT DISTINCT o FROM Order o LEFT JOIN FETCH o.orderItems")
    List<Order> findAllWithItems();
}
```

## 性能优化

### 1. 数据库性能优化

#### 查询优化建议
```java
// AI分析慢查询并提供优化建议
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    
    // ❌ 原始查询可能较慢
    @Query("SELECT p FROM Product p WHERE p.category.name = :categoryName " +
           "AND p.price BETWEEN :minPrice AND :maxPrice " +
           "AND p.available = true")
    List<Product> findProductsByCriteria(@Param("categoryName") String categoryName,
                                       @Param("minPrice") BigDecimal minPrice,
                                       @Param("maxPrice") BigDecimal maxPrice);
    
    // ✅ AI优化建议：添加索引和查询优化
    @Query(value = "SELECT p.* FROM products p " +
                   "INNER JOIN categories c ON p.category_id = c.id " +
                   "WHERE c.name = :categoryName " +
                   "AND p.price BETWEEN :minPrice AND :maxPrice " +
                   "AND p.available = true " +
                   "ORDER BY p.created_at DESC",
           nativeQuery = true)
    List<Product> findProductsByCriteriaOptimized(@Param("categoryName") String categoryName,
                                                @Param("minPrice") BigDecimal minPrice,
                                                @Param("maxPrice") BigDecimal maxPrice);
}
```

### 2. 缓存策略

#### 智能缓存实现
```java
@Service
@CacheConfig(cacheNames = "products")
public class ProductService {
    
    private final ProductRepository productRepository;
    private final RedisTemplate<String, Object> redisTemplate;
    
    // AI建议的缓存策略
    @Cacheable(key = "#id", unless = "#result == null")
    public ProductDto getProductById(Long id) {
        return productRepository.findById(id)
                .map(this::convertToDto)
                .orElseThrow(() -> new ProductNotFoundException("Product not found: " + id));
    }
    
    @Cacheable(key = "'category:' + #categoryId + ':page:' + #pageable.pageNumber")
    public Page<ProductDto> getProductsByCategory(Long categoryId, Pageable pageable) {
        return productRepository.findByCategoryId(categoryId, pageable)
                .map(this::convertToDto);
    }
    
    @CacheEvict(key = "#result.id")
    public ProductDto updateProduct(Long id, UpdateProductDto updateDto) {
        Product product = productRepository.findById(id)
                .orElseThrow(() -> new ProductNotFoundException("Product not found: " + id));
        
        updateProductFields(product, updateDto);
        Product savedProduct = productRepository.save(product);
        
        return convertToDto(savedProduct);
    }
    
    @CacheEvict(allEntries = true)
    public void clearProductCache() {
        // 清除所有产品缓存
    }
}
```

## 最佳实践

### 1. AI辅助开发流程

```markdown
## 开发流程最佳实践

### 1. 需求分析阶段
- 使用AI生成详细的用户故事
- 创建技术规范文档
- 生成API设计文档

### 2. 编码阶段
- 先写注释描述功能，让AI生成基础代码
- 使用AI进行代码审查
- 自动生成单元测试

### 3. 测试阶段
- AI生成测试用例
- 自动化集成测试
- 性能测试建议

### 4. 优化阶段
- AI分析性能瓶颈
- 代码重构建议
- 安全漏洞检测
```

### 2. 团队协作规范

```java
// 团队AI使用规范示例
@TeamAIGuidelines
public class TeamStandards {
    
    /**
     * AI生成代码的审查清单：
     * 1. 业务逻辑正确性
     * 2. 异常处理完整性
     * 3. 测试覆盖率
     * 4. 性能考虑
     * 5. 安全性检查
     */
    
    // ✅ 好的AI提示示例
    // AI: 创建一个用户服务类，包含CRUD操作，需要：
    // 1. 数据验证
    // 2. 异常处理
    // 3. 事务管理
    // 4. 审计日志
    
    // ❌ 不好的AI提示示例
    // AI: 写个用户类
}
```

### 3. 代码质量保证

```yaml
# AI辅助的质量检查流程
quality_gates:
  - name: "AI Code Review"
    tools:
      - jetbrains_ai_assistant
      - sonarqube
      - checkstyle
    
  - name: "Security Scan"
    tools:
      - snyk
      - owasp_dependency_check
    
  - name: "Performance Analysis"
    tools:
      - jmeter
      - apache_bench
```

---

*最后更新: 2025年*

[返回顶部](#intellij-idea--ai-完整指南) | [English](./intellij-ai-guide-en.md) 